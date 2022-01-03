# Deepfake technology for depressed patient  
딥페이크 기술을 이용한 비대면 코로나 블루 진단

## Necessity
- 대면 진료의 어려움
- 제3자에게 얼굴 노출에 대한 거부감과 불편함
- 얼굴 정보 비식별화를 통해 얼굴 노출에 대한 불안감을 해소, 감정 분석을 통해 실시간으로 비대면 진료가 가능 

## Contributes
- 실시간 비대면 진료
- DeepLearning을 이용한 감정인식
- DeepFake을 이용한 얼굴 비식별화
## Result 
![image](https://user-images.githubusercontent.com/70633080/147924467-2a753856-aa2e-46ea-bf80-6794a726f9bd.png)\
![image](https://user-images.githubusercontent.com/70633080/147924472-e0734742-b00a-4939-a9d2-78b6f7cd0b6c.png)\
- 비대면 코로나블루 진단 프로그램 예시: (a) Happy (b) Surprising (c) Sad (d) Neutral
- 본인의 얼굴을 연예인얼굴로 대체함으로써 얼굴 노출의 부담감 감소, 개인정보보호 가능
- 표정 정보를 보존하고 딥러닝  감정 분석을 통해 코로나 블루 진단 보조

## Detail of Technique
### 1. Deep fake를 이용한 얼굴 비식별화
 ```First Order Motion Model```을 사용하여 얼굴 데이터셋인 VoxCelebDataset을 사용하여 모델을 FineTuning 시킨다.\
![mona](https://user-images.githubusercontent.com/70633080/147925725-a27e7538-7584-43bd-b196-b17f3c454c27.gif)
- 기존의 Deepfake : Autoencoder + GAN
- 한계: 기존 Deepfake는 추가정보를 필요로 한다는 것 ex) 머리움직임 매핑 > 얼굴 랜드마크 , 전신 움직임 > 포즈 추정
- **First Order Motion Model for Image Animation은 추가정보가 필요로 하지 않다는 것.**
 - 논문-https://arxiv.org/abs/2003.00196 
#### Image animation 이란?
- video sequence를 사용하여 원하는 motion과 object로 video sequence를 생성한다. 
- 전체 프로세스 : Motion 추출 / Motion video 생성
  - video object와 source object에 여러 지점을 표시(Key point)한 후 video object와 일치하도록 source의 해당 지점 근처에서 변환(로컬아핀변환)을 생성

#### Image animation을 위한 first order model
![image](https://user-images.githubusercontent.com/70633080/147919500-6ab1af0c-5392-4160-baba-2aaf4e44ff3b.png)
- Source(S): source image는 애니메이션을 적용하려는 이미지
- Drive frame(D) : Drive frame은 원하는 motion이 포함된 video object , 해당 motion을 source image에 포함하는 것이 목적
- Motion module: S와 D를 입력으로 받아 key point detect, 로컬아핀변환을 통해 **Dense optical flow와 Occlusion map을 생성**
   - Key point detector 
        - Key point : 이미지의 특징점, 보통 물체의 모서리나 코너 
        - Autoencoder를 이용하여 S와 D 모두에서 핵심 키 포인트를 예측하는 감지기 
   - 로컬아핀변환
        - 각 key point 뿐만아니라 주변에서의 motion을 수행할 수 있도록 변환. 
        - D에서 역방향 광학 흐름을 추정한다. 
        - Key point를 근사화하기위해 First order Taylor Series 확장을 사용한다.
        - Taylor Series : 어떤 미지의 함수 f(x)를 근사 다항함수로 표현하는 것 
- Generation module: Drive video sequence에서 제공되는 motion으로 source image를 렌더링한다. 
    - 생성 네트워크 : S를 왜곡하고 Occlusion mask를 이용해 source image에서 가려진 image 부분을 생성

   
### 2. 표정 분석을 통한 감정 인식
```Fer2013``` Dataset을 사용하여 총 7개의 감정을 분류\
![image](https://user-images.githubusercontent.com/70633080/147924377-6321b905-7a1b-4349-9fe8-7013c441f662.png)
- 논문: https://github.com/oarriaga/face_classification/blob/master/report.pdf
- 얼굴 인식 : ```haarcascade_frontalface_default.xml``` 사용
- 감정 인식: CNN 기반 모델 (논문 참고) 사용 ```emotion_model.hdf5``` \
![image](https://user-images.githubusercontent.com/70633080/147922923-c6be8db4-52fa-49e1-8f81-656837be6ec6.png)



## Code_inform
### 개별코드
- [Deepfake](https://github.com/ShrimpSnack/DeepFake_project/blob/main/code/Deepfake_face.ipynb)
  - 입력된 Video또는 image에서의 얼굴을 target image로 변환.
  - Google colab 환경에서 실행 or cuda toolkit & pytorch_gpu 설치 필요
  - ``` git clone https://github.com/alievk/first-order-model```
- [Emotion](https://github.com/ShrimpSnack/DeepFake_project/blob/main/code/Emotion.ipynb)
  - Real-time으로 얼굴표정으로 부터의 Emotion detection
### 통합코드
- [corona_blue](https://github.com/sugyeong-yu/DeepFake_project/tree/main/code/%5Bavatarify%5DCoronablue)
 - 기존 깃헙에 제공하던 deepfake 코드를 참고하여 감정인식기술을 추가
 - [기존깃헙](https://github.com/sugyeong-yu/avatarify-python) clone 후 afy dir의 code를 [[avatarify]Coronablue](https://github.com/sugyeong-yu/DeepFake_project/tree/main/code/%5Bavatarify%5DCoronablue)로 교체
 - 실시간으로 웹캠을 통해 frame을 받아와 얼굴 비식별화(deep fake)와 감정인식을 해줌
 - pytorch(cpu버전 사용시 딜레이발생가능), anaconda 외 모듈 설치필요
- 실행방법(cmd) ``` run_windows.bat ```

## 참고자료
- [real time deepfake code(github)](https://github.com/sugyeong-yu/avatarify-python)
- [image_to_deepfake_code(github)](https://github.com/alievk/first-order-model)
- [image_to_deepfake_code(colab)](https://colab.research.google.com/drive/1EwBV9XAmiXRFQ5WDa-k-sE4ZKRvDQU4j?usp=sharing)
- [youtube(deepfake_realtime)](https://www.youtube.com/watch?v=ItA_24srjyI&t=598s)
- [youtube(deepfake_image)](https://www.youtube.com/watch?v=sKDPunhmzkk)
- [youtube(model)](https://youtu.be/u-0cQ-grXBQ)
- [first-order-motion-model](https://rubikscode.net/2020/05/25/create-deepfakes-in-5-minutes-with-first-order-model-method/)
- [emotion detect model(github)](https://github.com/petercunha/Emotion)
