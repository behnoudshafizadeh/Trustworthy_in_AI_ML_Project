# 🛡️ Trustworthy in AI — Machine Learning Security & Explainability

A hands-on collection of Jupyter notebooks exploring the core topics of **Secure and Trustworthy Machine Learning**, built on top of the [SecML](https://github.com/pralab/secml) library.

---

## 📂 Project Structure

```
Trustworthy_in_AI_ML_Project/
├── 00_SecML.ipynb               # Introduction to the SecML library
├── 01-Evasion.ipynb             # Evasion attacks & adversarial examples
├── 02-AdversarialTraining.ipynb # Defending via adversarial training
├── 03-Poisoning.ipynb           # Poisoning attacks at train time
└── 04-Explainability.ipynb      # Post-hoc model explainability methods
```

---

## 📓 Notebooks Overview

---

### `00_SecML.ipynb` — Introduction to SecML

**Goal:** Learn the core building blocks of the SecML library before tackling attacks and defenses.

- Overview of the `CArray` data structure (NumPy-compatible, 2D only)
- CArray arithmetic, dot products, norms, broadcasting
- Wrapping **scikit-learn** and **PyTorch** models inside SecML
- Training a CNN on MNIST and an SVM on a synthetic 3-class dataset

**Key Results:**

| Model | Dataset | Accuracy |
|---|---|---|
| SVM (RBF kernel) | Synthetic 2D (3 classes) | **98.8%** |
| CNN (2×Conv + 2×FC) | MNIST | **96.5%** |
| KNN | MNIST | 41.7% |

> The SVM and CNN baselines established here are used as victim models in the following attack notebooks.

---

### `01-Evasion.ipynb` — Evasion Attacks

**Goal:** Fool a trained classifier at **test time** with minimal input perturbation.

- Crafting **adversarial examples** manually via gradient ascent
- Automated **Projected Gradient Descent (PGD-L2)** attack with perturbation budget ε
- Targeted attack: digit `0` → misclassified as digit `2`

**Key Results:**

| Condition | Classifier Output |
|---|---|
| Original sample (digit `0`) | ✅ Correctly classified as `0` |
| After PGD-L2 attack | ❌ Misclassified as `2` |
| Baseline test accuracy (before attack) | **99.6%** |

> A visually imperceptible perturbation is enough to completely redirect the model's prediction.

---

### `02-AdversarialTraining.ipynb` — Adversarial Training

**Goal:** Improve model robustness by including adversarial examples during training (min-max optimization).

- Iterative adversarial training loop (10 iterations) on a 2D problem
- Evaluation of **clean accuracy** and **robust accuracy** under PGD attack
- Scaling to MNIST: comparison of a standard vs. a pre-trained robust network
- Integration with **RobustBench** for state-of-the-art robust models

**Key Results:**

| Model | Clean Accuracy | Robust Accuracy (under PGD) |
|---|---|---|
| Standard model (2D) | **100%** | 71% |
| Adversarially trained model (2D) | **100%** | 71% |
| Standard CNN (MNIST) | **100%** | Degrades quickly with ε |
| Robust CNN (MNIST, pre-trained) | **100%** | Maintains higher accuracy across ε |

> Adversarial training preserves clean accuracy while significantly slowing down the degradation curve under attack.

---

### `03-Poisoning.ipynb` — Poisoning Attacks

**Goal:** Degrade a classifier by injecting crafted samples **at training time**.

- Gradient-based poisoning of an **SVM with RBF kernel** (Biggio et al., ICML 2012)
- Security evaluation across increasing numbers of poisoned points
- Analysis of how poisoned models behave when also subjected to evasion attacks

**Key Results:**

| Poisoned Samples Injected | Test Accuracy |
|---|---|
| 0 (clean) | **94%** |
| 1 point | 93% |
| 10 points | 91% |
| 20 points | 88% |
| 75 points | 61% |
| 100 points | **5%** ⚠️ |

> With only ~13% of the training set poisoned (100 points), accuracy collapses from 94% to 5% — demonstrating the severe impact of train-time attacks.

---

### `04-Explainability.ipynb` — Model Explainability

**Goal:** Understand *why* a model makes a decision using post-hoc explanation methods.

- **Feature-based (gradient) explanations** on MNIST via `CExplainerGradient`, `CExplainerGradientInput`, `CExplainerIntegratedGradients`
- Red/blue pixel heatmaps: positive vs. negative relevance per class
- **Influence functions** to identify the most impactful training prototypes for each prediction (top-3 per class)

**Key Results:**

| Classifier | Dataset | Accuracy |
|---|---|---|
| SVM (RBF, feature attribution) | MNIST | **83.8%** |
| SVM (RBF, influence functions) | MNIST | **96.2%** |

> The three gradient methods produce distinct but complementary heatmaps — Integrated Gradients highlights more stable, class-discriminative regions than plain Gradient. Influence functions reveal which training samples are most responsible for each test prediction.

---

## ⚙️ Setup

### Option 1 — Local (Conda)

```bash
# Create and activate environment
conda create -n secml python=3.8
conda activate secml

# Install SecML
pip install secml
```

### Option 2 — Google Colab

Each notebook includes an **Open in Colab** badge at the top. Click it to run directly in your browser with no local setup.

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/<your-username>/Trustworthy_in_AI_ML_Project.git
cd Trustworthy_in_AI_ML_Project

# Activate your environment
conda activate secml

# Launch Jupyter
jupyter notebook
```

Then open the notebooks in order, starting from `00_SecML.ipynb`.

---

## 📚 References

- Biggio, B., Nelson, B., Laskov, P. — *Poisoning attacks against support vector machines*, ICML 2012. [arXiv](https://arxiv.org/abs/1206.6389)
- Xiao, H., Biggio, B., et al. — *Feature space perturbations yield more transferable adversarial examples*, ICML 2018. [arXiv](https://arxiv.org/abs/1804.07933)
- Baehrens, D., et al. — *How to explain individual classification decisions*, JMLR 2010. [PDF](http://www.jmlr.org/papers/volume11/baehrens10a/baehrens10a.pdf)
- [SecML Documentation](https://secml.readthedocs.io/en/v0.15/)

---

> 💡 Replace `<your-username>` with your actual GitHub username.
> Make sure you've created the repository on GitHub first (without a README, so there are no conflicts).

---

## 📄 License

This project is intended for educational purposes.
