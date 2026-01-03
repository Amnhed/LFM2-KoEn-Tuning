# 📊 Evaluation

모델 성능 평가용 벤치마크 노트북

## 📂 파일 목록

| 파일 | 설명 |
|------|------|
| `benchmark_flores200.ipynb` | Flores-200 벤치마크 (1012 샘플) |

## 🎯 평가 지표

| 지표 | 설명 |
|------|------|
| **CHrF++** | Character n-gram F-score (주요 지표) |
| **BLEU** | Bilingual Evaluation Understudy |

## 🚀 사용법

### 1. Colab에서 실행
```
GitHub → benchmark_flores200.ipynb → Colab에서 열기
```

### 2. 평가할 모델 설정
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

### 3. 결과 확인
- CSV 파일 자동 다운로드
- 문장별 번역 결과 비교 가능

## 📈 벤치마크 결과 예시

| Model | CHrF++ | BLEU |
|-------|:------:|:----:|
| LFM2-v8-RL (SOTA) | 34.61 | 13.21 |
| LFM2-v6.4 | 33.53 | 12.31 |
| LFM2-v6.1 | 32.48 | 11.89 |

## ⚙️ 환경 요구사항

- Colab T4 GPU (15GB VRAM)
- 평가 시간: 모델당 ~15분
