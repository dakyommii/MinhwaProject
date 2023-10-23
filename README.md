# AI 기반 한국 전통 민화 데이터 생산 모델 연구
#### 동국대학교 영상문화콘텐츠연구원 (2021.10~)
개발인원: 2인 1조(개발 1, PM 1)<br>
#### Language 
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"> 

#### IDE
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white) 
![googlecolab](https://img.shields.io/badge/googlecolab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)

## 1. 한국 전통 민화 데이터 증강 솔루션 연구
기간: 2021.10~2022.12<br>
역할: 개발 전담
#### Framework
<img src="https://img.shields.io/badge/Pytorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white"> 

#### Library
![opencv](https://img.shields.io/badge/opencv-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white) 

#### DL Model
StyleGAN2-ada, AlexNet
#### datasets
꽃 민화 web crawling

### 소개
#### 이미지 생성형 AI 모델을 활용한 민화 데이터 증강 알고리즘
한국 전통 민화 데이터는 객체당 최대 100개 정도로 콘텐츠 AI 모델 학습에 활용하기에는 데이터가 부족합니다. 
생성형 AI 모델을 적은 데이터로 학습하면 생성된 이미지가 불분명하고 흐릿해지는 문제가 있었습니다.
이를 해결하기 위해, StyleGAN2-ada와 LPIPS 이미지 거리 계산 방법을 결합하여 새로운 데이터 증강 방법을 
개발하였습니다.

#### LPIPS 이미지 거리 계산법 도입
데이터 증강을 위해 StyleGAN2-ada 모델로 초기 학습을 진행한 후, 명확한 이미지만 선별하여 기존 데이터셋에 추가하는 과정을 반복하는 방식의 솔루션을 제안하였습니다. 이 방법을 활용해 충분한 데이터가 확보되고 GAN의 성능 평가 척도인 FID 값이 낮아질 때까지 반복하여 데이터를 증강하고자 하였습니다.
이미지의 품질을 정량적으로 평가하기 위해, AlexNet 기반의 perceptual loss 함수로 계산한 LPIPS 값을 기준으로 선정하였습니다. 여러 차례의 실험 결과, 고정적으로 명확한 이미지가 생성되는 비율을 파악하였고 그 결과, LPIPS의 표준 정규값 0.2% 이하를 이미지 선별 기준 비율로 정의하였습니다.

***
## 2. 한국 전통 민화를 자동 설명하기 위한 알고리즘 연구
기간: 2023.03~2023.10<br>
역할: 개발 전담
#### Framework
![Pytorch](https://img.shields.io/badge/Pytorch-EE4C2C?style=for-the-badge&logo=Pytorch&logoColor=white) 
![tensorflow](https://img.shields.io/badge/tensorflow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white) 

#### Library
![opencv](https://img.shields.io/badge/opencv-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white) 
![scikitlearn](https://img.shields.io/badge/scikitlearn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white) 

#### DL Model
YOLOv5, koGPT2
#### datasets (feat. Roboflow)
민화 설명문 작문 text, 민화 web crawlling

### 전체 flowchart

### 기능 상세
#### Step 1. YOLOv5 모델로 민화 속 객체 인식 
민화 속 객체를 인식하여 이름과 민화 내에서의 위치 정보를 추출하였습니다. 위치 정보를 활용해 객체 간 상하좌우 관계를 파악하였고 이를 민화 설명 데이터셋 구축에 활용하였습니다.

#### Step 2. 색상 분류 Sequential 모델로 객체의 색상 분류
색상 정보를 추가하여 민화 설명문의 표현을 풍부하게 하기 위해 HSV 값을 기준으로 13개의 색상으로 분류할 수 있는 Sequential 모델을 구축하였습니다. 
객체의 색상을 분류하기 위해 먼저, K-Means Clustering 방법을 활용해 객체 내에서 주요 색상을 추출하였습니다. 이후, RGB에서 HSV로 변환하여 색상 분류기를 통해 색상을 판별하였습니다.

색상 분류기 설계도

#### Step 3. 민화 설명문 자동 생성을 위한 koGPT2 fine-tuning
객체 명 레이블, 민화 장르, 객체의 위치 및 색상 정보를 바탕으로 작성된 민화 설명문을 각각의 레이블로 데이터셋을 구축하였습니다. 이를 기존 koGPT2 토크나이저에 추가하여 민화 객체 명이 입력되면, 이에 기반한 민화 설명문이 출력될 수 있도록 모델을 fine-tuning 하였습니다.

ko-GPT2 설계도


