# DeepFake_project
Deepfake technology for depressed patient  
딥페이크 기술을 이용한 비대면 코로나 블루 진단

## Necessity
- 대면 진료의 어려움
- 비대면 진료 시 환자들의 거부 반응

## Contributes
- 실시간 비대면 진료
- DeepLearning을 이용한 감정인식
- DeepFake을 이용한 얼굴 비식별화

## Detail of Function
- 얼굴 비식별화
 ```First Order Motion Model```을 사용하여 얼굴 데이터셋인 VoxCelebDataset을 사용하여 모델을 FineTuning 시킨다
- 표정인식
```Fer2013``` Dataset을 사용하여 총 7개의 감정을 분류    
모델은 CNN기반 모델을 사용하였다.

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
- 실행방법(cmd)
```
run_windows.bat
```

## 참고자료
- [real time deepfake code(github)](https://github.com/sugyeong-yu/avatarify-python)
- [image_to_deepfake_code(github)](https://github.com/alievk/first-order-model)
- [image_to_deepfake_code(colab)](https://colab.research.google.com/drive/1EwBV9XAmiXRFQ5WDa-k-sE4ZKRvDQU4j?usp=sharing)
- [youtube(deepfake_realtime)](https://www.youtube.com/watch?v=ItA_24srjyI&t=598s)
- [youtube(deepfake_image)](https://www.youtube.com/watch?v=sKDPunhmzkk)
- [youtube(model)](https://youtu.be/u-0cQ-grXBQ)
- [first-order-motion-model](https://rubikscode.net/2020/05/25/create-deepfakes-in-5-minutes-with-first-order-model-method/)
- [emotion detect model](https://github.com/petercunha/Emotion)
