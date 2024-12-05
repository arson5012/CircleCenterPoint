# 원 중심점 찾기   
(Find the center point of the circle with RANSAC)

* #### 💡 개요
  * 이미지 크기(px)와 반지름(px)만을 알고있을 때  
    원의 중심점 좌표(px)를 반환하는 데모 프로그램
   
* #### 🌍 환경 & 호환성  
  * OS:	MS Windows 10 ~
  * Language : C++ 11 ~
  * Opencv version : 4.6.0 ~

* #### Ui (User interface) 설명
  ![image](https://github.com/user-attachments/assets/ee12a025-c515-4e91-9c97-9825b74836f2)

  #### TopLeft 부터 설명  
  * File Name : 이미지의 파일명을 표시  
  * Threshold : 이미지의 임계값을 수동으로 조정 할 수 있는 EditCtrl (기본 값은 THRESH_OTSU)  
  * LOAD 버튼 : 이미지를 불러와 Screen에 표시
  * ">" 버튼 :  Screen 그리기 도구 열기
  * Screen : 이미지 및 결과를 보여주는 Ctrl로 기본적으로 확대, 축소, 화면 이동등을 지원  
  * 결과 : 찾은 원의 중심점을 보여주는 그룹으로 X, Y 각각의 좌표를 표시  
  * 입력 : 찾고 싶은 원의 반지름을 px 단위로 입력하고 RANSAC의 반복 횟수를 설정  
  * RUN 버튼 : 원 중심점 찾기 Processing
  
  #### 그리기 도구 ( ">" 버튼을 눌러 나오는 그리기 도구 )  
  * LINE : 스크린에 시작점과 끝점을 클릭하여 라인 생성하며 시작점과 끝점 간 픽셀단위 거리를 표시  
  * VLINE : 스크린에 수평선을 그리고 수평선에 대응하는 수직선을 생성하며 시작점과 끝점 간 픽셀단위 거리를 표시  
  * MLINE : 버튼 위 EditCtrl의 숫자를 수정하여 몇 개의 연결되는 라인을 생성할지 정하고 LINE 과 동일한 방법으로 생성  
  * HLINE : 버튼 위 EditCtrl의 숫자를 수정하여 몇 개의 수직선을 생성할지 정하고 VLINE 과 동일한 방법으로 생성   
  * 3PT A : 3 점을 선택하고 각도를 표시  
  * 4PT A : 4 점을 선택하고 각 라인의 교점의 각도를 표시  
  * 3PT C : 3 점을 선택하고 3개의 점으로 원을 생성한 후 반지름을 표시  
  * 2PT C : 2 점을 선택하고 2개의 점으로 원을 생생한 후 반지름을 표시  
  * TEXT : 표시된 픽셀 단위 거리 및 각도, 반지름 등의 폰트 크기를 변경  
  
  #### 모든 그리기 공통 기능
  * Shift : 마우스 커서 위치에 따른 수직, 수평 고정 그리기  
  * Ctrl : 저장된 포인트 (Processing 이후)가 있을 경우 커서 위치 고정  


* #### 알고리즘 설명
  <img src="https://github.com/user-attachments/assets/07860e87-0ed5-405e-9da9-b43f30091d28" alt="블록도" height="180" width="580">   
  
  * LOAD 된 이미지에서 검은색이 더 많은지 반별하여 THRESH_BINARY 또는 THRESH_BINARY_INV 적용하여 이진화
  * 입력된 반지름으로 각 반지름 계산 후 외부 원부터 내부 원 순으로 각각의 포인트를 찾음
  * 각각의 포인트들에서 이상치 제거를 위해 포인트들 간 RANSAC 후 최종 결과 포인트 계산

---
