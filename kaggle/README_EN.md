[🇰🇷 한국어](README.md)

# 🏋️ Kaggle Notebooks

Training notebooks for Kaggle

## 📂 Files

| File | Description | GPU | Time |
|------|-------------|:---:|:----:|
| `SFT_v6.1_curriculum.ipynb` | SFT Curriculum Learning (v6.1) | T4 x2 | ~5h |
| `SFT_v6_200k.ipynb` | SFT 200k data training | T4 x2 | ~8h |

## 🔧 Usage

### 1. Required Kaggle Settings

1. **Accelerator**: GPU T4 x2
2. **Internet**: On (for model download)
3. **Secrets**: Set `HF_TOKEN`

### 2. Add Dataset

```
Add Data → Upload → .jsonl files
```

### 3. HuggingFace Token Setup (Kaggle Secrets)

```python
from kaggle_secrets import UserSecretsClient
user_secrets = UserSecretsClient()
os.environ["HF_TOKEN"] = user_secrets.get_secret("HF_TOKEN")
```

## ⚙️ Kaggle T4 x2 Configuration

```python
# DDP (Data Parallel) setup
accelerate launch --num_processes=2 train.py

# Batch Size calculation
# per_device=1 x gradient_accumulation=16 x gpu=2 = effective 32
```

## 📌 Colab vs Kaggle

| Item | Colab T4 | Kaggle T4 x2 |
|------|----------|--------------|
| GPU | 1 | 2 |
| VRAM | 15GB | 30GB |
| Session | 12 hours | 12 hours |
| Cost | Free | Free |

## ⚠️ Notes

- Kaggle optimized for DDP
- Code may differ from Colab notebooks
