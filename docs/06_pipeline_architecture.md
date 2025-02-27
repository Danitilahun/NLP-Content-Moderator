# Amharic Text Moderation Pipeline Architecture

![Pipeline Architecture Diagram](/Diagram/RLNTZkCq5BxtKnn5MZGL7J7CWeH66hJzQLc9Tgdw0qW8hLpdD35rx60xiriXxWiy0XBYYXi4T-pxz4quTYRPj9gRoSJvllFpVUUuBvpdrbU5ObvwXJ0eScwbW3M-zJ0tALhkfT6ma2KggP6nal1Io99h3yd6eKs0EzYSdo-uHNekZAC_r.png)  
*End-to-End Architecture for Real-Time Amharic Text Moderation You can view the pipeline diagram in SVG format [here](https://www.plantuml.com/plantuml/svg/RLNTZkCq5BxtKnn5MZGL7J7CWeH66hJzQLc9Tgdw0qW8hLpdD35rx60xiriXxWiy0XBYYXi4T-pxz4quTYRPj9gRoSJvllFpVUUuBvpdrbU5ObvwXJ0eScwbW3M-zJ0tALhkfT6ma2KggP6nal1Io99h3yd6eKs0EzYSdo-uHNekZAC_rWXqpjJ0nM9n3fsZvodt75RUM9uXN8tfRSiTzY9XlZh7ZqnHeBuCExg8EiISFqWAg62WkJeuwI9kE3Z7ZL585ngSw8pQYvZnv1pJaM4WmiFLXLs4cYAcMoxsC3EcZ8ZfZB7xUtX23Aapk5fO5AOeAuzf3-xlsGQkFm_wtC788lVuqQPCwH69ZCxRpnDDPXrWIVHCorZOrQDnryF9Sjq7L_BHeNT6MfkIV1qfJjbtKl2QzkrilZHRj9xVKHv5mOJhmyJdMWhAqQSaIcO4xSCNg97qRAAICNVHCuJ6mevrZCrNRUht5eiS2ywqyGXMPha7imi6_yG0afBQV2tJv0uIlXKVtpvF-k4OGxCI7Pr_bvn-_Ujq_EVqoxlJR-zEn_-IFjH7_vwEVzGlVvwElv-EVoVVHx8FJTVKjgU0QrfzX5LHwFGrzo7xxStj9zStdrrJ1UndXZg5K72qycBuoCRMk14rkggsXVGDYerQdQReHTuCGYC7VM-9eSl0QQVrtD5UYttQ_RevMAdAadrVuk6DiQdhik92Nxh_CepNgaGKUH--skrGE-p34BNCT4CU3c9vQTjxy1Xsna9OVcWMhIqywlJ4-WMXXeCcuYX7iQyZl9JE6tku_1Z7FWWyjVXZXLeqYF6445o9IeNgbzBjQQwChGqQ7pGlf82BlGx9nvE6FSWoYrbWHw8x4m8-lNa67tOSUHxV9uzZ2BStpthTMEaFbVEmpYbERbJgOCWTfc1qOtTSFDUbbAKY_og5mUNAc-kXCc9FQ-S43qtrOPNprBoXK6G3uyh3UnW30AY3pKchUDPu4x_DeqgREtXblDmTQf6lsdjpYOLvm3Gws6axwJ5K3jiQBjB42OYKgk2QWZn8V1CPdLelE3FPMGRuclpOIaMZ6rQAiRhCwOnm9kl-r3JMHJ_FBjNWudJMqDOsd4-vSl6A97SUqC47y8giZVztiDyWxeFcw2sNEaoLsSMSgeEY0-rpWitmhHHKINt_EiPUKCLLeVu7).*

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
