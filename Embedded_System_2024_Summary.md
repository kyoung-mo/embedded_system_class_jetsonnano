# 📘 임베디드 시스템 실습 (1~10주차 요약)

## Week 1 – 리눅스 기본 & 스왑 설정
- **이론**
  - 리눅스 기본 명령어: `ls`, `mkdir`, `cd`, `rm`, `vim`  
  - 메모리 확인: `free -m`, `free -h`  
  - 서비스 제어: `systemctl`  
  - 스왑 메모리 생성 과정 (`fallocate`, `chmod`, `mkswap`, `swapon`)
- **실습**
  - `jtop` 설치 및 실행  
  - `vim`으로 파일 생성 및 편집, 삭제 실습  
  - 스왑 파일(6GB) 생성 및 fstab 등록  
- **추가 실습**
  - student 디렉토리와 학번/이름 파일 만들기  
  - 2GB, 4GB 스왑 파일 생성 및 삭제  

---

## Week 2 – Python & 파일 권한
- **이론**
  - Python3 확인 및 실행 (`python3 -V`, `python3`)  
  - 파일 권한 구조(`rwx`, 8진수 표기)  
  - 권한 변경: `chmod`  
  - argparse 모듈 기초
- **실습**
  - `vim`으로 `test.py` 작성 후 실행  
  - `chmod`로 권한 변경, 실행 불가 파일 실행 테스트  
  - argparse로 CLI 입력 프로그램 작성
- **추가 실습**
  - argparse 활용 계산기 프로그램  

---

## Week 3 – Jetson GPIO 기초
- **이론**
  - GitHub 저장소 `jetson-gpio` 설치  
  - Jetson Nano 40핀 핀맵 이해
- **실습**
  - `simple_out.py` 실행 → LED 점등  
  - `button_led.py` 실행 → 버튼으로 LED 제어
- **추가 실습**
  - 스위치 입력 → LED 점멸 프로그램 작성  

---

## Week 4 – PWM 제어 & LED 밝기
- **이론**
  - Jetson-IO로 핀 설정(`pwm0`, `pwm2`)  
  - PWM 기본 동작 (Duty Cycle, Frequency)
- **실습**
  - `GPIO.PWM` 활용 LED 밝기 조절  
  - `simple_pwm.py` 실행
- **추가 실습**
  - 버튼 입력 시 LED 밝기 점점 증가  

---

## Week 5 – 피에조 부저
- **이론**
  - 주파수에 따라 음계 출력  
  - PWM을 이용한 주파수 제어
- **실습**
  - 멜로디 리스트를 이용해 도~도까지 8개 음계 출력
- **추가 실습**
  1. 도-레-미 반복 3회 출력  
  2. 버튼 입력 시 LED 밝기 + 음계 동기화  

---

## Week 6 – 서보 모터 제어
- **이론**
  - 서보 모터 동작 원리 (PWM 50Hz, Duty 3~12.5%)  
  - 0~180도 제어
- **실습**
  - Python 코드로 서보 각도 제어 (0 ↔ 180도 반복)
- **추가 실습**
  1. argparse로 입력 각도 제어 프로그램  
  2. 버튼 입력 시 30도 단위 회전 (0~180 왕복)  
  3. 버튼 누를 때 180도 유지, 떼면 0도 유지  

---

## Week 7 – I2C & OLED 디스플레이
- **이론**
  - `dpkg`, `i2c-tools` 설치 확인  
  - I2C 개념 및 SSD1306 OLED 모듈  
  - Pillow 라이브러리 (Image, Draw, Font)
- **실습**
  - `i2cdetect`로 장치 확인  
  - `Adafruit_SSD1306` 라이브러리 설치 및 예제 실행  
  - 이미지·도형·텍스트 출력
- **추가 실습**
  1. Pillow 함수 조사 및 학번/이름 출력  
  2. 네모 안에 네모 출력 코드 작성  

---

## Week 8 – SPI & MCP3208 ADC
- **이론**
  - SPI 설정 (`jetson-io.py`)  
  - MCP3208: 12bit ADC (0~3.3V → 0~4095)  
  - `spidev` Python 패키지
- **실습**
  - SPI 초기화 및 데이터 전송 (`xfer`)  
  - 아날로그 입력 전압 읽기 (가변저항)
- **추가 실습**
  1. 차동 입력 모드 구현  
  2. PWM + ADC → 가변저항에 따른 LED 밝기 제어  

---

## Week 9 – Docker & 카메라
- **이론**
  - Docker 실행 파일(`docker_dli_run.sh`) 작성  
  - Jupyter Notebook 접속 (`http://[ip]:8888`)  
  - 기본 비밀번호: `dlinano`
- **실습**
  - `usb_camera.ipynb` 실행 → USB 카메라 영상 확인  

---

## Week 10 – 딥러닝 분류 (Jupyter Notebook)
- **이론**
  - `classification_interactive.ipynb` 실행  
  - 데이터셋: `thumbs_up`, `thumbs_down`  
  - 모델 저장/불러오기 (Save & Load Model)  
  - Epochs 개념 (훈련 횟수)
- **실습**
  - 제스처 데이터 직접 촬영 (각 30장)  
  - Epochs 값 변경 후 성능 비교  
  - 저장된 모델 불러와 추가 학습
- **탐구 과제**
  - Epochs 및 데이터 크기에 따른 성능 차이 분석  
