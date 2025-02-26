# Amharic Text Moderation Pipeline Architecture

![Pipeline Architecture Diagram](/Diagram/RLLTZ-Cq57tthxYAj6YgRSKm2n8QQT3sezLADAlIj824qCfrRXDJnmwsCxiHudtWcMVUu0t-K_y9jaEoIJHzQ5hxdFjnZg_psbYgRLK8GYot0c5Uv5Hp1WVyO25MAMfgkPAmuoKABf6GqX4uuoML5gAZGHq1DN0Shk-eHlVSAUE-j69eZ6g0kzrk28tHq.png)  
*End-to-End Architecture for Real-Time Amharic Text Moderation You can view the pipeline diagram in SVG format [here](https://www.plantuml.com/plantuml/svg/RPNVZkCq5CRl_HH7aHPDHIk6MP3GI8EsVrgjHBkgcXQG45gvpcbYwjZ1TcOtGjmNU0Gan1Kt2ExOz-cRO3kRR1BDNcmczlSTdtD-FkaBOwcsPIu8iTmAX6cUKSqPxF6jXOrAK5FBbOGjBr1mYOGKpi0PBwYq41qCwWYeWKD_VKirkkTM6VUVLWoDKRLmkztsfHkqDA6MGcoLfYd2pSAz7Qd1KJ1iuhv-hl8SvJ3iV11rXXbzv2wWWAcaeZBS1DrisjSja77Z2rpAb4iCciMoh-cqOShymzI93KAj49CZPMTOArK4nMfDoCC3FD4CBbEusMfaAYzAYya87Xx80IPV-lxSmrmZjVZ9eKZS8nY9Ms-tbzB1gc3dxAda8R6Rz-0ci-LkFmPJq7arwfdsgd1SvuAwqq-SqThsxNgpKqVKbhRgJNmVM20qQ3f82Dd4RSWFw5Y6EILIMGJDqyo2EdbmFn60g73fl-P9T0yHFR9Fxvv7Ox-ClWYEngr_5rr__Ujw-UVwoxlhR--kb_-YCTHB_rulVqGGtlwyNdw_NlwElWzkwwkflKkRIGV1LjwrLO9RlrFBoj31v3Mr_lYxsxlF9hTVJ5mAv6U2CW6VSM0qk5MEJqjaxYgDosFERQCYyxPHAxGiQmWt_N3xhT6NwJtjDUoZ6hNQfx7MnK4iIct6y1LMRvHEJDSL9dM8zQM_Dt61oB8np2i7-5WAKRco6kji6f9BsiezOZWf3NwcePcVDktGfIUcohTfDcqYpZDavph2IswiqjLmCznctzwLnXzBbAnHB9PEGGKhXSzznyqPOgPqZMTHIPfp1eDnzOSlberxcgOQK-yEHjDh0tn--mm-xl1u7jwNxsyXtDq-6tLZ9J-Kni8-St4o9H83Csem0IKRs66UJDTI5CBHAmLwngLLavbGx3o6fM7K5pM6EAE9UkD2IJT8L5Zu82FW_jN1DgvNOQrX4_OseKk7UtYbB3zLTPDlsi_X3dFrY4aWs2ax6X4K1jiS1iU46n0iPKwb2_B8yKrmT78TUDQyCmhmjUDnv8BRoWyK8NMQgxNJgRJx2zAW2pnxtqfFSRLkR7ljrrTKcF3bStGUqS17yCgX3NztjDyWddtFqMhAfRzLwXJE55tLHacRETaQttAc9DIVLKF82vUn_-tx7m00).*

---

## 1. Parent Post(Comment) Processing (Precomputed)
**When a post(Comment) is created/updated**:
- **Entity Recognition**: Extract named entities (e.g., `"ኦሮሞ"`, `"ኦርቶዶክስ"`) using  *Amharic-BERT*.  
- **Topic Classification**: Assign categories (`Religion`, `Ethnicity`, `Politics`) via a fine-tuned *XLMRoberta* model.  
- **Metadata Storage**:    
  - **Mongo**: For long-term storage and auditability.  

**Metadata Schema**:  
```json
{
  "post_id": "abc123",
  "entities": ["ብሔር", "ኦሮሞ"],
  "topics": ["Ethnicity", "Politics"],
  "updated_at": "2024-08-23"
}
```

---

## 2. Comment Processing
**Input**: Comment text + Parent Post(comment) ID.  
**Workflow**:  
1. **Fetch Parent Metadata**: Retrieve precomputed entities/topics from Redis.  
2. **Analyze Comment**:  
   - **Sentiment Analysis**: Score negativity (0–1) using *Amharic-BERT*.  
   - **Entity Recognition**: Detect ethnic slurs or sensitive terms.  
   - **Text Classification**: Predict probabilities for `Hate Speech`, `Cyberbullying`, and `Explicit Content`.  

---

## 3. Behavioral Analysis
- **User History Check**:  
  - Past flagged content.  
  - Activity spikes (e.g., 50+ comments/hour).  
- **Risk Score**:  
  - Repeat offenders (≥3 flags) receive higher scores.  

---

## 4. Dynamic Decision Engine
### Aggregation Logic  
| Component         | Weight | Threshold Adjustment by Topic       |  
|-------------------|--------|--------------------------------------|  
| Hate Speech       | 50%    | Ethnicity: 70%, Religion: 75%       |  
| Sentiment         | 30%    | Politics: 0.7 sentiment threshold    |  
| Entities          | 20%    | Stricter rules for ethnic slurs      |  

### Rule-Based Actions  
- **Auto-Block**:  
  - `IF (hate_speech > threshold) OR (parent_entity = "ብሔር" AND comment_entity = "አማራ")`  
- **Escalate**:  
  - `IF (60% < hate_speech < 80%) OR (parent_topic = "Politics" AND sentiment > 0.7)`  
- **Shadow Ban**:  
  - `IF user_risk_score > 90%` (e.g., repeat offenders with 5+ flags).  

**Output Example**:  
`Blocked: Hate speech (85%) + Parent topic (Ethnicity)`  

---

## 5. Post-Moderation Actions  
- **User Notification**:  
  - *"Your comment was removed for violating our hate speech policy."*  
- **Appeals Process**:  
  - Human-reviewed form with timestamps and logs.  
- **Shadow Banning**:  
  - Restrict toxic users’ visibility without notification.  

---

## 6. Feedback Loop  
- **Logging**: Track false positives/negatives.  
- **Retraining**: Weekly model updates with new flagged data.  
- **Lexicon Updates**: Monthly refresh of cultural terms (e.g., new slurs).  

---

## Key Features  
| Feature                  | Description                                                                 |  
|--------------------------|-----------------------------------------------------------------------------|  
| **Decoupled Parent Analysis** | Metadata precomputed once (no real-time reprocessing).                     |  
| **Context-Aware Rules**       | Parent topics/entities dynamically adjust decision thresholds.             |  
| **Behavioral Integration**    | User history and risk scores enhance moderation accuracy.                  |  
| **Human-in-the-Loop**         | Manual appeals and reviews for borderline cases.                           |  

---

## Tools & Infrastructure  
- **NLP Models**: *Amharic-BERT*, *spaCy*, *XLMRoberta*.  
- **Databases**: *Mongo* (user logs).  
- **Deployment**: *FastAPI* (real-time API).  
