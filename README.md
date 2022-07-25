# 연구계기
![1](https://user-images.githubusercontent.com/100258615/179919223-509a8e26-a5a3-469c-b0ac-158729aeec3a.PNG)
* 개인형 이동장치 헬멧 착용이 21.05.13 부터 시행 그러나 전동킥보드 이용자의 **97%가 헬멧 미착용**
* 공유 전기자전거는 방식에 따라 안전모 착용여부를 지정, 안전사각 지대에 있음<br><br>

![1](https://user-images.githubusercontent.com/100258615/180337515-719f7f66-dc7c-4ee8-a8d9-34b80669563b.PNG)
* **음향기기**(이어폰, 헤드폰 등)착용 또한 외부소음이 차단되어 안전한 운행불가
* 서울시에서는 PM 기본수칙으로 이어폰과 같은 **음향기기 사용금지**를 공지한 바가 있음

![1](https://user-images.githubusercontent.com/100258615/179919586-d892dca5-55e4-429a-83cc-5da68e7ccdc4.PNG)
* 공유 전동 모빌리티 특징상 속도가 굉장히 빠름
* 자동차와 달리 사고발생 시, 충격을 온 몸으로 흡수: 최소한의 **헬멧착용의무** 필요성
* 현재 헬멧착용 단속중이나 한계가 있음<br><br>

*“실시간으로 **헬멧 착용 여부를 탐지**하고, 더 나아가 운행에 방해되는 요소인 **음향기기 탐지**하는 모델을 구축하여 플랫폼에 도입하는 것이 효율적”*
# 사용모델
![image](https://user-images.githubusercontent.com/100258615/179921236-b3974b29-e354-4075-9314-e2eac9d18f07.png)<br>
[YOLOv5 github](https://github.com/ultralytics/yolov5)
* 실시간 객체 탐지 알고리즘
  * YOLOv5 모델사용
* 사용이유
  * 이미지 전체를 학습하기 때문에 맥락학습 가능
  * 기존 객체탐지 알고리즘보다 높은 FPS와 높은 mAP -> **실시간객체탐지에 유리**
# 데이터
### [데이터 종류]
1. 헬멧 착용 사진
2. 헬멧 미착용 사진
3. 이어폰 착용한 귀 사진
4. 헤드폰 착용 사진<br>

### [데이터 수집 방법]
![image](https://user-images.githubusercontent.com/100258615/180339274-494aaeef-5706-4408-8ba2-1c57447131fe.png)
1. 오픈소스로 공개된 데이터셋 사용
2. 구글 웹크롤링을 통해 다양한 데이터수집<br><br>
![1](https://user-images.githubusercontent.com/100258615/180339995-6f3611c0-f86a-4198-99c7-9849674a4fef.PNG)
3. 미흡한 부분, 직접 영상 촬영 후 프레임단위로 나눠 데이터셋화
![2](https://user-images.githubusercontent.com/100258615/180339999-4a7af902-1e1f-4143-97cb-16c28e877da9.PNG)
### [데이터 전처리]
![1](https://user-images.githubusercontent.com/100258615/180347510-da253e80-7f10-4cbd-b49e-0ce5fd49e0d1.PNG)
![2](https://user-images.githubusercontent.com/100258615/180347512-2e19f8c6-ebd4-4051-aa85-56b6f7bf6d7a.PNG)
### [데이터 증식]
* 데이터 Augmentation 진행
 * 좀 더 robust 한 성능을 위해 이미지 변형과 동시에 증강
 * Albumentations 라이브러리 이용
 * 해당 라이브러리 이용하면 이미지 변형과 동시에 라벨도 변형가능
![image](https://user-images.githubusercontent.com/100258615/180348041-d34b6584-b189-406e-ab2f-62deb5bb98de.png)
### [최종 데이터셋]
![image](https://user-images.githubusercontent.com/100258615/180362545-aab28262-77ee-4e4a-8a26-872938f96ef8.png)
* 헬멧미착용: 2371
* 헬멧착용: 2497
* 이어폰 착용: 2109
* 헤드폰 착용: 2440

# 학습
* optimizer
  * SGD, Adam
* batch size
  * 64
* epochs
  * 1000 (early stopping 적용, patience: 100)  
* learning rate
  * 0.01
# 학습결과
* 가장 성능이 좋았던 모델은 SGD로 최적화한 모델
* early stopping으로 총 447 epoch 학습
* mAP@0.5 = 0.93
* mAP@0.5:0.95 = 0.82 

### [실제 시연(Adam 최적화)]
![earphoneFP](https://user-images.githubusercontent.com/100258615/180369154-da03fb20-6d19-40f5-b6b6-8f542bf87604.gif)<br>
* Adam으로 최적화한 모델은 **이어폰**에 대해 **오탐**이 큼 -> 실제 서비스 응용 시 오히려 **주행에 방해**가 됨
  * 귀의 음영만 보고 이어폰착용으로 탐지하는 경향
  * 이어폰은 **보수적으로 탐지**하는 것이 좋다고 판단
  
* 실험계획
  * bounding box 내부 작은 객체인 이어폰 탐지에 어려움을 겪음
    * Augmentation으로 인한 과도한 일반화로 이어폰 오탐이 증가하여 증강데이터 과감히 삭제
  * 좀 더 보수적인 탐지, 이어폰 착용 label에 대한 가중치 업데이트를 줄이기 위해 정면 착용사진 삭제
    
### [실제 시연(SGD 최적화)]
![earphone+helmet](https://user-images.githubusercontent.com/100258615/180366045-bf7647e7-624e-48e9-a291-333f54c41d4c.gif)
![headphone](https://user-images.githubusercontent.com/100258615/180366173-4e6eff2b-a059-4ab9-9d42-cd0cb861f27c.gif)
![nohelmet+earphone](https://user-images.githubusercontent.com/100258615/180366215-a9ccf198-fe6e-42f1-ba03-bdebebae9a29.gif)

* 4가지 Class:  헬멧 미착용, 헬멧 착용, 이어폰 착용, 헤드폰 착용 모두 탐지
* 제대로 착용하지 않으면 헬멧 미착용으로 탐지
* 좀 더 보수적인 이어폰 탐지성능
* bounding box가 겹치는 경우, FN가 높아지는 경향<br>
# 프로젝트 후기
* 모델링은 일반화와 상세화 사이, 의도에 맞는 한 지점으로 수렴해 나가는 과정
* 최대한 다양한 분산, 많은 양의 자료가 존재해야함
* label이 없는 자료가 많고, 양질의 Dataset 구축이 가장 오랜시간이 걸린다
* 때로는 SGD가 Adam보다 좋은 성능을 낸다
* 어떤 데이터를 쓰냐에 따라 성능이 달리 나오기 때문에 EDA 과정을 반드시 거치고, 다양한 데이터, 다양한 실험을 통해 결과를 비교분석 해야함
# 앞으로 계획
* 캡스톤 발표를 위해, 응용에 대한 타당성 부여
* 플랫폼(모바일 환경)에서 구동하는 것을 목표로 현재 모델경량화와 안드로이드app에 배포 시도 중.
