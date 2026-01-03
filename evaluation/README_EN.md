[🇰🇷 한국어](README.md)

# 📊 Evaluation

Benchmark notebooks for model evaluation

## 📂 Files

| File | Description |
|------|-------------|
| `benchmark_flores200.ipynb` | Flores-200 Benchmark (1012 samples) |

## 🎯 Metrics

| Metric | Description |
|--------|-------------|
| **CHrF++** | Character n-gram F-score (primary) |
| **BLEU** | Bilingual Evaluation Understudy |

## 🚀 Usage

### 1. Run in Colab
```
GitHub → benchmark_flores200.ipynb → Open in Colab
```

### 2. Configure Models to Test
```python
MODELS_TO_TEST = [
    {
        "name": "LFM2-v8-RL",
        "id": "gyung/lfm2-1.2b-koen-mt-v6.4-merged",
        "adapter_id": "gyung/LFM2-v8-rl-10k-adapter",
        "type": "peft_adapter"
    },
    {
        "name": "LFM2-v6.4",
        "id": "gyung/lfm2-1.2b-koen-mt-v6.4-merged",
        "type": "transformers"
    }
]
```

### 3. View Results
- CSV file auto-downloads
- Compare sentence-by-sentence translations

## 📈 Benchmark Results Example

| Model | CHrF++ | BLEU |
|-------|:------:|:----:|
| LFM2-v8-RL (SOTA) | 34.61 | 13.21 |
| LFM2-v6.4 | 33.53 | 12.31 |
| LFM2-v6.1 | 32.48 | 11.89 |

## ⚙️ Requirements

- Colab T4 GPU (15GB VRAM)
- Evaluation time: ~15min per model
