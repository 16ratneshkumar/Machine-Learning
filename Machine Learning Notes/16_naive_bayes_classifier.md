# 16. Naive Bayes Classifier

## 1. Overview
The Naive Bayes Classifier is a highly practical probabilistic classifier grounded in Bayes' Theorem. It relies on the "naive" assumption of conditional independence between every pair of features given the class label. Despite its simplicity, it is highly competitive with (and sometimes outperforms) decision trees and neural networks, particularly in domains like text classification.

## 2. Bayes' Theorem Foundations
Bayes' Theorem calculates the posterior probability of a hypothesis $h$ given observed data $D$. It gracefully accommodates probabilistic predictions (e.g., "this pneumonia patient has a 93% chance of complete recovery"):
$$ P(h|D) = \frac{P(D|h)P(h)}{P(D)} $$

The **Maximum A Posteriori (MAP)** hypothesis selects the hypothesis that maximizes this probability (ignoring the constant denominator $P(D)$):
$$ h_{\text{MAP}} = \arg\max_h P(D|h)P(h) $$
*Cancer Diagnosis Example:* Given cancer prevalence $P(C) = 0.008$, lab test TP = 98%, and TN = 97%. Even if the test returns positive ($+$), $h_{\text{MAP}}$ is still $\neg C$ because the prior for no-cancer heavily outweighs the false positive rate ($0.992 \times 0.03 > 0.008 \times 0.98$).

### Bayes Optimal Classifier
Instead of just applying the MAP hypothesis, the **Bayes Optimal Classifier** finds the most probable classification for a *new* instance by combining the predictions of *all* hypotheses, weighted by their posterior probabilities. No other method using the same hypothesis space can outperform this on average.
$$ P(v_j \mid D) = \sum_i P(v_j \mid h_i)\,P(h_i \mid D) $$
The resulting effective decision rule can correspond to a predictor that is *not* explicitly one of the hypotheses in $H$.

The source also highlights the practical approximation called **Gibbs classifier**: sample one hypothesis $h$ from the posterior $P(h \mid D)$ and classify using that single sampled hypothesis.

## 3. The Naive Assumption
For a given class $v_j$ and an input vector of attributes $a_1, a_2, \dots, a_n$, the true conditional probability $P(a_1, \dots, a_n | v_j)$ is extremely difficult to compute. 

Naive Bayes drastically simplifies this by assuming feature independence:
$$ P(a_1, \dots, a_n | v_j) \approx \prod_{i=1}^{n} P(a_i | v_j) $$

## 4. Classification Rule
The final Naive Bayes prediction rule selects the class $v_j$ that maximizes the product of the prior and the conditional probabilities:
$$ v_{\text{NB}} = \arg\max_{v_j} P(v_j) \prod_{i=1}^{n} P(a_i | v_j) $$

## 5. Practical Considerations & Smoothing
- **Estimation & Search:** Priors $P(v_j)$ and conditionals $P(a_i|v_j)$ are estimated directly from training frequencies. Unlike other algorithms, Naive Bayes does not perform an explicit search through a hypothesis space; it simply counts frequencies.
- **The Zero-Frequency Problem:** If a specific feature value never occurs with a specific class in the training data, its conditional probability is $0$. Because Naive Bayes multiplies probabilities, a single zero wipes out the entire score.
- **m-estimate Smoothing (Laplace Smoothing):**
  Adjusts probability estimates to prevent zero-counts:
  $$ P(a_i|v_j) = \frac{n_c + m p}{n + m} $$
  *(Where $n$ is total examples of class $v_j$, $n_c$ is examples with $a_i$, $p$ is the prior estimate, and $m$ is the equivalent sample size. Typically, $p$ is assumed to be uniform, i.e., $p = 1/k$ where $k$ is the number of possible values. The constant $m$ represents adding $m$ "virtual" samples).*

## 6. Probabilistic Flow

```text
    [Input: a_1, a_2, ..., a_n]
                |
                v
  (Compute P(v) for each class)  <--- Prior
                |
  (Compute Π P(a_i | v))         <--- Likelihood
                |
                v
  [ Score(v) = P(v) * Likelihood ]
                |
                v
    [ Output: argmax Score(v) ]
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Text Classification:** Industry standard for document categorization, spam filtering, and sentiment analysis due to its high performance with word frequencies.
2. **Real-time Prediction:** Exceptionally fast at both training and predicting, making it suitable for real-time applications and streaming data.
3. **Multi-class Classification:** Naturally handles multi-class problems (e.g., categorizing news articles into Sports, Politics, Technology) efficiently.
4. **Small Training Data:** Works surprisingly well even when the training dataset is relatively small, as it only needs to estimate feature probabilities rather than search a complex hypothesis space.
5. **Recommendation Systems:** Often used in collaborative filtering to build fast, probabilistic recommendation engines.

**5 Limitations (When NOT to use):**
1. **The "Naive" Assumption:** Assumes all features are strictly independent. If features are highly correlated, the calculated probabilities become extremely skewed and unreliable.
2. **Zero-Frequency Problem:** If a category-feature combination was unseen during training, it assigns a zero probability, wiping out the entire prediction (unless smoothed).
3. **Bad Estimator:** While it is a good classifier (ranking the correct class highest), the actual probability outputs (the MAP scores) are notoriously poorly calibrated and shouldn't be taken literally.
4. **Continuous Variable Handling:** Native implementations assume categorical data. To handle continuous variables, one must either discretize them or assume a specific distribution (like Gaussian), which might not fit the real data.
5. **Complex Interactions:** Incapable of learning complex, non-linear feature interactions (unlike Decision Trees or Neural Networks).

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](15_decision_trees.md) | [Next](17_logistic_regression.md)
