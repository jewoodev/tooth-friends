# :pushpin: Tooth-friends(치아프렌즈)
>치아 건강 관리 시스템 (개인 프로젝트)    

</br>

## 1. 제작 기간 & 참여 인원
- 2022.9.3 ~ 2022.12.25
- 개인 프로젝트

</br>

## 2. 사용 기술
  - Python
  - Yolo(v5)

</br>

## 3. 치아프렌즈는 무엇인가?
![image](https://github.com/jewoodev/tooth-friends/assets/105477856/58be4970-a28d-42d9-89a6-b7db2fe45cb1)

치아프렌즈라는 단어를 들으시면 어떤 이미지가 떠오르시나요? 치아친구? 가깝게 지내면서 도와준다는 건가? 떠올리던걸 멈추고 이젠 치아와 관련된 단어로 치과를 떠올려볼까요?

![image](https://github.com/jewoodev/tooth-friends/assets/105477856/b83380b4-be6f-41f5-a94e-4ab1d3c21485)

저는 어렸을 때 치과에서 괴로웠던 기억이 제일 많이 떠오르는데요, 치아치료도 그렇지만 치료 중에 계속 입을 벌리고 있어야해서 턱이 너무 고통스러웠었습니다. 치과하면 지금 떠올려도 고통스러운 이미지가 제일 큰거 같아요. 저뿐만 아니라 많은 분들이 그럴거라 생각합니다.

치아프렌즈는 그런 고통을 덜기 위해 빠르게 충치를 찾아내서 악화되는 것을 막아주는 친구입니다. 중요하지만 놓치기 쉬운 치아건강을 AI가 관리해주는 것이죠.

## 4. 시스템 설계
![image](https://github.com/jewoodev/tooth-friends/assets/105477856/5dfd2be1-cbe4-462a-b5de-a89754aa2fb8)
치아프렌즈의 시스템은 사용자 친화적입니다. 간단하게 입안에 넣기 쉬운 크기의 카메라로 치아들을 촬영하면 AI시스템이 분석해서 치아상태를 알려줍니다. 

![image](https://github.com/jewoodev/tooth-friends/assets/105477856/fc0d8ad3-3681-4785-8137-c0cfb21bf08c)

필요한 장치는 구강용 카메라와 노트북 뿐입니다. 이런 하드웨어를 사용하기 때문에 호기심이 왕성한 낮은 연령대의 사용자가 검사하는데에 재미를 느낄 수 있고 때문에 수시로 검사하는데에 거부감이 없어 높은 기대효과를 갖고 있습니다. 

## 4. 핵심 기능
치아프렌즈 시스템의 핵심 기능은 충치 진단입니다. 사용자는 그저 구강 카메라로 궁금한 치아를 촬영하면 시스템이 치아 상태를 알려줍니다. 정상, 일반 충치, 2차 충치(수복물 치료 치아)의 세가지 형태로 치아가 어떤지 알려줌으로써 쉽게 놓칠 수 있는 치아 건강을 케어할 수 있게 해줍니다.  



이처럼 2차 충치도 케어할 수 있기 때문에 넓은 사용자 폭을 갖습니다. 충치가 심각하다면 제거한 후에 치아를 수복해야하는 치료를 하게 되는데, 이런 치아에서 발생하는 2차 충치는 알아차리기가 어렵고 방치되다가 신경치료를 해야할 정도로 심각해지는 일이 많습니다. 치아프렌즈는 2차 충치 또한 검사가 가능해서 사용자가 2차 충치로 괴롭지 않도록 돕습니다.  
  
치아프렌즈는 실시간 치아 관리 서비스를 제공하기 위해 딥러닝 기술이 적용되어져 있습니다. 영상에서 객체를 탐색하고 설정된 목표물을 구별하여 치아의 상태를 알려줄 수 있도록 Object detection 기술을 사용합니다. 치아프렌즈의 기능을 구현하기 위해 사용된 모델, 학습된 데이터에 대한 내용은 아래 버튼을 누르시면 확인하실 수 있습니다.

<details>
<summary><b>핵심 기능 설명 펼치기</b></summary>
<div markdown="1">

### 4.1. Object Detection model
![Yolo](https://user-images.githubusercontent.com/105477856/204968803-86140472-ffe5-4950-a8b4-3e32b17a43f9.JPG)
치아프렌즈는 실시간 치아 관리를 하기 위해 Object detection을 할 수 있는 여러가지 모델 중에 FPS(Frame Per Seconds)와 mAP(Mean Average Precision)가 높은 Yolo(v5)를 사용했습니다.

![image](https://github.com/jewoodev/tooth-friends/assets/105477856/bb752c55-341b-48ba-a3f1-b36009ce6e2c)
>출처: 'yolo network design' 논문

이 모델은 하나의 CNN구조로 디자인되어 있는데 앞단은 컨볼루션 계층, 이어서 전결합 계층으로 구성되어 있습니다. 컨볼루션 계층은 이미지로부터 특징을 추출하고, 전결합 계층은 클래스 확률과 바운딩 박스의 좌표를 예측합니다. 욜로를 선택한 이유는 실시간 검출에 알맞기 때문입니다. 다른 모델들에 비해 빠른 속도를 자랑하기 때문인데요. 기존의 검출모델을 재정의해서 사용하고 있습니다. 기존의 검출 모델에서 대표적인 R-CNN은 이미지 안에서 바운딩 박스를 생성하기 위해 region proposal이라는 방법을 사용합니다. 그렇게 제안된 바운딩박스에 classifier를 적용해 분류하고 바운딩 박스를 조정하고, 중복된 검출을 제거하고, 객체에 따라 box의 점수를 재산정하기 위해 후처리를 합니다. 이런 과정을 복잡하게 거치기 때문에 R-CNN은 느립니다. 욜로는 객체 검출을 하나의 회귀 문제로 보고 절차를 개선시킨 모델입니다. 이미지 픽셀로부터 bounding box의 위치, 클래스 확률을 구하기까지의 일련의 절차를 하나의 회귀 문제로 재정의한 것입니다. 이런 시스템을 통해 어떤 물체인지와 물체의 위치를 하나의 파이프라인으로 빠르게 구해줍니다. 이미지를 한 번만 보면 객체를 검출할 수 있다고 해 이름이 유 온리 룩 원스 줄여서 욜로입니다.

Yolo는 시간을 거쳐 여러 버전으로 변화를 갖게 되는데 흔히 그렇듯 새로운 버전이 나올수록 성능이 향상됩니다. 저희가 사용한 것은 v5입니다. 그림 3을 보시면 Yolov5가 다른 객체 검출 모델들에 비해 FPS와 mAP가 높은 걸 확인하실 수 있습니다.


### 4.2. 데이터베이스
모델 학습에 사용된 데이터베이스는 자체 데이터베이스입니다.

자체 데이터베이스를 구축하기 위해 Python 환경에서 크롤링을 통해 데이터 마이닝을 한 후, 사용할 데이터를 선별하고 나서 라벨링 작업을 거쳤습니다. 

어떤걸 검출해야하고 어떻게 답을 내려야 하는지 알려주는 정답지와 같은 역할을 하는 것이 라벨링 데이터이기 때문에 정확하고 일관성있는 라벨링이 매우 중요했습니다. 

데이터양과 라벨링의 상태를 두고 저울질하며 모델링 작업을 이어가며 총 5번의 테스트 과정을 거쳐 데이터 수정 작업이 이루어졌습니다. 어떤걸 버리고 어떤걸 살려야할지, 정제하고 수정하는 동안 성능은 계속 개선되었습니다.

![image](https://github.com/jewoodev/tooth-friends/assets/105477856/eb1b3c86-9852-429b-b06f-1571aaa5b5bc)

작업이 마무리 된 데이터의 구성은 정상치아 208개, 충치 212개, 2차 충치 201개 총 621개입니다. 클래스는 fine, decay, secondary_decay 세가지 클래스의 annotation 값이 존재합니다. 

</details>

## 5. 모델 성능
<p align="center"><img src="https://github.com/jewoodev/tooth-friends/assets/105477856/da40efdb-40be-4e68-a0b1-ab79c4ec3d5a" width="100" height="100"/></p>

yolov5는 다양한 크기의 network 구성을 갖고 있어 상황에 맞는 선택이 가능합니다. 나노부터 스몰, 미디엄, 라지, 엑스라지 순으로 무거울수록 정확도가 높아지고 속도는 느려집니다. 저는 치아프렌즈에 알맞다고 판단된 s 모델을 선택했습니다.

위의 표는 Yolov5의 공식적인 성능표, 아래의 표는 치아프렌즈의 성능표로 위의 YOLOv5s의 mAP과 아래의 mAP을 비교하면 각 치아 검출의 성능이 어떤지 알 수 있습니다.  
![image](https://github.com/jewoodev/tooth-friends/assets/105477856/67d82d7e-737d-42c8-8b26-e927454728f6)

# 6. 실제 작동 화면
<p align="center"><img src="https://github.com/jewoodev/tooth-friends/assets/105477856/d29cc9ea-a5a8-4861-9a08-5abd038df93a" width="100" height="100"/></p>

<p align="center"><img src="https://github.com/jewoodev/tooth-friends/assets/105477856/60734e8c-c19e-4abf-8f17-1710bcf069d3" width="100" height="100"/></p>

<p align="center"><img src="https://github.com/jewoodev/tooth-friends/assets/105477856/9d9e0946-1b65-430b-9e9b-b465e664cb3d"/></p>