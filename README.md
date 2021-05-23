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
- [Deepfake](https://github.com/ShrimpSnack/DeepFake_project/blob/main/code/Deepfake_face.ipynb)
  - 입력된 Video에서의 얼굴을 target image로 변환.
  - Google colab 환경에서 실행 or cuda toolkit & pytorch_gpu 설치 필요
- [Emotion](https://github.com/ShrimpSnack/DeepFake_project/blob/main/code/Emotion.ipynb)
  - Real-time으로 얼굴표정으로 부터의 Emotion detection

