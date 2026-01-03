[🇰🇷 한국어](README.md)

# 🔧 Quantization

GGUF quantization conversion notebooks

## 📂 Files

| File | Description |
|------|-------------|
| `convert_to_gguf_github.ipynb` | GGUF conversion (GitHub, token removed) |
| `convert_to_gguf.ipynb` | Original (with token, reference only) |

## 🎯 Supported Quantizations

| Quantization | Size | Quality | Use Case |
|--------------|:----:|:-------:|----------|
| **Q8_0** 🏆 | 1.25G | Best | Quality priority |
| **Q5_K_M** | 843M | Great | Balanced |
| **Q4_K_M** | 731M | Good | Lightweight/Mobile |

## 🚀 Usage

### 1. Run in Colab
```
GitHub → convert_to_gguf_github.ipynb → Open in Colab
```

### 2. Configure Model
```python
MODEL_ID = "gyung/lfm2-1.2b-koen-mt-v8-rl-10k-merged"
OUTPUT_REPO = "gyung/lfm2-1.2b-koen-mt-v8-rl-10k-merged-GGUF"
```

### 3. Conversion Process
1. Build llama.cpp
2. Download HuggingFace model
3. Convert to FP16 GGUF
4. Quantize to Q4/Q5/Q8
5. Upload to HuggingFace

## 📊 Performance Comparison

| Quantization | CHrF++ | BLEU | vs fp32 |
|--------------|:------:|:----:|:-------:|
| fp32 | 34.32 | 13.10 | - |
| Q8_0 | 34.39 | 12.93 | +0.07 |
| Q5_K_M | 34.08 | 12.78 | -0.24 |
| Q4_K_M | 33.97 | 12.56 | -0.35 |

> **Conclusion**: Quantization has minimal impact on quality!

## ⚙️ Requirements

- Colab CPU instance (GPU not required)
- High-RAM recommended (for large models)
- Conversion time: ~30min

## ⚠️ Notes

- `convert_to_gguf_github.ipynb`: Token replaced with `login()` format
- `convert_to_gguf.ipynb`: Original (in `.gitignore`, not uploaded)
- Change `OUTPUT_REPO` to your HuggingFace ID before running
