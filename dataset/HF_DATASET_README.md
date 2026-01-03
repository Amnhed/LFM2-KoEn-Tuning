---
license: apache-2.0
language:
- ko
- en
tags:
- translation
- lfm2
- grpo
- sft
dataset_info:
- config_name: grpo_sample_100
  features:
  - name: input
    dtype: string
  - name: output
    dtype: string
  - name: direction
    dtype: string
  splits:
  - name: train
    num_bytes: 12358
    num_examples: 106
  download_size: 10929
  dataset_size: 12358
- config_name: manual_1000_grpo
  features:
  - name: input
    dtype: string
  - name: output
    dtype: string
  - name: direction
    dtype: string
  splits:
  - name: train
    num_bytes: 557584
    num_examples: 2000
  download_size: 332735
  dataset_size: 557584
- config_name: manual_1000_sft
  features:
  - name: instruction
    dtype: string
  - name: input
    dtype: string
  - name: output
    dtype: string
  - name: source
    dtype: string
  - name: model
    dtype: string
  splits:
  - name: train
    num_bytes: 678584
    num_examples: 2000
  download_size: 333746
  dataset_size: 678584
- config_name: sft_sample_100
  features:
  - name: instruction
    dtype: string
  - name: input
    dtype: string
  - name: output
    dtype: string
  - name: source
    dtype: string
  - name: model
    dtype: string
  splits:
  - name: train
    num_bytes: 18029
    num_examples: 106
  download_size: 11901
  dataset_size: 18029
configs:
- config_name: grpo_sample_100
  data_files:
  - split: train
    path: grpo_sample_100/train-*
- config_name: manual_1000_grpo
  data_files:
  - split: train
    path: manual_1000_grpo/train-*
- config_name: manual_1000_sft
  data_files:
  - split: train
    path: manual_1000_sft/train-*
- config_name: sft_sample_100
  data_files:
  - split: train
    path: sft_sample_100/train-*
---

# 🇰🇷🇺🇸 LFM2-KoEn-Samples

**LiquidAI LFM2-1.2B 모델의 한국어-영어 번역 파인튜닝을 위한 학습 데이터셋입니다.**

SFT(Supervised Fine-Tuning) 및 GRPO(Group Relative Policy Optimization) 강화학습을 위한 포맷을 제공합니다.

## 📂 데이터셋 구성 (Configurations)

이 데이터셋은 `datasets` 라이브러리의 `name` (config) 파라미터를 통해 원하는 데이터를 로드할 수 있습니다.

| Config Name | 설명 | 수량 (행) | 용도 |
|-------------|------|:---:|------|
| **`manual_1000_sft`** | 수동 제작 고품질 데이터 (SFT 포맷) | 2,000 | **SFT 학습 (Main)** |
| **`manual_1000_grpo`** | 수동 제작 고품질 데이터 (GRPO 포맷) | 2,000 | **RL 학습 (Main)** |
| `sft_sample_100` | SFT 학습용 샘플 데이터 | 106 | 포맷 테스트 |
| `grpo_sample_100` | GRPO 학습용 샘플 데이터 | 106 | 포맷 테스트 |

> **참고**: 모든 데이터셋은 `En->Ko` 및 `Ko->En` 양방향 데이터를 포함하여 원본 쌍의 2배 개수입니다.

## 🚀 사용 방법

```python
from datasets import load_dataset

# 1. SFT 데이터 로드 (Main)
dataset_sft = load_dataset("gyung/lfm2-koen-samples", "manual_1000_sft")
print(dataset_sft['train'][0])

# 2. GRPO 데이터 로드 (Main)
dataset_grpo = load_dataset("gyung/lfm2-koen-samples", "manual_1000_grpo")
print(dataset_grpo['train'][0])
```

## 📊 데이터 형식 (Format)

### 1. SFT Format (`manual_1000_sft`)

Instruction Tuning을 위한 형식입니다.

```json
{
  "instruction": "Translate the following text to Korean.",
  "input": "The weather is exceptionally clear today, making it perfect for a picnic.",
  "output": "오늘 날씨가 유난히 맑아서 소풍 가기에 완벽합니다.",
  "source": "manual",
  "model": "Gemini 3 Pro"
}
```

### 2. GRPO Format (`manual_1000_grpo`)

강화학습(RL)을 위해 Input/Output이 분리된 형식입니다. `direction` 키가 포함될 수 있습니다.

```json
{
  "input": "제2외국어를 배우는 것은 인지 능력을 크게 향상시킬 수 있습니다. 연구에 따르면 이중 언어 사용자는 단일 언어 사용자에 비해 더 나은 문제 해결 능력, 향상된 멀티태스킹 능력, 그리고 나이와 관련된 인지 저하의 지연을 보이는 경우가 많습니다.",
  "output": "Learning a second language can significantly enhance cognitive abilities. Studies have shown that bilingual individuals often exhibit better problem-solving skills, improved multitasking capabilities, and a delayed onset of age-related cognitive decline compared to monolinguals.",
  "direction": "ko2en"
}
```

## 🛠️ 제작 정보

- **Language Directions**: English ↔ Korean (Bidirectional)
- **Source**: Manually curated / AI assisted verification
- **License**: Apache 2.0
