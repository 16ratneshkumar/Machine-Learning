# 22. Classification Evaluation Metrics

## 1. Overview
Evaluating classification models requires moving beyond simple accuracy, especially in the presence of imbalanced datasets. Various metrics are derived from the Confusion Matrix to capture the trade-offs between different types of errors.

## 2. The Confusion Matrix
A $K \times K$ matrix summarizing the performance of a classification algorithm. For binary classification ($2 \times 2$):

| | Predicted Positive | Predicted Negative |
|---|---|---|
| **Actual Positive** | True Positive (TP) | False Negative (FN) |
| **Actual Negative** | False Positive (FP) | True Negative (TN) |

## 3. Core Metrics

**Accuracy:** The overall proportion of correct predictions.
$$ \text{Accuracy} = \frac{\text{TP} + \text{TN}}{N} = 1 - \text{Error Rate} $$
*(Warning: Misleading if the dataset is heavily imbalanced).*
$$ \text{Error Rate} = \frac{\text{FP} + \text{FN}}{N} $$

**Precision (Positive Predictive Value):** Of all the instances the model *predicted* as positive, how many were *actually* positive? (A "retrieved-relevant" view).
$$ \text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}} $$

**Recall / Sensitivity / True Positive Rate (TPR):** Of all the *actual* positive instances, how many did the model correctly *find*?
$$ \text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}} $$

**Specificity / True Negative Rate (TNR):** Of all the *actual* negative instances, how many were correctly rejected?
$$ \text{Specificity} = \frac{\text{TN}}{\text{TN} + \text{FP}} = 1 - \text{False Positive Rate (FPR)} $$

**F1-Score:** The harmonic mean of Precision and Recall, providing a single metric that balances both.
$$ F_1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} $$

## 4. Threshold Dynamics & ROC
If a classifier outputs a continuous probability, applying a threshold $\theta$ dictates the final class. Shifting $\theta$ directly trades off FP vs FN (or Precision vs Recall).

- **ROC Curve (Receiver Operating Characteristic):** A plot of True Positive Rate (TPR) versus False Positive Rate (FPR) across all possible thresholds. A better classifier pushes the curve towards the upper-left corner.
- **AUC (Area Under the Curve):** Summarizes the ROC curve into a single scalar value. An ideal, perfect classifier has an AUC of $1.0$, while a random guess yields $0.5$.
- **Diagonal rule:** The diagonal ROC corresponds to random guessing. A classifier below the diagonal can be improved by flipping its predictions.
- **Intersecting ROC curves:** If two ROC curves intersect, each can be better under different error-cost (loss) settings.
- **Precision-Recall curve:** By varying threshold $\theta$, one can also plot precision versus recall, especially useful for retrieval and class-imbalance scenarios.
- **Sensitivity-Specificity curve:** Another threshold curve is sensitivity versus specificity.
- Source caution: in multiclass confusion matrices, off-diagonal mass indicates which class pairs are being confused, and class-wise precision/recall should be inspected (not only a single aggregate score).
- For $K>2$, source guidance also evaluates $K$ one-vs-rest binary views (each class vs. all others) to compute class-wise precision/recall/specificity.

## 5. ROC Curve Conceptual Diagram

```text
  TPR
  1.0 |      .------- (Ideal)
      |    .
      |   .  (Good Model)
      |  .
      | .
  0.0 +-------------------------
     0.0         FPR          1.0
          (Random Guessing = Diagonal)
```

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](21_support_vector_machine.md) | [Next](23_clustering_approaches.md)
