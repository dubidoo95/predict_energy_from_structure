# predict_energy_from_structure

## 1. Introduction

분자의 3차원 구조를 바탕으로 해당 분자의 S1 energy와 T1 energy 간의 차이를 예측하는 모델입니다.

![image](https://user-images.githubusercontent.com/110075956/210160843-0a849a01-96a9-44b9-beb5-6ce2d40c6d52.png)

S1 energy란 전자가 singlet excited state에 있을 때의 energy이며, T1 energy란 전자가 triplet excited state에 있을 때의 energy를 뜻합니다. 이 정보는 현재 유기발광소재 OLED의 활성과 관련이 있고, 이 외에도 반도체나 디스플레이 분야 신소재 개발, 신약 개발 등 다양한 분야에서 핵심적인 역할을 할 수 있다고 합니다.

## 2. Data

데이터의 출처는 다음과 같습니다.

https://dacon.io/competitions/official/235789/overview/description

## 3. BluePrint

디렉토리 구조는 다음과 같습니다.

&nbsp;&nbsp;├ predict_energy_from_structure.ipynb<br>
&nbsp;&nbsp;└ data<br>
&nbsp;&nbsp;&nbsp;&nbsp;├ train.csv<br>
&nbsp;&nbsp;&nbsp;&nbsp;├ dev.csv<br>
&nbsp;&nbsp;&nbsp;&nbsp;├ test.csv<br>
&nbsp;&nbsp;&nbsp;&nbsp;├ train_sdf<br>
&nbsp;&nbsp;&nbsp;&nbsp;├ dev_sdf<br>
&nbsp;&nbsp;&nbsp;&nbsp;└ test_sdf<br>

## 4. Libraries

deep learning framework로는 pytorch 0.8.0 버전을 사용하였습니다.
RDKit을 이용하여 분자 구조를 3차원 형태의 이미지로 전환하여 CNN 모델에서 사용하였고 DeepChem을 이용하여 분자 구조를 토큰화하여 RNN 모델에서 사용하였습니다.

## 5. Models

모델 네트워크 구조는 다음과 같습니다.

![image](https://user-images.githubusercontent.com/110075956/210160942-9e74ca23-cbf0-47a1-ba5e-59368511e7f3.png)

RDKit으로 만든 분자 구조 이미지를 깊은 네트워크를 가지고 있어 세세하게 분류할 수 있는 ResNet 모델을 통해 하나의 feature로 바꾸었습니다. 이후 해당 feature와, DeepChem으로 만든 분자 구조 토큰을 LSTM 모델에 넣어 결과를 출력하였습니다.

## 6. Conclusions

![image](https://user-images.githubusercontent.com/110075956/210161203-132cac90-53a7-4d4a-8299-470aa58503e1.png)

총 20 epoch 동안 모델 학습을 진행하였고 Mean squared error를 이용해 학습 성능을 관찰하였습니다. train loss와 validation loss가 모두 우하향하는 모습을 보아 학습을 더 진행한다면 좀 더 나은 결과를 보여줄 것이라 생각합니다.
