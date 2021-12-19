# Verification-of-normality-of-log-return.
## 주가의 로그리턴이 정규분포를 따르는지 확인한다. (컴퓨터물리 강의 팀프로젝트)
펫테일에 의해 feedback 루프 존재

- 도구

    [![파이썬 Badge](https://img.shields.io/badge/python-3776AB?style=flat-square&logo=python&logoColor=white&link=mailto:wjtls01@naver.com)](mailto:wjtls01@naver.com)

    [![파이토치 Badge](https://img.shields.io/badge/pytorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white&link=mailto:wjtls01@naver.com)](mailto:wjtls01@naver.com)

    [![주피터 Badge](https://img.shields.io/badge/jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white&link=mailto:wjtls01@naver.com)](mailto:wjtls01@naver.com)

- 목표: 주가의 로그리턴이 정규성을 따르는지 확인. 

- 구현 이유: 결과가 정규분포라면 정상성을 가지므로 주가를 예측하기가 상대적으로 수월 하지만 <br/>
          정규분포가 아니라면 트랜드의 영향을 예상보다 많이 받을것이다 이러한 결과는 향후 트레이딩 모델 구현에 참고할 수 있을것이다.
  
<br/><br/><br/><br/><br/>


## 기능
    - csv 데이터 호출
    - 데이터의 log return 출력
    - 트랜드 제거(특정 구간별 선형 함수 피팅)
    - p-value 계산
    - 결과 시각화
  <br/><br/><br/><br/><br/>


## 요약
  ![image](https://user-images.githubusercontent.com/60399060/146669544-09f4ef93-88ef-4c30-b04f-b1a489e292de.png)

    - 브라운 운동(액체나 기체속 미소입자들이 불규칙적으로 운동하는 현상) ,
      바슐리에 투기 이론(주가는 결과를 예측할 수 없는 외부 사건과 반복적 충격을 받아 무작위적으로 변동)에 따르면 
      주가는 무작위 운동을 하며 정규 분포 곡선을 이용하면 미래 주가를 예측할수 있다고 주장한다. 
      이후 모리 오즈번은 주가가 아닌 주가의 로그 수익률이 정규분포를 따른다는 주장을 했다. 
      이에 대해 현 프로젝트에서 주가의 로그수익률이 정규분포를 따르는지 검증한다.


  <br/><br/><br/><br/><br/>


## 본론

 - 주가의 로그 수익률이 정규분포를 따르는지 확인하기에 앞서, <br/>
   주가의 추세를 제거하여 데이터의 변동에 초점을 맞추기 위해 트랜드를 제거하는 Detrended procedure 를 거친다.
   이 과정을 거치면 데이터에 왜곡을 일으킨다고 여겨지는 부분을 제거할 수 있다.<br/><br/>
   
 - Detrended 과정
   ![image](https://user-images.githubusercontent.com/60399060/146667054-0d3b15d7-769d-41be-a7dd-6cf8975e8657.png)<br/>
   G(t)=주가의 로그 수익률
   
   ![image](https://user-images.githubusercontent.com/60399060/146667060-ba3256e8-5458-4590-8383-39c9b74821d4.png)<br/>
   트랜드 제거 과정을 거치기전 부분구간을 설정하고<br/>
   지수 트랜드(x'(t))를 구하기 위해 부분 구간별로 rolling 하여 선형함수 weight와 bias를 구하여 피팅시킨다.
   
   ![image](https://user-images.githubusercontent.com/60399060/146667083-78ab7987-69c7-4d53-b2d2-926ec5163d11.png)<br/>
   여기서 x*(t) = lnZ(t) - x'(t) 이고,<br/>
   Z(t) = 디트랜디드화 된 로그 수익률이다.
   
   
   
  <br/><br/><br/><br/><br/>

 
## 결론 

  <br/><br/><br/><br/><br/>
  
  
  
  

## 문제점 및 개선방안
