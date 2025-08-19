# 임베디드 시스템 (Jetson Nano 2GB 기반) – 실전형 프로젝트 중심



---

| 참고 사이트 | 링크 |
|-------------|------|
| Jetson Orin Nano | https://www.yahboom.net/study/Jetson-Orin-NANO |
| Jetson Nano 4GB  | https://www.yahboom.net/study/jetson-nano-2 |
| Jetson Nano 2GB  | https://www.yahboom.net/study/Jetson-nano-2GB |


---

# 📘 내년 임베디드 시스템 수업 계획 (수정안)

## 📌 과목 개요
이 수업은 **Jetson Nano 2GB** 보드를 기반으로 임베디드 시스템을 학습하고, 딥러닝 기반 **Object Detection** 및 IoT 융합 프로젝트를 실습합니다.  
최종적으로는 **캡스톤 디자인에 적용 가능한 주제**를 경험하며, 마지막 주에는 **미니 캡스톤 발표**를 진행합니다.

---

## 🎯 학습 목표
- 리눅스 및 Jetson Nano 환경 설정 능력 습득
- 센서·카메라·디바이스 제어 기술 학습
- 딥러닝 기반 객체 탐지(Object Detection) 프로젝트 경험
- 캡스톤 디자인 연계형 실전 프로젝트 수행 능력 강화

---

## 📅 수업 구성
- **총 15주**
  - 리눅스·디바이스 학습: 8주
  - 오브젝트 디텍션·응용 프로젝트: 6주
  - 미니 캡스톤 발표: 1주
- **매주**: 2시간 이론 + 2시간 실습
- **진행 방식**
  - 각 주차: 개념 학습 + 실습 병행  
  - 프로젝트 단위는 2주(개념 → 구현)

---

## 📂 커리큘럼

## **1주차 – 개발 환경 구축 & 리눅스 기초, Python & 파일 권한**
- Jetson Orin Nano 소개 (Nano ↔ Orin 비교)  
- OS 설치 및 초기 세팅 (언어/계정/네트워크)  
- SSH, VSCode Remote 환경 설정  
- Linux 기본 명령어 (`ls`, `cd`, `mkdir`, `vim`)  
- `jtop` 설치 및 시스템 자원 모니터링
- Python3 환경 확인 및 실행  
- argparse 모듈 기초 (CLI 인자 입력)  
- Linux 파일 권한 구조(`rwx`, `chmod`)  
- **실습**:  
  - `test.py` 작성 후 실행  
  - argparse 활용 간단 계산기 구현  
  - 보드 접속 및 기본 명령어 사용  

---

## **2주차 – GPIO & PWM 제어 (LED, 부저, 서보 통합)**
- GPIO 핀맵 및 Jetson.GPIO 활용  
- PWM 원리 (Duty Cycle, Frequency)  
- **실습**:  
  - LED 점등/점멸 + 밝기 제어 (PWM)  
  - 부저로 음계 출력 (PWM 주파수 제어)  
  - 서보 모터 각도 제어 (0° ↔ 180°)  
- **추가 실습**: 버튼 입력에 따라 LED 밝기 변화 + 서보 회전 + 부저음 동기화  

---

## **3주차 – I2C & SPI 통신 (OLED + ADC 통합)**
- I2C 개념 및 장치 인식 (`i2cdetect`)  
- SPI 개념 (MISO, MOSI, SCK, CS)  
- **실습**:  
  - I2C SSD1306 OLED: 텍스트/도형 출력  
  - SPI MCP3208: 가변저항 입력 읽기  
  - ADC 값 → OLED에 실시간 표시  
- **추가 실습**: 조도 센서/가변저항 입력값을 OLED 그래프 형태로 출력  

---

## **4주차 – Jupyter & Tensor 기초**
- Docker 컨테이너 실행, Jupyter Notebook 환경 구축  
- Numpy 기본 연산 (배열 생성, 연산, 변환)  
- PyTorch Tensor 기본 연산 및 GPU 활용  
- Dataset & DataLoader 개념  
- **실습**: MNIST 데이터 불러오기 & 시각화  

---

## **5주차 – CNN 기초 & 모델 훈련**
- CNN 기본 구조 (Conv2d, ReLU, Pooling, Linear)  
- PyTorch `nn.Module` 기반 CNN 정의  
- **실습**:  
  - MNIST 데이터셋으로 CNN 학습 (Epoch 조정)  
  - 손실 함수 & Optimizer 변경 실험  
- **추가 실습**: CIFAR10 데이터셋으로 확장  

---

## **6주차 – CNN 성능 향상 기법**
- Normalization & Standardization  
- Batch Size 효과 분석  
- Model Complexity (레이어 수, 필터 크기)  
- **실습**:  
  - CIFAR100 데이터셋 학습  
  - Batch size/Layer/Epoch 변화에 따른 정확도 비교  
- **추가 실습**: Data Augmentation 일부 적용 (RandomCrop, Flip)  

---

## **7주차 – CNN 심화 & 시각화**
- Batch Normalization & Dropout  
- Feature Map 시각화, 오분류 케이스 분석  
- **실습**:  
  - BN/Dropout 적용 전후 성능 비교  
  - Matplotlib으로 학습 곡선(Train vs Validation Loss) 시각화  
- **추가 실습**: 직접 만든 작은 Dataset으로 Fine-tuning
  
---

## **8주차 – 객체 탐지(Object Detection) & 카메라 활용**
- 객체 탐지 기본 개념 (Classification vs Detection vs Segmentation)  
- 카메라 입력 처리 과정 (프레임 캡처, 전처리, 후처리)  
- YOLO 계열 모델 개요 (YOLOv3 ~ YOLOv8 특징, 임베디드 친화적 모델)  
- **실습**:  
  - OpenCV로 카메라 영상 캡처 및 출력  
  - 사전 학습된 YOLOv5/YOLOv8 모델 적용 → 실시간 객체 탐지  
  - Bounding Box 및 Confidence Score 시각화  
- **추가 실습**:  
  - 특정 객체 탐지 시 LED/부저 동작 (GPIO 제어)  
  - 직접 수집한 Dataset으로 YOLO Fine-tuning
 
---

### **[Part 2: Object Detection & 응용 프로젝트 (총 6주)]**

#### **Week 9-10: Object Detection 기초**
- YOLOv8 기반 객체 탐지 실습  
- Jetson Nano 최적화 기법(FPS 확인, TensorRT 변환)  

#### **Week 11-12: 객체 탐지 + 하드웨어 연동**
- 특정 클래스 탐지 시 LED·부저 동작  
- 객체 종류 + 거리 표시 (카메라 + 센서 융합)  

#### **Week 13-14: 실시간 응용 프로젝트**
- 예시: AI 블랙박스 / 스마트 CCTV / 안전 감지 시스템  
- 영상 스트리밍 + 원격 제어 기능 포함  

---

### **Week 15: 미니 캡스톤 발표**
- 팀별 프로젝트 결과 발표 및 시연  
- 피드백 및 캡스톤 디자인 적용 아이디어 공유  

---

## 📌 개발 환경
- **하드웨어**: Jetson Nano 2GB, 카메라 모듈, 센서(DHT22, HC-SR04), LED, 부저, 모터  
- **소프트웨어**: Ubuntu 기반 Jetson OS, Python 3.x, OpenCV, PyTorch, TensorRT, MQTT/Firebase  

---

0812:


작년꺼는 보드 사용법이나 리눅스 사용법이나 디바이스 사용법에 대해 진행. 이후 실습 진행
올해꺼는 cnn 올인

디바이스 실습시 시간이 너무 오래걸림
디바이스 사용법 합치기

주피터 노트북 사용한 씨엔엔 제외(작년거)
올해거에서 추가

작년거는 기본적으로 교재 기반 - 리눅스, 기본 세팅, 이를 기반으로 디바이스 연결, 씨엔엔 실습
올해 - 리눅스 시텡, 시엔엔, 디바이스, 씨엔엔+튜닝

내년 - 캡스톤 디자인에 사용 가능한 주제 / 마지막 2주는 발표 - 임베디드 시스템을 사용하여 미니 캡스톤 디자인
리눅스 사용법, 디바이스 사용법(올해거에서 확인)+카메라 사용법
딥러닝 맛보기 올해건 너무 딥했다 -> 오브젝트 디텍션(공유해주신 중국 사이트에서 참고하여 그대로 따라할 수 있게끔)

2주동안 기획만

리눅스 , 디바이스, 카메라 - 8주차

---

0819 : 

