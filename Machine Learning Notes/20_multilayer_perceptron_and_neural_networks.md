# 20. Multilayer Perceptron And Neural Networks

## 1. Overview
A Multilayer Perceptron (MLP) is a fully connected class of feedforward artificial neural network (ANN). By stacking multiple layers of neurons and incorporating non-linear activation functions, MLPs overcome the limitations of the single-layer perceptron, enabling the modeling of highly complex, non-linear relationships.
- **Deep Learning History:** Neural networks rose to fame in the late 1980s (catalyzing the Annual NeurIPS meetings at exotic ski resorts), stabilized in the 1990s, fell somewhat from favor in the 2000s due to the rise of less tinker-heavy models like SVMs and Random Forests, and resurfaced post-2010 under the name "Deep Learning" driven by massive datasets and modern GPU architectures.
- **Biological Analogy:** Originally inspired by neurons in the brain, where activation values close to 1 represent "firing" and those close to 0 represent "silent" nodes.
- **Deep Learning Jargon:** In the deep learning community, intercepts are referred to as **biases** and coefficients are referred to as **weights**.

## 2. Network Architecture
An MLP consists of at least three layers of nodes: an input layer, one or more hidden layers, and an output layer.

**Hidden Activation Formula ($A_k$):**
Each node $k$ in the hidden layer computes:
$$ A_k = g\left( w_{k0} + \sum_{j} w_{kj} X_j \right) $$

**Single-Hidden-Layer Output Formulation:**
The final prediction maps the hidden activations to the output:
$$ f(X) = \beta_0 + \sum_{k} \beta_k \cdot g\left( w_{k0} + \sum_{j} w_{kj} X_j \right) $$

*Interaction Proof Example:* The sum of two nonlinear transformations of linear functions can naturally construct interactions. Given $p = 2$ inputs, $K = 2$ hidden units with activation $g(z) = z^2$, and parameters:
$$ \beta_0 = 0, \beta_1 = \frac{1}{4}, \beta_2 = -\frac{1}{4} $$
$$ w_{10} = 0, w_{11} = 1, w_{12} = 1; \quad w_{20} = 0, w_{21} = 1, w_{22} = -1 $$
This constructs $h_1(X) = (X_1 + X_2)^2$ and $h_2(X) = (X_1 - X_2)^2$, yielding:
$$ f(X) = \frac{1}{4}(X_1 + X_2)^2 - \frac{1}{4}(X_1 - X_2)^2 = X_1 X_2 \quad (\text{a pure interaction!}) $$

## 3. The Necessity of Non-Linearity & Activation Functions
The function $g(\cdot)$ represents a non-linear activation function. Without non-linear activation functions, cascading multiple layers mathematically collapses into a single linear transformation, rendering the deep architecture useless.
- **Sigmoid:** $g(z) = \frac{1}{1 + e^{-z}}$. Used in early ANNs, converting linear functions to $0-1$ probability ranges.
- **ReLU (Rectified Linear Unit):** $g(z) = (z)^+ = \max(0, z)$. Piecewise-linear modern standard. Highly preferred in modern networks because it can be computed and stored much more efficiently than sigmoids.
- **Softmax:** Used at the output layer for multiclass tasks to represent class probabilities.

## 4. Deep Architecture Advantages & Task Settings
- Multiple hidden layers allow the network to model hierarchical, complex non-linear interactions (discovering representations where layer L2 treats L1 outputs as features).
- Deep architectures often facilitate much more efficient representation learning compared to expanding a single shallow layer to a massive width.
- **Image & Digit Classification (e.g., MNIST):** Pixels (e.g., $28 \times 28 = 784$ features) map to a one-hot encoded vector representing digit classes 0–9. Historically, digit recognition at AT&T Bell Laboratories in the late 1980s was the catalyst that accelerated neural network research.
- **Multi-task Learning:** Predicting different qualitative or quantitative responses simultaneously with a single network, where all tasks share and influence the formation of the hidden layers.

## 5. Training Mechanics
- **Backpropagation:** An algorithm that applies the chain rule of calculus to efficiently compute the gradients of the loss function with respect to every weight in the network.
- **Optimization:** Gradients are utilized by algorithms like Stochastic Gradient Descent (SGD) or Adam to minimize the loss (e.g., Squared Error or Cross-Entropy).
- **Generalization:** Heavy reliance on regularization (L2, Dropout) and careful tuning of SGD parameters (learning rate, early stopping) is required to prevent extreme overfitting.

## 6. Feedforward Structure

```text
  [Input Layer]      [Hidden Layer(s)]       [Output Layer]
      (X_1) -------------- (A_1) 
               \  /       /      \
      (X_2) ---- X ---- (A_2) ---- (Sum & Activate) ---> Output f(X)
               /  \       \      /
      (X_3) -------------- (A_3)
```

## Use Cases & Limitations

**5 Use Cases (When to use):**
1. **Complex Non-Linear Representation:** Unmatched at discovering complex, non-linear relationships and interactions without requiring manual feature engineering.
2. **Image and Audio Tasks:** The foundational architecture that scales into Convolutional (CNN) and Recurrent (RNN) networks for computer vision and speech recognition.
3. **Multi-Task Learning:** Capable of predicting multiple different outputs simultaneously within a single model architecture, sharing learned hidden representations.
4. **Massive Datasets:** Performance scales incredibly well with data; unlike older algorithms that plateau, deep networks keep improving with millions of examples.
5. **Natural Language Processing:** The core mechanism driving modern text embeddings and transformer architectures used in LLMs.

**5 Limitations (When NOT to use):**
1. **The "Black Box" Problem:** Highly uninterpretable. It is extremely difficult to explain *why* the network made a specific prediction, which is unacceptable in heavily regulated industries like finance or medicine.
2. **Data Hungry:** Performs very poorly on small datasets where simpler models like Random Forests or Naive Bayes would excel.
3. **High Computational Cost:** Training requires significant hardware resources (GPUs/TPUs) and time, making it expensive to deploy and iterate.
4. **Hyperparameter Sensitivity:** Requires extensive tuning of learning rates, layer sizes, activation functions, and regularization techniques to prevent severe overfitting.
5. **Lack of Uncertainty Calibration:** Can confidently output wildly incorrect predictions for data outside its training distribution.

---
[Index](Topic_Wise_Notes_Index.md) | [Prev](19_perceptron.md) | [Next](21_support_vector_machine.md)
