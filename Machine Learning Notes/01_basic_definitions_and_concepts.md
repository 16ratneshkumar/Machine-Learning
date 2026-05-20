# 01. Basic Definitions And Concepts

## 1. Overview
Machine learning (ML) is an approach employed when the input/output structure of a problem is known, but a complete explicit algorithm to map inputs to outputs is absent. Instead of hand-crafting rules, ML utilizes data to infer the underlying transformation automatically.

## 2. Core Concepts
- **Definition:** Machine learning is programming computers to optimize a performance criterion using example data or past experience.
- **Algorithm Limitations:** Explicit algorithms exist for structured tasks (e.g., sorting). However, complex real-world tasks (e.g., spam filtering, facial recognition) lack direct programmatic solutions.
- **Data-Driven Inference:** In the absence of explicit knowledge, ML compensates by collecting labeled examples to learn the appropriate mapping.
- **Optimization:** Learning fundamentally involves adjusting internal model parameters using training data to approximate the true underlying process.

## 3. The Role of Machine Learning
- **Adaptive Systems:** Essential for artificial intelligence (AI) systems operating in dynamic environments where rigid rules fail.
- **Pattern Recognition:** Excels at tasks where human intuition operates effectively but cannot be formally codified (e.g., recognizing that a face is symmetric with eyes, nose, and mouth, rather than a random pixel collection).
- **Data Mining (KDD):** Applying ML to massive datasets to extract compact, high-value predictive structures. *Analogy:* Processing a massive volume of earth to extract a small amount of precious material. This helps predict hyper-specific consumer behaviors (e.g., buying spices for Glühwein in winter, clicking a specific web link, or choosing an ice cream flavor).
- **Model Purpose:** Models can be **predictive** (making predictions about the future) or **descriptive** (gaining knowledge and explaining the data process), or both.
- **Interdisciplinary Nature:** ML lies at the intersection of statistics (inference from finite samples) and computer science (efficient, scalable algorithms). Time and space complexity are often as critical as predictive accuracy.

## 4. Mathematical Abstraction

The core abstraction of an ML model can be expressed as:
$$ y = g(x | \theta) $$

**Where:**
- $x$: Observed attributes or features.
- $y$: Target output.
- $g(\cdot)$: Model family (the functional form).
- $\theta$: Model parameters adjusted during the learning process.

The learning objective is typically defined as minimizing a loss function $L$ over a dataset $D$:
$$ \theta^* = \arg\min_\theta L(\theta; D) $$

## 5. System Architecture

```text
       (Underlying Process)
                |
                v
          [Raw Data] -> (Preprocessing) -> [Features, x]
                                                 |
                                                 v
(Training Labels, y) <---- Loss L(θ) <---- [Model: y = g(x|θ)]
                                                 ^
                                                 |
                                      (Update Parameters θ)
```

---
[Index](Topic_Wise_Notes_Index.md) | [Next](02_key_elements_of_ml.md)
