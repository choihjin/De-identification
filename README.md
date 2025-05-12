# 🔒 Image & Video De-identification System

이미지 및 영상 내 번호판과 얼굴 정보를 자동으로 비식별화하는 딥러닝 기반 시스템입니다.

<img src="src/pipeline.png" width="800">


## 주요 기능

- **DeepLabV3 기반 번호판 Segmentation**
- **YOLOv5 기반 얼굴 검출 및 블러 처리**
- 이미지 및 영상 파일의 자동 비식별화 파이프라인
- CLI 기반 다중 입력, 디렉토리 처리 기능

## 기술 스택

- Python 3.11.5
- PyTorch, OpenCV, torchvision
- DeepLabV3 (License Plate), YOLOv5 (Head Detection)
- CUDA 11+

## 비식별화 처리 흐름

### 1. 데이터 구조
```
.
├── data/ # 원본 이미지/영상
│ ├── input1.png
│ └── input2.mp4
├── license/ # 번호판 비식별화 결과
├── output/ # 최종 출력 결과
├── pytorch_licenseplate_segmentation/
├── yolov5_crowdhuman/
├── blur.py # 메인 실행 파일
└── requirements.txt
```

### 2. 처리 순서
1. `data/` 폴더 내 파일 입력
2. 번호판 비식별화 → `license/`에 저장
3. 얼굴 비식별화 → `output/`에 최종 저장

## 실행 방법

### 1. Conda 환경 설정
```bash
conda create -n blur_env python=3.11.5
conda activate blur_env
pip install -r requirements.txt
```

### 2. 기본 실행
bash
복사
편집
python blur.py
data/ 내 모든 파일을 처리하여 output/에 저장합니다.

### 3. 추가 옵션
| 옵션                 | 설명                       |
| ------------------ | ------------------------ |
| `--initial_source` | 입력 파일 경로 지정              |
| `--project`        | 결과 저장 폴더 지정              |
| `--name`           | 결과물 폴더 이름 지정 (`exp` 기본값) |
| `--exist-ok`       | 결과 폴더가 존재해도 덮어쓰기 허용      |
| `--person`         | 사람 전체 비식별화 옵션 활성화        |

#### 예시
```bash
python blur.py --initial_source ./custom_input --project ./results --name result_v2 --exist-ok
```

## 결과 예시
| 원본 영상              | 번호판 검출               | 얼굴 검출 후 최종 출력       |
| ------------------ | -------------------- | ------------------- |
| ![](src/input.png) | ![](src/license.png) | ![](src/output.png) |

## 참고 모델
YOLOv5 Crowdhuman
License Plate Segmentation

## 프로젝트 구조 요약
- `blur.py`: 메인 실행 로직
- `pytorch_licenseplate_segmentation/`: 번호판 세그멘테이션 모델
- `yolov5_crowdhuman/`: 얼굴 검출 모델
- `data/`, `license/`, `output/`: 입출력 디렉토리