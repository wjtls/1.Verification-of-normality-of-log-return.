# Verification-of-normality-of-log-return.
## 주가의 로그리턴이 정규분포를 따르는지 확인한다. 

- 도구

    [![파이썬 Badge](https://img.shields.io/badge/python-3776AB?style=flat-square&logo=python&logoColor=white&link=mailto:wjtls01@naver.com)](mailto:wjtls01@naver.com)

    [![파이토치 Badge](https://img.shields.io/badge/pytorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white&link=mailto:wjtls01@naver.com)](mailto:wjtls01@naver.com)

    [![주피터 Badge](https://img.shields.io/badge/jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white&link=mailto:wjtls01@naver.com)](mailto:wjtls01@naver.com)

- 목표: 주가의 로그리턴이 정규성을 따르는지 확인. (컴퓨터물리 강의 팀프로젝트)

- 구현 이유: 결과가 정규분포라면 정상성을 가지므로 주가를 예측하기가 상대적으로 수월 하지만 <br/>
          정규분포가 아니라면 트랜드의 영향을 예상보다 많이 받을것이다 이러한 결과는 향후 트레이딩 모델 구현에 참고할 수 있을것이다.
  
<br/><br/><br/><br/>


## 기능
  - csv 데이터 호출
  - 데이터의 log return 출력
  - 트랜드 제거(특정 구간별 선형 함수 피팅)
  - p-value 계산
  - 결과 시각화
  <br/><br/><br/><br/>


## 요약
  ![image](https://user-images.githubusercontent.com/60399060/146669544-09f4ef93-88ef-4c30-b04f-b1a489e292de.png)

   - 브라운 운동(액체나 기체속 미소입자들이 불규칙적으로 운동하는 현상) ,
      바슐리에 투기 이론(주가는 결과를 예측할 수 없는 외부 사건과 반복적 충격을 받아 무작위적으로 변동)에 따르면 
      주가는 무작위 운동을 하며 정규 분포 곡선을 이용하면 미래 주가를 예측할수 있다고 주장한다. 
      
   - 이후 모리 오즈번은 주가가 아닌 주가의 로그 수익률이 정규분포를 따른다는 주장을 했다. 
      이에 대해 현 프로젝트에서 주가의 로그수익률이 정규분포를 따르는지 검증한다.
      

  <br/><br/><br/><br/>


## 본론
  - 정규분포 
    많은 자연현상이나 사회현상의 확률분포는 정규분포와 유사한 형태를 지니고 있기 때문에, 자연과학이나 사회과학의 거의 모든 분야에서 정규분포가 쓰임
    정규분포(N)는 평균(μ)과 분산(σ^2)의 두개 모수를 가짐 :
    
  - 확률분포 
    가지고 있는 정보를 종합하여 수익률의 확률이 어떻게 분포되어 있는지를 알아내고 이를 분석하는 과정이 바로 투자의사결정의 요체
    미래의 상황에 따라 다른 값을 갖는 변수의 성질
    모수 (Paremeter): 확률분포의 형태를 결정짓는 통계량 
    => 모수의 값을 알면 확률분포의 그래프를 정확히 그릴 수 있음
    
  - 확률 밀도 함수(PDF:Probability density function)
    확률 변수의 분포를 나타내는 함수
    확률 밀도 함수 f(x)와 구간 [a,b]에 대해서 확률 변수 X가 구간에 포함될 확률 P(a≤X≤b)는 
    확률 밀도 함수f(x) 조건
    모든 실수값 x에 대해 f(x) ≥ 0
 

 - 주가의 로그 수익률이 정규분포를 따르는지 확인하기에 앞서, <br/>
   주가의 추세를 제거하여 데이터의 변동에 초점을 맞추기 위해 트랜드를 제거하는 Detrended procedure 를 거친다.
   이 과정을 거치면 데이터에 왜곡을 일으킨다고 여겨지는 부분을 제거할 수 있다.<br/><br/>
   
 - Detrended 과정<br/>
   ![image](https://user-images.githubusercontent.com/60399060/146667054-0d3b15d7-769d-41be-a7dd-6cf8975e8657.png)<br/>
   G(t)=주가의 로그 수익률
   
   ![image](https://user-images.githubusercontent.com/60399060/146667060-ba3256e8-5458-4590-8383-39c9b74821d4.png)<br/>
   트랜드 제거 과정을 거치기전 부분구간을 설정하고<br/>
   지수 트랜드(x'(t))를 구하기 위해 부분 구간별로 rolling 하여 선형함수 weight와 bias를 구하여 피팅시킨다.
   
   ![image](https://user-images.githubusercontent.com/60399060/146667083-78ab7987-69c7-4d53-b2d2-926ec5163d11.png)<br/>
   여기서 x*(t) = lnZ(t) - x'(t) 이고,<br/>
   Z(t) = 디트랜디드화 된 로그 수익률이다.
   
   
   
  <br/><br/><br/><br/>

 
## 결론 
  - ![image](https://user-images.githubusercontent.com/60399060/146708903-12865ba3-8c23-439a-8550-9e4ff7493344.png)
  -  QQ plot 은 정규분포의 이론적 분위수(해당값보다 작은 값을 나타냄) 와 표본 분위수를 나타내어 해당 분포가 얼마나 정규분포와 닮았는지 확인하는 방법이다. 이는 직선에 가까울 수록 정규성을 지닌다.
  -  p value는 관찰된 데이터의 검정통계량이 귀무가설을 지지하는 정도를 확률로 표현한 것이다.
     (귀무가설 : 관측값의 분포가 정규분포를 따른다)
    
  - 출력된 모든 분포는 p-value 값이 0.05 이하 였으며 QQ plot 에서도 선형성을 띄지않고 선에서 벗어나므로 정규분포가 아니다.

  - ![image](https://user-images.githubusercontent.com/60399060/146700305-be1873e9-520e-4b27-b0b5-ffc922227336.png)
  - 결과로 출력된 10분봉, 120분봉, 240분봉, 1일 데이터의 디트랜디드 로그리턴 분포는 <br/>
    fat tail(위와 같이 정규분포에 비해 꼬리 부분의 확률 밀도 함수가 높음, 붉은 그래프)특성이 있다.
  - fat tail 특성으로 인해 극빈 값들 (외부 영향으로 하한가 또는 상한가, 서브프라임 모기지, 코로나영향 등등) 의 빈도가 
    정규 분포보다 높기 때문에 예측이 힘들어 진다.
  
  <br/><br/><br/><br/><br/>
  

## 방안
  - 분석 결과 주가의 수익률은 fat tail을 가지는 분포이므로 평균에 근거한 예측을 할경우 틀릴 확률이 높다.
  - 따라서 블랙스완(fat tail risk)를 회피하기위한 전략을 사용 하거나
  - 트레이딩 모델 구현시 예측을 하되, 매 상황에 대한 대응을 중점적으로 학습시키는 방안이 있을 것이다.

