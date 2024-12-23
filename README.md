# **Data-Creator-Camp** | 2024 데이터 크리에이터 캠프

### 🏆 우수상 (한국지능정보사회진흥원 원장상) 수상

- **팀원 : 김홍재(팀장), 김동현, 박준영, 배한준**
- **팀명 : 비타맥스**

---

## 🌟 **Introduction | 대회 소개**

데이터 크리에이터 캠프는 데이터 분석 저변 확대와 창의력 있는 인재 양성을 위한 데이터 분석, 인공지능 분야 대회로 과학기술정보통신부와 한국지능정보사회진흥원이 주최하며 K-ICT 빅데이터센터가 주관합니다.

---

## 📅 **Progress Period | 진행 기간**

- **2024.09.23 ~ 2024.11.30**

---

## 🚀 **Process |** 수행 과정

### Mission 1 (ResNet-18을 이용한 패션 스타일 이미지 분류)

![스크린샷 2024-12-21 오전 1.02.32.png](https://github.com/user-attachments/assets/48eaed85-c9fa-483f-8534-fe23eb988e06)

- 주어진 이미지에 대해 총 31가지의 성별+스타일 조합을 예측하는 문제
- 사용 모델 : ResNet-18
- 데이터 변환 방법 : 시멘틱 세그멘테이션(Deeplabv3_MobileNetV3_Large)
- 성능 향상 방법 : 데이터 증강(Resize/Rotate) / 레이블 스무딩(e:0.05) / 스케쥴러(size=5)
- 최종 모델 : validation Top-1 Score 기준 64.35% (epoch 50)

### Mission 2 (라벨 데이터를 통한 패션 스타일 선호 여부 파악)

![스크린샷 2024-12-21 오전 1.02.51.png](https://github.com/user-attachments/assets/ce456332-2c0c-4442-b134-df938fc86da3)

- 라벨링 데이터로부터 스타일 선호 정보표 생성
- 이미지 데이터와 유효한 라벨링 데이터에 동시에 존재하는 ID의 데이터만 추출
- 라벨링 데이터(json)의 선호 여부 추출

### Mission 3 (Item-based Filtering을 이용한 패션 스타일 선호 여부 예측)

![스크린샷 2024-12-21 오전 1.03.57.png](https://github.com/user-attachments/assets/d190a6bb-271e-4608-81c5-4fc46fc60e48)

- 이미지 간의 유사도를 이용한 패션 이미지 선호 여부 예측
- 사용 방법 : 혼합 매트릭스를 이용한 아이템 기반 필터링
- 모델 개선 : 이웃의 개수와 최소 유사도 파라미터 추가 및 Optuna 튜닝
- 방법 상세
    1. 미션 2의 스타일 선호 정보표로부터 Rating Matrix 구성
    2. 미션1의 ResNet으로부터 추출한 이미지 피처 벡터와 라벨링 데이터의 유의미한 설문 정보를 결합하여 혼합 매트릭스 구성
    3. 혼합 매트릭스의 코사인 유사도를 계산하여 아이템 간 유사도 매트릭스 생성
    4. 유사도를 가중치로 활용하여 valid data의 추정값을 구하고 임계치와 비교하여 최종 예측
- 최종 모델 : F1 Score 86.67% / Accuracy 89.20%

---

## 📁 **Key Directories and Files | 주요 디렉토리 및 파일**

- `notebooks/`: 미션 수행 Jupyter notebook
- `presentation/`: 미션 수행 과정을 담은 발표 자료
- `resources/`: 스타일 선호 정보표, Feature Matrix 등 코드 실행에 필요한 리소스 파일
