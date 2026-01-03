[🇰🇷 한국어](README.md)

# 📚 Dataset

Training data samples and upload scripts

## 📂 Structure

```
dataset/
├── dataset_manual_1000_sft.jsonl     # Gemini 3 Pro dataset (SFT, 1000)
├── dataset_manual_1000_grpo.jsonl    # Gemini 3 Pro dataset (GRPO, 1000)
├── samples/                          # Training data samples
│   ├── sample_sft_100_bidirectional.jsonl
│   └── sample_grpo_100_bidirectional.jsonl
├── upload_to_hf.py                   # Upload script (personal)
└── upload_to_hf_github.py            # Upload script (GitHub public)
```

## 📊 Data Format

### SFT Data
```json
{
  "instruction": "Translate the following text to Korean.",
  "input": "The weather is exceptionally clear today, making it perfect for a picnic.",
  "output": "오늘 날씨가 유난히 맑아서 소풍 가기에 완벽합니다."
}
```

### GRPO Data
```json
{
  "input": "Hello, world!",
  "output": "안녕하세요, 세계!"
}
```

## 🚀 Usage

### 1. Environment Setup
```bash
# Create .env file in project root
cp ../.env.example ../.env

# Add HF token to .env
HF=your_huggingface_token_here
```

### 2. Upload
```bash
cd dataset

# Upload all samples
python upload_to_hf.py

# Upload specific file
python upload_to_hf.py --file sample_sft_100_bidirectional.jsonl

# Upload to different repo
python upload_to_hf.py --repo YOUR_ID/your-dataset-name
```

## ⚠️ Notes

- `upload_to_hf.py`: Contains personal REPO_ID (in `.gitignore`, not uploaded)
- `upload_to_hf_github.py`: Changed to `YOUR_ID` (public)
- Change `REPO_ID` in `upload_to_hf_github.py` to your own before use
