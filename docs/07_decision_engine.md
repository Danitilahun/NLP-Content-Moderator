# Decision Engine: Aggregation Strategies & Examples

The **Decision Engine** integrates outputs from **Sentiment Analysis**, **Entity Recognition**, and **Text Classification** to determine final content moderation actions. This section outlines aggregation methods, decision examples, and best practices to ensure a reliable moderation system.

![Decision Engine](/Diagram/XLPVRzis47_NfxWPA2PlIP2rouPuIr4taPS1ZHVOtlOuqDHPOaUHXaWb4OPzzvv9MLOfota9u2Fl-FjpTye7Orbfgq96twIu4GfXaTokflFVFYN09JCcYhw5Et_2TR7L2fKr81JO7255BepG2b1bT2CwvDur9uaxWFyYWCaqoqhCc4K3I.png)  
---

## Aggregation Methods

### Method 1: **Weighted Score Fusion**
- **Description**: Assigns weights to each component (e.g., 50% text classification, 30% sentiment, 20% entity recognition). The final score is calculated and compared to a threshold.
- **Use Case**: Best when one component (e.g., text classification) is more reliable than others and should be prioritized.

### Method 2: **Rule-Based Logic**
- **Description**: Defines explicit IF-THEN rules combining outputs from multiple components.
- **Use Case**: Ideal for clear-cut policies (e.g., block if hate speech > 90% OR ethnic slur detected).

### Method 3: **Ensemble Voting**
- **Description**: Uses majority voting (e.g., if 2 out of 3 components flag content, action is triggered).
- **Use Case**: Works best when all components have similar reliability and need to agree before taking action.

### Method 4: **Machine Learning Meta-Model**
- **Description**: Trains a classifier (e.g., logistic regression) to predict final decisions using outputs from Sentiment Analysis, Entity Recognition, and Text Classification as features.
- **Use Case**: Used in complex scenarios requiring nuanced decisions (requires labeled moderation data).

---

## Examples of Decision Logic

### Example 1: **Automatic Blocking**
- **Scenario**:
  - **Text Classification**: 95% hate speech
  - **Sentiment Analysis**: 0.9 (highly negative)
  - **Entity Recognition**: Detects an ethnic slur
- **Aggregation**:
  - **Rule**: IF (hate_speech_score > 90% OR entity = "ethnic_slur") THEN **BLOCK**
- **Result**:
  - Content is automatically removed.

### Example 2: **Escalate to Human Moderators**
- **Scenario**:
  - **Text Classification**: 65% cyberbullying
  - **Sentiment Analysis**: 0.7 (moderately negative)
  - **Entity Recognition**: No sensitive entities detected
- **Aggregation**:
  - **Weighted Score Calculation**:  
    (0.65 * 0.5) + (0.7 * 0.3) + (0 * 0.2) = 0.565  
    (Threshold = 0.6)
- **Result**:
  - Since the score is below the threshold (0.565 < 0.6), the case is escalated for human review.

### Example 3: **Allow but Monitor User**
- **Scenario**:
  - **Text Classification**: 30% explicit content
  - **Sentiment Analysis**: 0.4 (neutral)
  - **Entity Recognition**: Detects a public figure name ("Abiy Ahmed")
- **Aggregation**:
  - **Rule**: IF (explicit_score < 50% AND sentiment < 0.5) THEN **ALLOW** but log user ID for behavioral tracking.
- **Result**:
  - Content is allowed, but the user is added to a watchlist for future monitoring.

---

## Best Aggregation Practices

### 1. **Prioritize Text Classification**
- Assign the highest weight (e.g., 50-70%) to **text classification**, as it maps directly to moderation categories like hate speech and cyberbullying.

### 2. **Use Hybrid Approaches**
- Combine **rule-based logic** for explicit violations (e.g., ethnic slurs) with **weighted scoring** for ambiguous cases. This helps ensure robust decision-making while maintaining flexibility.

### 3. **Implement Dynamic Thresholds**
- Adjust thresholds based on platform risk tolerance:
  - **Strict Mode**:  
    - **Condition**: Hate Speech > 70%  
    - **Action**: Block Content
  - **Lenient Mode**:  
    - **Condition**: Hate Speech > 90% AND Sentiment > 0.8  
    - **Action**: Block Content

### 4. **Fallback to Human Review**
- **Escalate cases** when:
  - Confidence scores fall into borderline ranges (e.g., 60-80%).
  - There are **conflicting signals** (e.g., high negative sentiment but low classification score).

---

## Evaluation & Selection of Aggregation Methods

We will experiment with all of the aggregation methods outlined above and assess their performance in our context. Based on our tests, we will select the method(s) that work best for our needs. For example, **weighted score fusion** may be effective when one component (like text classification) is more reliable, while **ensemble voting** could be better suited when all components contribute equally. **Rule-based logic** will also be used for explicit violations, ensuring clarity and compliance with platform policies.

Our goal is to find the optimal combination of aggregation strategies to ensure that the moderation system is both accurate and efficient, while minimizing errors and ensuring fair decision-making.