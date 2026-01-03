[🇺🇸 English](README_EN.md)

# 📚 Dataset

학습 데이터 샘플 및 업로드 스크립트

## 📂 구조

```
dataset/
├── dataset_manual_1000_sft.jsonl     # Gemini 3 Pro 제작 데이터셋 (SFT, 1000개)
├── dataset_manual_1000_grpo.jsonl    # Gemini 3 Pro 제작 데이터셋 (GRPO, 1000개)
├── samples/                          # 학습 데이터 샘플
│   ├── sample_sft_100_bidirectional.jsonl
│   └── sample_grpo_100_bidirectional.jsonl
├── upload_to_hf.py                   # 업로드 스크립트 (개인용)
└── upload_to_hf_github.py            # 업로드 스크립트 (GitHub 공개용)
```

## 📊 데이터 형식

### SFT 데이터
```json
{
  "instruction": "Translate the following text to Korean.",
  "input": "The weather is exceptionally clear today, making it perfect for a picnic.",
  "output": "오늘 날씨가 유난히 맑아서 소풍 가기에 완벽합니다."
}
```

### GRPO 데이터
```json
{
  "input": "Hello, world!",
  "output": "안녕하세요, 세계!"
}
```

## 🚀 사용법

### 1. 환경 설정
```bash
# 프로젝트 루트에 .env 파일 생성
cp ../.env.example ../.env

# .env 파일에 HF 토큰 입력
HF=your_huggingface_token_here
```

### 2. 업로드 실행
```bash
cd dataset

# 모든 샘플 업로드
python upload_to_hf.py

# 특정 파일만 업로드
python upload_to_hf.py --file sample_sft_100_bidirectional.jsonl

# 다른 레포에 업로드
python upload_to_hf.py --repo YOUR_ID/your-dataset-name
```

## ⚠️ 주의사항

- `upload_to_hf.py`: 개인 REPO_ID 포함 (`.gitignore`에 포함, GitHub 업로드 안됨)
- `upload_to_hf_github.py`: `YOUR_ID`로 변경됨 (GitHub 공개용)
- 사용 전 `upload_to_hf_github.py`의 `REPO_ID`를 본인 것으로 변경 필요
