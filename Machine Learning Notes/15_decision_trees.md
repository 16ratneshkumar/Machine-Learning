# 15. Decision Trees

## 1. Overview
Decision trees are non-parametric models that learn discrete-valued (or continuous) functions by applying recursive attribute tests. They are highly interpretable and logically represent a disjunction of conjunctions (an OR of AND rules).

## 2. Tree Architecture
- **Internal Node:** Represents a logical test on a specific attribute.
- **Branch:** Represents the outcome of the attribute test.
- **Leaf (Terminal Node):** Represents the final class prediction or continuous value.

## 3. Learning Algorithm (Top-Down Greedy Search)
A family of algorithms including **ID3**, **ASSISTANT**, and **C4.5** build trees recursively from the top down:
1. At each node, evaluate all available attributes using a statistical test (e.g., Information Gain).
2. Select the attribute that yields the highest Information Gain to serve as the root of the current subtree.
3. Split the training data into subsets based on the selected attribute's outcomes.
4. Recurse on the resulting subsets until the nodes are pure (contain only one class), or all attributes are exhausted.
- **Inductive Bias:** These algorithms search a completely expressive hypothesis space but exhibit an inductive bias (Occam's razor) preferring smaller/shorter trees over larger ones.

**ID3-style stopping rules (from source):**
1. If all examples at a node belong to the same class, return that class (leaf).
2. If there are no remaining attributes to split, return the majority class at that node.
3. Otherwise, choose the best splitting attribute and recurse.

## 4. Mathematical Formulation

### Binary Entropy
Entropy $H(S)$ measures the impurity or uncertainty of a dataset $S$. For a binary classification problem:
$$ H(S) = -p_+ \log_2(p_+) - p_- \log_2(p_-) $$
*(Where $p_+$ is the proportion of positive examples, and $p_-$ is the proportion of negative examples. In all calculations, $0 \log 0$ is explicitly defined to be $0$. For a $c$-class problem, maximum entropy is $\log_2 c$).*

### Information Gain
The expected reduction in entropy caused by partitioning the examples according to attribute $A$. It represents the number of bits saved when encoding the target value of an arbitrary member of $S$, given the value of $A$:
$$ \text{Gain}(S, A) = H(S) - \sum_{v \in \text{Values}(A)} \frac{|S_v|}{|S|} H(S_v) $$
*(Where $S_v$ is the subset of $S$ for which attribute $A$ has value $v$).*

## 5. Advantages & Extensions
- **Appropriate Problems:** Best suited when instances are represented by attribute-value pairs, target functions have discrete outputs, and disjunctive descriptions are required.
- **Robustness:** Highly robust to noisy data (errors in classification or attribute values) and capable of handling missing attribute values seamlessly.
- **Interpretability:** Trees can be easily visualized and understood as explicit rules.
- **Flexibility:** Naturally supports disjunctive concepts and can be extended to regression tasks (Regression Trees).
- **Overfitting control:** Greedy tree growth can overfit; post-pruning/rule-pruning is used to simplify trees and improve generalization.

## 6. Tree Structure Example (PlayTennis)
*Example: Classifying Saturday mornings on whether they are suitable for playing tennis.*
```text
                 [Outlook?]
                /    |     \
          (Sunny) (Overcast) (Rain)
            /        |          \
      [Humidity?]  [YES]      [Wind?]
      /      \                /     \
  (High)   (Normal)      (Strong) (Weak)
   /          \            /         \
 [NO]        [YES]       [NO]       [YES]
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Rule Extraction:** When interpretability is paramount, as the model generates explicit IF-THEN rules understandable by non-technical stakeholders.
2. **Mixed Data Types:** Excellent for datasets containing a mix of numerical, categorical, and ordinal features without requiring extensive preprocessing or one-hot encoding.
3. **Missing Value Tolerance:** Useful when data is incomplete, as trees can natively handle missing values through surrogate splits.
4. **Medical Diagnosis:** For building clinical decision support systems where the diagnostic pathway must be logically verifiable by doctors.
5. **Customer Segmentation:** To visually split a customer base into distinct cohorts based on purchasing behavior and demographics.

**5 Limitations (When NOT to use):**
1. **High Overfitting Risk:** Very prone to overfitting the training data (memorizing noise) if allowed to grow deeply without proper pruning.
2. **Instability (High Variance):** Small variations in the training data can result in a completely different tree structure being generated.
3. **Smooth Boundaries:** Poor at modeling smooth continuous boundaries; it creates axis-aligned, jagged step-functions.
4. **Class Imbalance Sensitivity:** Tends to become biased toward the majority class if the dataset is heavily imbalanced.
5. **Extrapolation in Regression:** Cannot extrapolate beyond the range of the training data when used as Regression Trees.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](14_regression_evaluation_metrics.md) | [Next](16_naive_bayes_classifier.md)
