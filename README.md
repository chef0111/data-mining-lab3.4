# UIT — Data Mining Practical Lab 3 & 4

Classification and neural-network labs (Decision Trees, Naive Bayes, ensemble models, MLP/CNN).

## Prerequisites

- Python 3.10+ (3.11 recommended)
- Git clone of this repository

Place lab assets under `docs/` (not tracked in git):


| File                                           | Used by            |
| ---------------------------------------------- | ------------------ |
| `docs/heart.csv`                               | Lab 3 — Exercise 3 |
| `docs/winequality-red.csv`                     | Lab 3 — Exercise 2 |
| `docs/Lab3 - CTTT.pdf`, `docs/Lab4 - CTTT.pdf` | Reference only     |


## Setup

From the repository root (`data-mining-lab3.4`):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

On macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Lab 4 deep-learning cells need **PyTorch** and **torchvision** (included in `requirements.txt`). A GPU is optional; CPU training works but is slower for CIFAR-10 / VGG16.

## How to run

Always start Jupyter (or run cells) with the **working directory set to the repo root**, so paths like `docs/heart.csv` and `data/` resolve correctly.

### Option A — Jupyter Notebook (recommended)

```powershell
python -m jupyter notebook
```

Open:

- **Lab 3:** [lab3.ipynb](lab3.ipynb)
- **Lab 4:** [lab4-1.ipynb](lab4-1.ipynb)

Use **Run → Run All Cells** (or run section by section).

### Option B — VS Code

Open the notebook, select the project Python interpreter (your venv), and **Run All**. Confirm the notebook kernel cwd is the repo root (default when the folder is opened as the workspace).

### Option C — Execute without the UI

```powershell
python -m jupyter nbconvert --to notebook --execute lab3.ipynb --output lab3.ipynb
python -m jupyter nbconvert --to notebook --execute lab4-1.ipynb --output lab4-1.ipynb
```

---

## Lab 3 — [lab3.ipynb](lab3.ipynb)

Exercises: toy ID3/CART/Naive Bayes, wine quality, heart disease.


| Exercise | Dataset                    | Notes                                     |
| -------- | -------------------------- | ----------------------------------------- |
| 1        | Embedded in notebook       | Manual decision trees + Naive Bayes       |
| 2        | `docs/winequality-red.csv` | Binary label: quality ≥ 6 → Good          |
| 3        | `docs/heart.csv`           | Preprocessing + same models as Exercise 2 |


**Expected runtime:** A few minutes on CPU after dependencies are installed.

**If a CSV is missing:** copy `heart.csv` and `winequality-red.csv` into `docs/` from your course materials.

---

## Lab 4 — [lab4-1.ipynb](lab4-1.ipynb)

Exercises: gradient descent, MNIST (MLP vs CNN), CIFAR-10 (Basic CNN, VGG16, ResNet18).


| Exercise | Data       | Notes                               |
| -------- | ---------- | ----------------------------------- |
| 1        | NumPy only | Scalar GD + linear regression plots |
| 2        | MNIST      | Downloaded to `data/` on first run  |
| 3        | CIFAR-10   | Downloaded to `data/` on first run  |


**First run:** MNIST and CIFAR-10 are fetched into `data/` (gitignored). Full training on CPU can take **1–2 hours** (VGG16 is the slowest part).

**Later runs:** The notebook loads training histories from `data/lab4_train_cache.pkl` and `data/lab4_cifar_cache.pkl` if they exist, so **Run All** finishes in about a minute. To retrain from scratch, delete those `.pkl` files (and optionally the `data/MNIST` / `data/cifar-10-batches-py` folders).

**Tips:**

- For faster Lab 4 training, use a CUDA-enabled PyTorch build and a GPU.
- VGG16 on CPU uses fewer epochs by design; accuracy will be lower than on GPU/Kaggle.

---

## Troubleshooting


| Issue                                     | Fix                                                               |
| ----------------------------------------- | ----------------------------------------------------------------- |
| `FileNotFoundError` for `docs/*.csv`      | Add CSV files under `docs/`                                       |
| `ModuleNotFoundError` (torch, xgboost, …) | `pip install -r requirements.txt` in your active venv             |
| Notebook paths fail                       | Run from repo root, not from inside `docs/`                       |
| Lab 4 cell hangs on training              | Wait for first full train, or use existing cache files in `data/` |
| Out of memory (VGG / large batch)         | Lower batch size in the CIFAR cells or use GPU                    |


