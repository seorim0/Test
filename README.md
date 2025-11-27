# 🚀 AI 기반 이미지 분류 시스템 개발 프로젝트

본 문서는 AI 이미지 분류 시스템을 구축한 가상의 프로젝트 결과를 정리한 문서입니다.  
프로젝트는 이미지 데이터를 활용하여 사물 종류를 자동으로 분류하는 딥러닝 모델을 개발하는 것을 목표로 했습니다.

---

## 📌 프로젝트 개요

- **프로젝트명:** VisionFlow  
- **기간:** 2024.03 ~ 2024.06  
- **팀 구성:** 4명 (ML Engineer 2, Backend 1, PM 1)  
- **목표:**  
  - 20개 카테고리의 이미지를 95% 이상 정확도로 분류하는 AI 모델 개발  
  - 경량화 모델을 통해 Edge Device에서도 실시간 추론 가능하도록 최적화  
  - API 형태로 모델 제공 및 Dashboard 구축  

---

## 🧠 사용 기술

| 영역 | 기술 스택 |
|------|-----------|
| **ML / DL** | PyTorch, TorchVision, ONNX, Optuna |
| **Data Pipeline** | Python, NumPy, Albumentations |
| **Backend** | FastAPI, Docker |
| **Dashboard** | React, Chart.js |
| **Infra** | AWS EC2, S3, Lambda |

---

## 📂 데이터셋

- 총 **45,000장**의 이미지  
- 20 클래스(동물, 교통수단, 일상용품 등)  
- Train/Validation/Test = **70% / 20% / 10%**  
- 주요 전처리:
  - RandomCrop, HorizontalFlip, ColorJitter
  - 이미지 크기 224×224 통일
  - Label smoothing 적용

---

## 🤖 모델 구조 및 학습

### 모델 구조
- ResNet-50 기반 Transfer Learning  
- 마지막 FC Layer 변경 (2048 → 20 Class)  
- Swish Activation 적용  
- Dropout 0.4 사용  

### 하이퍼파라미터
| 항목 | 값 |
|------|-----|
| Batch Size | 32 |
| Learning Rate | 1e-4 |
| Optimizer | AdamW |
| Epoch | 40 |
| Scheduler | CosineAnnealing |

---

## 📈 성능 결과

### 최종 정확도
- **Top-1 Accuracy: 96.4%**
- **Top-5 Accuracy: 99.1%**

### Confusion Matrix 예시
```
정확도가 낮은 클래스:
- 고양이 ↔ 너구리 (약 8% 오분류)
- 바이크 ↔ 스쿠터 (약 5% 오분류)
```

### 모델 경량화 결과
| 모델 버전 | 용량 | 추론 속도 (ms) |
|-----------|------|----------------|
| Base | 95MB | 62ms |
| ONNX 최적화 | 41MB | 28ms |
| Quantized | 18MB | 17ms |

---

## 🌐 API 구성

### 엔드포인트
| Method | Endpoint | 설명 |
|--------|----------|------|
| POST | `/predict` | 이미지 업로드 후 클래스 예측 |
| GET | `/health` | 서버 헬스 체크 |
| GET | `/logs` | 최근 예측 로그 조회 |

### 예시 요청
```bash
curl -X POST "https://api.visionflow.ai/predict" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@sample.jpg"
```

---

## 📊 대시보드 기능

- 실시간 추론 결과 시각화  
- 클래스별 정확도 차트 제공  
- 최근 업로드 이미지 히스토리  
- 모델 버전 관리 페이지  

---

## 📝 회고 및 향후 계획

### 팀 회고
- 💡 *데이터셋 불균형을 초기에 해결했으면 학습 속도와 성능 모두 더 개선됐을 것*  
- ⚙️ *모델 경량화 작업에서 ONNX 변환 이슈가 반복적으로 발생해 예상보다 시간이 많이 소모됨*  

### 향후 개선 방향
- 클래스 확장 (20 → 50)  
- Hierarchical Classification 구조 적용  
- 모바일 앱 연동  

---

## 📦 Repository 구조 (예시)

```
📁 VisionFlow
 ├── 📂 data
 ├── 📂 models
 ├── 📂 src
 │    ├── train.py
 │    ├── dataset.py
 │    ├── inference.py
 │    └── utils.py
 ├── 📂 api
 │    ├── main.py
 │    └── routers/
 ├── 📂 dashboard
 └── README.md
```

---

필요하면 다른 콘텐츠나 분야로 된 버전도 만들어드릴게요!
