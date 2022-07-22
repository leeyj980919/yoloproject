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
## 사용될 데이터
1. 헬멧 착용 사진
2. 헬멧 미착용 사진
3. 이어폰 착용한 귀 사진
4. 헤드폰 착용 사진<br>

## 데이터 수집 방법
![image](https://user-images.githubusercontent.com/100258615/180339274-494aaeef-5706-4408-8ba2-1c57447131fe.png)
1. 오픈소스로 공개된 데이터셋 사용
2. 구글 웹크롤링을 통해 다양한 데이터수집<br><br>
![1](https://user-images.githubusercontent.com/100258615/180339995-6f3611c0-f86a-4198-99c7-9849674a4fef.PNG)
3. 미흡한 부분, 직접 영상 촬영 후 프레임단위로 나눠 데이터셋화
![2](https://user-images.githubusercontent.com/100258615/180339999-4a7af902-1e1f-4143-97cb-16c28e877da9.PNG)
## 데이터 전처리
![1](https://user-images.githubusercontent.com/100258615/180347510-da253e80-7f10-4cbd-b49e-0ce5fd49e0d1.PNG)
![2](https://user-images.githubusercontent.com/100258615/180347512-2e19f8c6-ebd4-4051-aa85-56b6f7bf6d7a.PNG)
## 데이터 증식
* 데이터 Augmentation 진행
 * 좀 더 robust 한 성능을 위해 이미지 변형과 동시에 증강
 * Albumentations 라이브러리 이용
 * 해당 라이브러리 이용하면 이미지 변형과 동시에 라벨도 변형가능
![image](https://user-images.githubusercontent.com/100258615/180348041-d34b6584-b189-406e-ab2f-62deb5bb98de.png)
