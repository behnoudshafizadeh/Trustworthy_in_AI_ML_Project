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

### `00_SecML.ipynb` — Introduction to SecML
- Overview of the `CArray` data structure (NumPy-compatible)
- Loading pre-trained models from **scikit-learn** and **PyTorch**
- Setting up a local conda environment or running on Google Colab

### `01-Evasion.ipynb` — Evasion Attacks
- Crafting **adversarial examples** to fool trained classifiers
- **Targeted** vs **untargeted** attacks
- Implementation of **Projected Gradient Descent (PGD)** attack with perturbation budget ε, step-size α, and iteration control

### `02-AdversarialTraining.ipynb` — Adversarial Training
- Defense strategy against adversarial examples
- Min-max optimization formulation for robust training
- Comparison of standard vs. adversarially trained models

### `03-Poisoning.ipynb` — Poisoning Attacks
- Injecting crafted samples **at training time** to degrade model accuracy
- Attack on **SVM with RBF kernel**
- Gradient-based poisoning following Biggio et al. (ICML 2012)

### `04-Explainability.ipynb` — Model Explainability
- **Post-hoc** explanation methods via `secml.explanation`
- Feature attribution techniques:
  - **Gradient-based** explanations
  - Other `CExplainer` subclasses
- Applied to MNIST with an SVM classifier

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

## 📄 License

This project is intended for educational purposes.
