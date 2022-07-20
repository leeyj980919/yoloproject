# 연구계기
![1](https://user-images.githubusercontent.com/100258615/179919223-509a8e26-a5a3-469c-b0ac-158729aeec3a.PNG)
* 개인형 이동장치 헬멧 착용이 21.05.13 부터 시행 그러나 전동킥보드 이용자의 **97%가 헬멧 미착용**
* 공유 전기자전거는 방식에 따라 안전모 착용여부를 지정, 안전사각 지대에 있음<br><br>

![1](https://user-images.githubusercontent.com/100258615/179919586-d892dca5-55e4-429a-83cc-5da68e7ccdc4.PNG)
* 공유 전동 모빌리티 특징상 속도가 굉장히 빠름
* 자동차와 달리 사고발생 시, 충격을 온 몸으로 흡수: 최소한의 **헬멧착용의무** 필요성
* 현재 헬멧착용 단속중이나 한계가 있음<br><br>
*“공유 모빌리티에 하드웨어적 제어를 할 수 있게,
**실시간 헬멧 탐지 가능한 모델을 구축**하여
플랫폼에 도입 하는 것이 효율적이다”*
# 사용모델
![image](https://user-images.githubusercontent.com/100258615/179921236-b3974b29-e354-4075-9314-e2eac9d18f07.png)<br>
[YOLOv5 github](https://github.com/ultralytics/yolov5)
* 실시간 객체 탐지 알고리즘
  * YOLOv5 모델사용
* 사용이유
  * 이미지 전체를 학습하기 때문에 맥락학습 가능
  * 기존 객체탐지 알고리즘보다 높은 FPS와 높은 mAP -> **실시간객체탐지에 유리**
# 데이터수집 방법
사용될 데이터<br>
1. 헬멧 착용 사진
2. 헬멧 미착용 사진
3. 이어폰 착용한 귀 사진
4. 헤드폰 착용 사진

