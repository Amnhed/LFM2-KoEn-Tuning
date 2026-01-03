[🇺🇸 English](README_EN.md)

# 🏋️ Kaggle Notebooks

Kaggle에서 실행 가능한 학습 노트북

## 📂 파일 목록

| 파일 | 설명 | GPU | 시간 |
|------|------|:---:|:----:|
| `SFT_v6.1_curriculum.ipynb` | SFT Curriculum Learning (v6.1) | T4 x2 | ~5h |
| `SFT_v6_200k.ipynb` | SFT 200k 데이터 학습 | T4 x2 | ~8h |

## 🔧 사용법

### 1. Kaggle 설정 필수 사항

1. **Accelerator**: GPU T4 x2
2. **Internet**: On (모델 다운로드 필요)
3. **Secrets**: `HF_TOKEN` 설정

### 2. 데이터셋 추가

```
Add Data → Upload → .jsonl 파일 업로드
```

### 3. HuggingFace 토큰 설정 (Kaggle Secrets)

```python
from kaggle_secrets import UserSecretsClient
user_secrets = UserSecretsClient()
os.environ["HF_TOKEN"] = user_secrets.get_secret("HF_TOKEN")
```

## ⚙️ Kaggle T4 x2 설정

```python
# DDP (Data Parallel) 설정
accelerate launch --num_processes=2 train.py

# Batch Size 계산
# per_device=1 x gradient_accumulation=16 x gpu=2 = effective 32
```

## 📌 Colab vs Kaggle

| 항목 | Colab T4 | Kaggle T4 x2 |
|------|----------|--------------|
| GPU | 1개 | 2개 |
| VRAM | 15GB | 30GB |
| 세션 | 12시간 | 12시간 |
| 가격 | 무료 | 무료 |

## ⚠️ 주의사항

- Kaggle은 DDP 전용 최적화됨
- Colab 노트북과 코드가 다를 수 있음
