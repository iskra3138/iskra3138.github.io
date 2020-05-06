**시계열** **데이터** **각각의** **관측값들은 random variable****의 realization****임**

CDF $P( X \le x) = F_x(x)$ 는 Random Variable X가 x보다 작거나 같을 확률

\-    RV가 2개면, CDF는 $P(X \le x, Y \le y) = F_{X,Y}(x,y)$  

CDF를 알면 Random Variable에 대한 확률적인 것을 다 안다고 할 수 있음. 이걸 알면 모든 정보를 안다고 보면 됨

CDF 를 미분하면 pdf를 구할 수 있음

 

**White Noise**

Noise는 시간에 따라 예측할 수 없는 factor

세가지를 만족하면 White Noise

1) 각각은 uncorrelated. 즉 covariance가 0  

   ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image006.png) for ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image008.png)

참고:두 Random Variable의 평균이 0일 경우, Cov[X, Y] = E[XY]가 되며, 두 변수가 linear하게 얼마나 연관되어 있는 지를 나타냄 (두 변수의 linear한 관계의 정도)

2) 평균은 0으로 모두 동일  à ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image010.png)

3) 분산은 모두 동일 à ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image012.png) (which is constant)

보통 ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image014.png) 라고 표현

 

**Stochastic Process** : 시간에 따른observation이 순서대로 있는 것

SP ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image016.png)

WN은 iid

보통 WN은 Gaussian white noise로 가정해서 시작

 

Correlation은 Covariance를 normalize 한 것으로 1차 선형관계 나타냄 ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image018.png)

Correlation은 ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image020.png)(로우) 라는 Greek 언어로 표현함. 범위는![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image022.png) 

**Stationary time series**

많은 시그널을 다 분석될 수 없으므로 stationary 시그널을가정해서 분석함

Stationary가 다른 시그널을 분석하는 기초자료, Tool이 됨 (아직은 안 와닿음)

 

Stationary하다는 말은 time series ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image024.png)의 joint distribution이 변하지 않는다.

**1) Strictly Stationary**

\- 시간간격을shift 시켜도 각 구간의CDF(joint distribution)가 같다면 stationary signal

For ![img](file:///C:\Users\YEONJE~1\AppData\Local\Temp\msohtmlclip1\01\clip_image026.png)

Stationary를 가정하고 AR, ARIMA, SARIMA등 다양한 모델을 개발

Strictly Stationary는 계산이 어려워서 weakly stationary고려

 

**Weakly stationary** 

1) E[x_t] 는 constant

2) 두 개에 대해서 shift한 cov가 동일

3) shift시켜도 분산 동일

 

** WN은 stationary인가?? (yes, weakly stationary)

일반적으로 stationary는 weakly stationary를 의미

 

**(weakly) stationary Xt**

Auto covariance function, gamma_x(h) = Cov(x_t, x_t+h) only dependent on h, not dependent on t.

h is called as ‘lag’

 

 

 

 $P(x)$ 

 

 $p(x)$ 





 $/latex$



 