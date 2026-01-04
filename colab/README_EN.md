[🇰🇷 한국어](README.md)

# 🚀 Colab Notebooks

Training notebooks for Google Colab

## 📂 Files

| File | Description | GPU | Colab |
|------|-------------|:---:|:----:|
| `GRPO_v8_adapter_github.ipynb` | **GRPO RL** (SOTA) | T4 | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1hqPC9yEI9uyD8DjqRtBKt49sMeIcqsQh#scrollTo=KRiTAlPQOFbK) |
| `GRPO_v8_unsloth_vllm_github.ipynb` | GRPO + Unsloth/vLLM optimized | T4/L4 | |
| `SFT_colab_github.ipynb` | **SFT Curriculum** (Colab style) | T4 |  |

## ⚠️ GitHub Version Notes

`*_github.ipynb` files have **the same functionality** as originals:
- HF token changed to `login()` format (manual input)
- Outputs removed
- Comments cleaned up
- `OUTPUT_MODEL_ID` set to `YOUR_ID/your-output-model` (needs change)

## ⚙️ Requirements

- **T4 GPU**: Available in free Colab
- **L4/A100 GPU**: Colab Pro recommended

## 📌 Recommended Settings (T4)

```python
TrainingArguments(
    fp16=True,          # BF16 not supported
    gradient_checkpointing=True,
    per_device_train_batch_size=4,
)
```

## ⚠️ Notes

- `*_github.ipynb`: Token replaced with `YOUR_HF_TOKEN` (public)
- Original files are in `.gitignore` and not uploaded
