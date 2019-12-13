# AI Explainability Whitepaper

## About This Whitepaper

이 whitepaper는 Google Cloud의 AI Explanations product와 함께 제공되는 technical reference입니다. ML 모델을 설계하고 delivery하는 모델 개발자와 데이터 사이언티시트들을 대상으로 합니다. 우리의 목표는 AI Explanations을 활용하여 모델 개발을 단순화하고 주요 이해 관계자에게 모델의 동작을 설명하는 것입니다.



~~제품 관리자, 비즈니스 리더, End User는 이 whitepaper의 일부, 특히 AI Explanations에 의해 사용되는 use case와 관련하여, 적절한 사용법과 현재 제한 사항에 대한 고려 사항을 고려할 수도 있습니다.~~ 

특별히, 우리는 이러한 독자들에게 "Usage Examples"및 "Attribution Limitations and Usage Considerations"섹션을 찾아볼 것을 제안합니다.



## Overview

### Evolution of Machine Learning

보다 정확한 AI를 만들기 위해, 데이터 세트 크기의 증가와 컴퓨팅 리소스의 가용성이 더욱 복잡한 비선형 모델이 AI의 중심이 되게 하였습니다. 

handcrafted rules, 휴리스틱부터 선형 모델, 의사 결정 트리, 앙상블 및 심층 모델까지, 가장 최근에는 메타 학습 또는 다른 모델들을 생성하는 모델까지 발전되고 있습니다.






이와 같은 좀 더 정확한 모델들은 여러 차원에서 패러다임 전환을 가져 왔습니다.

- **표현력(Expressiveness)**: 예측(forecasting), 순위(ranking), 자율 주행(autonomous driving), 입자 물리학(particle physics), 약물 발견(drug discovery) 등과 같은 점점 더 많은 도메인에서 다양한 기능 제공이 가능해짐
- **다양성(Versatility)**: 다양한 데이터 양식 (이미지, 오디오, 음성, 텍스트, 표, 시계열 등)에 적용될 뿐만 아니라, 공동 / 멀티 모달 애플리케이션이 가능해짐
- **적응성(Adaptability)**: Transfer and multi-task learning을 통해 small data 도 적용 가능
- **효율성(Efficiency)**: GPU, TPU와 같은 맞춤형 최적화 하드웨어를 통해 더 큰 모델을 더 빠르고 저렴하게 학습할 수 있음



반면에, 이러한 복잡한 모델들은 점점 해석이 어려워졌습니다. 이러한 모델들이 여전히 기본적으로 상관 관계 및 연관성을 기반으로 구축되었다는 사실로 인해, 몇 가지 문제가 발생합니다.

- **비논리적인 상관관계(Spurious correlations)**: 비논리적인 데이터 상관 관계 학습으로 일반화 능력이 저해되고 실제 결과가 좋지 않을 수 있음
- **디버깅 가능성 및 투명성 상실(Loss of debuggability and transparency)**: 모델을 수정하거나 개선하기도 어려울 뿐더러 신뢰도도 낮아짐. 특별히, 금융, 헬스케어 같은 규제 산업에서 이러한 불투명성을 모델 도입을 꺼리게 만드는 요소임
- **proxy objective**: 모델이 어플리케이션에 디플로이되어 작동할 때와 비교하여, 종종 proxy metric을 matching하는 것에서 오프라인에서 수행되는 방식들과 큰 차이가 발생할 수 있음 (주. Acc와 Loss의 차이인가?)
- **통제력 상실(Loss of control)**: 실무자가 문제 해결을 위한 능력치가 낮을 때 발생
- **바람직하지 않은 데이터 증폭(Undesirable data amplification)**: 우리의 사회적 규범과 원칙에 반하는 bias



이러한 챌린지들은 loop에서 사람들을 지키는 것과  [AI를 책임감있게 활용](https://ai.google/responsibilities/responsible-ai-practices/)하고 개발하할 수 있도록 하기 위해 explainability의 필요성을 강조합니다.







