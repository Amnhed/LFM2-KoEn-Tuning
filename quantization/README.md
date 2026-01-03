[🇺🇸 English](README_EN.md)

# 🔧 Quantization

GGUF 양자화 변환 노트북

## 📂 파일 목록

| 파일 | 설명 |
|------|------|
| `convert_to_gguf_github.ipynb` | GGUF 변환 (GitHub용, 토큰 제거) |
| `convert_to_gguf.ipynb` | 원본 (토큰 포함, 참고용) |

## 🎯 지원 양자화

| 양자화 | 크기 | 품질 | 용도 |
|--------|:----:|:----:|------|
| **Q8_0** 🏆 | 1.25G | 최고 | 품질 최우선 |
| **Q5_K_M** | 843M | 우수 | 균형 추천 |
| **Q4_K_M** | 731M | 양호 | 경량화/모바일 |

## 🚀 사용법

### 1. Colab에서 실행
```
GitHub → convert_to_gguf_github.ipynb → Colab에서 열기
```

### 2. 모델 설정
```python
MODEL_ID = "gyung/lfm2-1.2b-koen-mt-v8-rl-10k-merged"
OUTPUT_REPO = "gyung/lfm2-1.2b-koen-mt-v8-rl-10k-merged-GGUF"
```

### 3. 변환 과정
1. llama.cpp 빌드
2. HuggingFace 모델 다운로드
3. FP16 GGUF 변환
4. Q4/Q5/Q8 양자화
5. HuggingFace 업로드

## 📊 성능 비교

| 양자화 | CHrF++ | BLEU | fp32 대비 |
|--------|:------:|:----:|:---------:|
| fp32 | 34.32 | 13.10 | - |
| Q8_0 | 34.39 | 12.93 | +0.07 |
| Q5_K_M | 34.08 | 12.78 | -0.24 |
| Q4_K_M | 33.97 | 12.56 | -0.35 |

> **결론**: 양자화가 품질에 미치는 영향 거의 없음!

## ⚙️ 환경 요구사항

- Colab CPU 인스턴스 (GPU 불필요)
- High-RAM 권장 (대형 모델의 경우)
- 변환 시간: ~30분

## ⚠️ 주의사항

- `convert_to_gguf_github.ipynb`: 토큰이 `login()` 형식으로 대체됨
- `convert_to_gguf.ipynb`: 원본 (`.gitignore`에 포함, GitHub에 업로드 안됨)
- 실행 전 `OUTPUT_REPO`를 본인 HuggingFace ID로 변경 필요
