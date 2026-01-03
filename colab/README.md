# 🚀 Colab Notebooks

Google Colab에서 실행 가능한 학습 노트북

## 📂 파일 목록

| 파일 | 설명 | GPU | 시간 |
|------|------|:---:|:----:|
| `GRPO_v8_adapter_github.ipynb` | **GRPO 강화학습** (SOTA 달성) | T4 | ~2h |
| `GRPO_v8_unsloth_vllm_github.ipynb` | GRPO + Unsloth/vLLM 최적화 | T4/L4 | ~2h |
| `SFT_colab_github.ipynb` | **SFT Curriculum** (Colab 스타일) | T4 | ~3h |

## ⚠️ GitHub용 파일 설명

`*_github.ipynb` 파일들은 원본과 **동일한 기능**을 수행하며:
- HF 토큰이 `login()` 형식으로 변경됨 (수동 입력)
- 출력(output) 제거됨
- 주석 정리됨
- `OUTPUT_MODEL_ID`가 `YOUR_ID/your-output-model`로 변경됨 (변경 필요)

## ⚙️ 환경 요구사항

- **T4 GPU**: 무료 Colab에서 사용 가능
- **L4/A100 GPU**: Colab Pro 권장

## 📌 권장 설정 (T4)

```python
TrainingArguments(
    fp16=True,          # BF16 미지원
    gradient_checkpointing=True,
    per_device_train_batch_size=4,
)
```

## ⚠️ 주의사항

- `*_github.ipynb`: 토큰이 `YOUR_HF_TOKEN`으로 대체됨 (GitHub 공개용)
- 원본 파일들은 `.gitignore`에 포함되어 업로드되지 않음
