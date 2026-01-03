[🇰🇷 한국어](README.md)

# 🇰🇷 LFM2-KoEn-Tuning

**LiquidAI LFM2-1.2B Korean-English Bidirectional Translation Model Fine-tuning**

[![Hugging Face](https://img.shields.io/badge/🤗%20Models-Hugging%20Face-yellow)](https://huggingface.co/gyung)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

> ⚠️ **Note**: This repo contains code generated using Claude Opus 4.5 in Antigravity, based on previously trained code. The notebooks have not yet been validated by running in Colab and Kaggle. Additional updates including links to executed notebooks will be added after testing.

---

## 🏆 Key Achievements

> **1.2B model outperforms 4B models!** **1.78 CHrF++** higher than Gemma-3 (4B)  
> Achieved SOTA in just **400 Steps (0.78 Epoch)**

---

## 📊 Benchmark (Flores-200, 1012 Samples)

### Model Comparison (Sorted by CHrF++)

| Rank | Model | CHrF++ | BLEU | Params | Note |
|:----:|-------|:------:|:----:|:------:|------|
| 1 | Google Translate | 39.27 | 18.18 | - | Commercial (Target) |
| 2 | Yanolja-4B-GGUF | 38.61 | 16.03 | 4B | Open Source SOTA |
| 3 | NLLB-200 (3.3B) | 35.09 | 11.68 | 3.3B | Translation-only |
| **4** | **🏆 LFM2-v8-rl-10k-adapter** | **34.61** | **13.21** | **1.2B** | **This Project SOTA** |
| 5 | LFM2-v6.4-merged | 33.53 | 12.31 | 1.2B | SFT Base |
| 6 | Gemma-3-4B-it-GGUF | 32.83 | 11.36 | 4B | Google Latest 4B |
| 7 | LFM2-v6.1-curriculum | 32.48 | 11.89 | 1.2B | SFT Curriculum |
| 8 | NLLB-200-Distilled-600M | 31.97 | 10.32 | 600M | Lightweight |
| 9 | LFM2-v4-100k | 31.53 | 11.13 | 1.2B | Initial SFT |
| 10 | LFM2-1.2B (Base) | 27.23 | 6.43 | 1.2B | Baseline |

### GGUF Quantization Performance (v8 merged)

| Quantization | CHrF++ | BLEU | Size | Note |
|--------------|:------:|:----:|:----:|------|
| fp32 (Original) | 34.32 | 13.10 | 4.68G | Repetition bug |
| **Q8_0** 🏆 | **34.39** | 12.93 | 1.25G | Best quality+stability |
| Q5_K_M | 34.08 | 12.78 | 843M | Balanced |
| Q4_K_M | 33.97 | 12.56 | 731M | Lightweight/Mobile |

> **Conclusion**: 4/5/8-bit quantization maintains virtually identical performance to fp32!

---

## 📈 Training Progress

| Step | Epoch | CHrF++ | BLEU | Note |
|:----:|:-----:|:------:|:----:|------|
| 0 | 0.00 | 33.53 | 12.63 | v6.4 Base |
| 200 | 0.39 | 34.10 | 12.93 | +0.57 |
| 300 | 0.59 | 34.19 | 13.24 | Historic High |
| **400** | **0.78** | **34.61** | **13.21** | **🏆 SOTA** |

---

## ✨ v8 Model Strengths

- **Honorific Consistency**: Formal Korean endings applied consistently across all 1012 samples
- **Natural Sentences**: Handles complex sentences naturally
- **Context Awareness**: Flexibly translates "While" to "반면", "동안" based on context
- **Technical Terms**: Accurately translates "rachis" to "우축"

### ⚠️ Known Limitations

- **Proper Noun Hallucination**: "George W. Bush" → "조지 워싱턴" (base model bias)
- **Solution**: Hallucination correction via SFT + DPO planned (v9)

---

## 📂 Project Structure

```
├── colab/              # Colab notebooks
│   ├── GRPO_v8_adapter_github.ipynb      # RL GRPO (SOTA)
│   ├── GRPO_v8_unsloth_vllm_github.ipynb # RL Unsloth+vLLM
│   └── SFT_colab_github.ipynb            # SFT Colab style ⭐
├── kaggle/             # Kaggle notebooks
│   ├── SFT_v6.1_curriculum.ipynb     # SFT v6.1
│   └── SFT_v6_200k.ipynb             # SFT v6 200k
├── evaluation/
│   └── benchmark_flores200.ipynb     # Benchmark
├── quantization/
│   └── convert_to_gguf_github.ipynb  # GGUF conversion
└── dataset/
    ├── samples/                      # Training data samples
    └── upload_to_hf_github.py        # HF upload script
```

---

## 🚀 Quick Start

### Using SOTA Model (v8 Adapter)

```python
from transformers import AutoModelForCausalLM, AutoTokenizer
from peft import PeftModel

# Load base model
base_model = AutoModelForCausalLM.from_pretrained(
    "gyung/lfm2-1.2b-koen-mt-v6.4-merged",
    device_map="auto",
    torch_dtype="auto"
)
tokenizer = AutoTokenizer.from_pretrained("gyung/lfm2-1.2b-koen-mt-v6.4-merged")

# Load and merge adapter
model = PeftModel.from_pretrained(base_model, "gyung/lfm2-1.2b-koen-mt-v8-rl-10k-adapter")
model = model.merge_and_unload()

# Translate
messages = [
    {"role": "system", "content": "Translate to Korean."},
    {"role": "user", "content": "Hello, world!"}
]
inputs = tokenizer.apply_chat_template(messages, return_tensors="pt")
outputs = model.generate(inputs, max_new_tokens=256, temperature=0.3)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

### Using GGUF (llama.cpp)

```python
from llama_cpp import Llama
from huggingface_hub import hf_hub_download

model_path = hf_hub_download(
    "gyung/lfm2-1.2b-koen-mt-v8-rl-10k-merged-GGUF",
    "lfm2-1.2b-koen-mt-v8-rl-10k-merged-Q8_0.gguf"
)

llm = Llama(model_path=model_path, n_ctx=4096, n_gpu_layers=-1)

prompt = """<|im_start|>system
Translate to Korean.<|im_end|>
<|im_start|>user
Hello, world!<|im_end|>
<|im_start|>assistant
"""
output = llm(prompt, max_tokens=256, stop=["<|im_end|>"], temperature=0.3)
print(output['choices'][0]['text'])
```

---

## 📊 Dataset

Training data samples in `dataset/samples/`:

| File | Purpose | Count |
|------|---------|-------|
| `sample_sft_100_bidirectional.jsonl` | SFT | 100 |
| `sample_grpo_100_bidirectional.jsonl` | GRPO | 100 |

### HuggingFace Upload

```bash
# Set HF=your_token in .env file
cd dataset
python upload_to_hf_github.py --repo YOUR_ID/your-dataset-name
```

---

## ⚙️ Training Configuration

### GRPO (v8 SOTA)

| Item | Value |
|------|-------|
| Base Model | gyung/lfm2-1.2b-koen-mt-v6.4-merged |
| Method | GRPO (Group Relative Policy Optimization) |
| Reward | COMET + CHrF++ |
| Dataset | 10,000 samples (bidirectional) |
| Steps | 400 |
| LoRA Rank/Alpha | 32 / 64 |

### SFT (v6.4 Base)

```python
SFTConfig(
    per_device_train_batch_size=1,
    gradient_accumulation_steps=16,
    learning_rate=1e-5,
    lr_scheduler_type="cosine",
    warmup_ratio=0.1,
    optim="paged_adamw_8bit",
    fp16=True,  # T4 optimization
)
```

---

## 🔗 Model Links

| Model | Description | Link |
|-------|-------------|------|
| **v8 Adapter** 🏆 | SOTA (CHrF++ 34.61) | [HuggingFace](https://huggingface.co/gyung/lfm2-1.2b-koen-mt-v8-rl-10k-adapter) |
| v8 GGUF | Quantized | [HuggingFace](https://huggingface.co/gyung/lfm2-1.2b-koen-mt-v8-rl-10k-merged-GGUF) |
| v6.4 Merged | Base | [HuggingFace](https://huggingface.co/gyung/lfm2-1.2b-koen-mt-v6.4-merged) |
| v4 100k | Initial SFT | [HuggingFace](https://huggingface.co/gyung/lfm2-1.2b-koen-mt-v4-100k) |
| LFM2-1.2B | Original Base | [LiquidAI](https://huggingface.co/LiquidAI/LFM2-1.2B) |

---

## 📝 Citation

```bibtex
@misc{lfm2-koen-v8-rl,
  author = {gyung},
  title = {LFM2-1.2B-KoEn-MT: GRPO-Enhanced Korean-English Translation},
  year = {2025},
  publisher = {Hugging Face},
  url = {https://huggingface.co/gyung/lfm2-1.2b-koen-mt-v8-rl-10k-adapter}
}
```

---

## 📜 License

This model follows **Liquid AI LFM Open License v1.0**.

- ✅ Academic research and personal use: Unlimited
- ✅ Commercial use: Free under $10M annual revenue
- ⚠️ Over $10M annual revenue: Separate license required

---

*Last Updated: 2026-01-03*
