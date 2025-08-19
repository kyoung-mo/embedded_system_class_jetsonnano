# 📘 2025년 임베디드 시스템 수업 요약

## 1주차 – Jetson Orin Nano 개발 환경 구축
- **수업 목표**: 딥러닝 프레임워크(PyTorch) 사용법, 임베디드 보드 활용법, 정수 연산 변환, 디바이스 제어 학습.  
- **Jetson Orin Nano 특징**: ARM CPU + Ampere GPU, ROS2, CUDA, cuDNN 지원.  
- **환경 구축**:  
  - PuTTY로 보드 초기 설정 (언어, 계정, 파티션, 네트워크).  
  - `nmcli`로 Wi-Fi 연결 및 ssh 접속.  
  - Linux 기본 명령어(`ls`, `cd`, `mkdir`, `vim`).  
  - Jetson-stats(`jtop`) 설치 후 시스템 모니터링.  
- **Docker 활용**:  
  - 컨테이너 실행(`docker run`), 이미지 관리(`docker pull`, `commit`, `stop`).  
  - 파이썬 패키지 설치 및 Jupyter Notebook 환경 구성.  

---

## 2주차 – Tensor & Dataset
- **Jupyter Notebook 환경**: Docker 컨테이너 실행 후 Notebook 실행 및 코드 실습.  
- **Numpy**:  
  - 다차원 배열 연산, 속성(`shape`, `dtype`).  
  - 배열 생성(`np.array`, `np.zeros`, `np.random.rand`).  
  - 연산(`+`, `*`, `@`, `np.add`, `np.dot`).  
  - 변환(`concatenate`, `reshape`).  
- **PyTorch Tensor**:  
  - Numpy와 유사한 연산 가능, GPU 전송(`.to('cuda')`).  
  - Tensor ↔ Numpy 변환 (`tensor.numpy()`, `torch.from_numpy`).  
- **Dataset & DataLoader**:  
  - `MNIST_784` 불러오기 → Train/Test 분할.  
  - `TensorDataset`, `DataLoader` 활용해 배치 처리.  

---

## 3주차 – CNN Model Training (1)
- **데이터셋 시각화**:  
  - Torchvision을 통한 MNIST, CIFAR100 다운로드/전처리.  
  - Grayscale vs RGB 시각화(Matplotlib).  
- **모델 구성 요소**:  
  - `Linear`, `ReLU`, `Conv2d`, `Pooling(MaxPool)`.  
  - `nn.Module` 기반 네트워크 정의 및 `forward` 함수 작성.  
- **훈련 과정**:  
  - 변수: `batch_size`, `epoch`, `learning rate`.  
  - 손실 함수, Optimizer, GPU 활용.  
  - 모델 저장(`torch.save`) 및 불러오기(`eval`, `torch.no_grad`).  
- **실습 포인트**: Epoch 증가에 따른 성능 변화 관찰.  

---

## 4주차 – CNN Model Training (2)
- **Normalization & Standardization**:  
  - `transforms.ToTensor()`: [0,1] 범위 정규화.  
  - `transforms.Normalize()`: 평균=0, 표준편차=1 표준화.  
  - CIFAR100에 적용 후 성능 비교.  
- **Batch Size 효과**:  
  - 작은 batch → 일반화 성능 ↑, 학습 속도 ↓.  
  - 큰 batch → 학습 속도 ↑, 일반화 성능 ↓.  
- **Model Complexity**:  
  - 레이어 수·필터 크기 증가 시 복잡도 증가.  
  - 과적합 위험 → 데이터 다양성 필요.  
  - **실습**: 다양한 변수(`Batch size`, `Layer 수`, `Epoch` 등) 조정해 최적 모델 구현.  

---

## 5주차 – Batch Normalization & Dropout
- **Batch Normalization (BN)**:  
  - 각 미니배치의 평균/표준편차 기반 정규화.  
  - 학습 안정성 증가, Convolution 뒤에 위치.  
  - `nn.BatchNorm1d`, `nn.BatchNorm2d` 사용.  
- **Dropout**:  
  - 학습 중 일부 뉴런 무작위 차단(`p` 확률).  
  - 과적합 방지, 일반화 성능 개선.  
  - 학습 시와 추론 시 동작 차이 존재.  
- **실습**: BN/Dropout 적용 여부에 따른 CIFAR100 성능 비교.  

---

## 8주차 – Quantization (1)
- **개념**: FP32 → INT8 변환, 추론 성능·속도 개선, 전력 감소.  
- **문제점**: Quant/Dequant Layer 추가 시 오버헤드 발생 → Layer Fusion 필요.  
- **방식**:  
  - **PTQ**: 훈련된 FP32 모델에 Calibration만 적용. 빠르지만 정확도 ↓.  
  - **QAT**: Quantization-aware Training. Fake Quantization으로 학습, 정확도 ↑.  
- **실습**:  
  - Jetson Orin Nano에서 FP32 vs INT8 모델 성능 비교.  
  - Calibration 알고리즘(Entropy vs Min/Max) 차이 확인.  

---

## 9주차 – Quantization (2)
- **ResNet18 활용**: CNN보다 파라미터가 많아 Quantization 효과 ↑.  
- **실험**: FP32 vs INT8 TensorRT 엔진 성능 비교(속도, 전력, 메모리).  
- **Layer 최적화**:  
  - AvgPooling → 단순 합/평균 → Quantization에 유리.  
  - ReLU6 → 6 이상 값 클리핑 → Scale 안정화.  
- **실습**: 기존 CNN에 AvgPooling + ReLU6 적용 후 QAT 성능 비교.  

---

## 10주차 – Boosting Performance
- **Data Augmentation**:  
  - 기법: Horizontal Flip, Random Crop, Cutout, Color Jitter.  
  - 목적: 데이터 다양성 확보, 과적합 방지.  
- **Residual Connection**:  
  - 입력을 직접 전달하여 Gradient 소실 방지.  
  - ResNet 구조 기반 → 안정적 학습.  
- **Squeeze-and-Excitation(SE)**:  
  - 채널 간 중요도 학습 → 정보 집중도 ↑.  
  - Global Avg Pooling + FC + Sigmoid 구조.  
- **실습**: 증강 기법 비교, Residual & SE 적용 모델 성능 분석.

---

## 🔹 11주차 – 인터럽트(Interrupt)
### 이론
- 인터럽트 개념: CPU가 실행 중인 작업을 멈추고 우선순위 높은 이벤트 처리  
- 종류: 하드웨어 인터럽트(외부 장치), 소프트웨어 인터럽트(프로그램 내 명령)  
- 인터럽트 벡터와 서비스 루틴(ISR) 동작 원리 설명  
- Jetson Orin Nano 환경에서 GPIO 이벤트를 인터럽트로 처리하는 방법 학습  

### 실습
- Python `gpiozero` 라이브러리 활용  
- 버튼 입력 시 인터럽트 발생 → LED 점등/소등 동작 확인  
- ISR 역할을 하는 콜백 함수 작성 및 실행  

### 추가 실습
- 버튼을 짧게 누르면 LED ON, 길게 누르면 LED OFF  
- 인터럽트 중복 발생 시 처리 방식 조사  

---

## 🔹 12주차 – PWM (Pulse Width Modulation)
### 이론
- PWM 원리: 주기(T) 내에서 ON 시간(High)의 비율(Duty Cycle)로 아날로그 신호 모사  
- 활용 예시: 모터 속도 제어, LED 밝기 조절, 오디오 신호 생성  
- Jetson Orin Nano에서 PWM 핀 활용법  

### 실습
- Python `Jetson.GPIO` 활용하여 PWM 신호 발생  
- LED 밝기 조절(10%, 50%, 90% Duty Cycle 실험)  
- 서보 모터 제어(0°, 90°, 180° 회전 확인)  

### 추가 실습
- 점진적으로 LED 밝기 변하게 하는 Fade-in / Fade-out 구현  
- 서보 모터를 버튼 입력에 따라 각도 조절  

---

## 🔹 13주차 – I2C 통신
### 이론
- I2C 개요: SDA, SCL 두 선으로 Master-Slave 구조 통신  
- Start/Stop 조건, ACK/NACK 원리  
- Slave는 7bit 주소 사용, Master는 Read/Write 결정  
- Jetson Orin Nano `i2c-7 bus` 및 `/dev/i2c-7` 장치 확인 방법  

### 실습
- `i2cdetect`로 SSD1306 OLED 모듈 인식 확인  
- Adafruit_SSD1306, PIL 라이브러리 설치 및 사용  
- OLED 디스플레이 초기화, 직사각형/텍스트 출력  

### 추가 실습
- Pillow 라이브러리로 도형(사각형, 원, 텍스트) 출력  
- 팀원 학번을 OLED 화면에 표시  

---

## 🔹 14주차 – SPI 통신
### 이론
- SPI 개요: Master-Slave 기반의 고속 직렬 통신  
- 4개 신호선 사용: MISO, MOSI, SCK, CS  
- Full-duplex 통신 가능, I2C보다 빠른 속도  
- Jetson Orin Nano의 SPI 장치(`/dev/spidev*`) 활용  

### 실습
- Python `spidev` 모듈 사용하여 SPI 통신 구현  
- SPI 신호 확인 및 데이터 송수신 테스트  
- OLED/TFT 디스플레이 모듈 제어  

### 추가 실습
- SPI 장치를 통해 문자열 전송 → 디스플레이 출력  
- I2C와 SPI의 장단점 비교 및 실제 응용 사례 조사  


