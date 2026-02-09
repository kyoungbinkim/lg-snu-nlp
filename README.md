# lg-snu-nlp
LG전자 서울대학교 AI Scientist 고급과정 자연어처리 Project

## 실행 결과
📊 **[실행 결과 보기 (Google Drive)](https://drive.google.com/drive/folders/1uvv1f-sgWt3y1zUc5JlKXdIPsVyBiU63?usp=sharing)**

---

## Project Information

| 항목 | 내용 |
|------|------|
| **Presenter** | 김경빈 |
| **Topic** | Privacy-Preserving LLM Inference for Korean Text |
| **Data and Baseline** | [SnD (Split-and-Denoise) - ICML 2024](https://github.com/NusIoraPrivacy/eaas-privacy) |
| **Novel Hypothesis** | Petals와 같은 분산형 LLM 추론 환경에서 프라이버시 노출 위험이 존재함. SnD(Split-and-Denoise) 기법을 한국어 텍스트에 적용하여 Local Differential Privacy(LDP)를 통한 프라이버시 보호 효과를 검증하고, 한국어 특성에 맞는 최적화 방안을 제안함. |
| **Output** | GitHub repo, PPT |

---

## Background

### Petals의 프라이버시 문제
- **Petals**: 분산형 LLM 추론 시스템으로, 여러 사용자가 협력하여 대형 모델을 실행
- **문제점**: 클라이언트가 텍스트/임베딩을 서버에 직접 전송 → 민감한 정보 노출 위험

### Split-and-Denoise (SnD) 접근법
- **논문**: "Split-and-Denoise: Protect large language model inference with local differential privacy" (ICML 2024)
- **핵심 아이디어**:
  1. 토큰 임베딩 레이어를 클라이언트에서 실행 (최소 연산 비용)
  2. 클라이언트가 임베딩에 노이즈를 추가한 후 서버로 전송
  3. 서버는 노이즈가 추가된 임베딩으로 추론 수행
  4. Denoise 모델을 통해 출력 품질 복원

---

## Reference

### Paper
- **Title**: Split-and-Denoise: Protect large language model inference with local differential privacy
- **Authors**: Peihua Mai, Ran Yan, Zhe Huang, Youjia Yang, Yan Pang
- **Venue**: ICML 2024
- **arXiv**: [https://arxiv.org/abs/2310.09130](https://arxiv.org/abs/2310.09130)

### Code
- **Original Repository**: [https://github.com/NusIoraPrivacy/eaas-privacy](https://github.com/NusIoraPrivacy/eaas-privacy)

---

## Project Structure

```
lg-snu-nlp/
├── README.md                          # 프로젝트 설명
├── notebooks/
│   └── snd_gpt2_korean_experiment.ipynb  # KoGPT2 한국어 실험 노트북
├── src/                               # 소스 코드 (추후 추가)
└── data/                              # 데이터셋 (추후 추가)
```

---

## Model

### KoGPT2 (SKT-AI)
- **Repository**: [https://github.com/SKT-AI/KoGPT2](https://github.com/SKT-AI/KoGPT2)
- **HuggingFace**: `skt/kogpt2-base-v2`
- **Parameters**: 125M
- **Architecture**: Decoder (12 layers, 12 heads, hidden size 768)
- **Training Data**: 한국어 위키피디아, 뉴스, 모두의 말뭉치 등 40GB+ 텍스트
- **Tokenizer**: Character BPE (vocab size: 51,200)

---

## Experiments

### 목표
1. GPT-2 모델을 활용한 SnD 프레임워크 구현
2. 한국어 텍스트 데이터셋에 대한 실험
3. Privacy-Utility Trade-off 분석

### 주요 파라미터
- **Noise Mechanism**: ChiDP (Chi-squared Differential Privacy) 또는 Gaussian
- **Privacy Budget (η/epsilon)**: 다양한 값으로 실험 (50, 100, 150)
- **Base Model**: KoGPT2 (SKT-AI) - 한국어 특화 GPT-2

### 평가 지표
- **Privacy**: Differential Privacy Budget (ε)
- **Utility**: Task-specific metrics (Accuracy, F1, etc.)
- **Denoising Quality**: MSE, Cosine Similarity

---

## How to Run

```bash
# 환경 설정
pip install torch transformers datasets tqdm h5py numpy

# Jupyter Notebook 실행
jupyter notebook notebooks/snd_gpt2_korean_experiment.ipynb
```

---

## License

This project is for academic purposes as part of the LG-SNU AI Scientist Advanced Course.
