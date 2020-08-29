# UNB 2012 침입탐지 데이터셋 기반의 네트워크 비정상 행위 탐지  
서재현 ‖ 원광대학교   
💼📜  
  
. 실험 결과에서 k-NN 알고리즘이 가장 우수한 성능을 나타내었다. 
. 인공기술 중에 서 누적된 과거 데이터를 사용하여 새로운 공격을 찾는 분류 기술이 주로 사용된다. 데이터를 활 용한 공격 유형 분류를 위해서는 데이터 전처리, 학습 모델링 및 성능 최적화에 관한 통찰이 필요 하다. 침입탐지 연구를 위해 사용하기 적합한 데이터는 내부 자료로 사용되어 일반적인 연구자들 이 접하기 어려운 측면이 있다. 공개된 침입탐지 데이터셋은 현실과 동떨어진 경우가 많아서 기존 의 연과 성과를 실제 환경에 적용하기 어려운 경우가 많았다. 
. UNB 2012 데이터셋은 일자별로 공격 유형에 대한 데이터를 pcap 파일과 xml 파일로 제공한다. pcap 파일은 패킷 분석을 위한 용도로 제공되고, xml 파일은 각 연결마다 공격유형에 대한 레이블을 제공하여 비정상 행위 기반 탐지 연구에 사용하기 적절하 다. 
본 연구에서는 기계학습 알고리즘을 사용하여 학습 모델을 만들고 성능 측정을 한다. SVM(Support Vector Machine), k-NN(k Nearest Neighbor) 및 의사결정트리(decision tree) 알고리 즘을 사용한 성능 비교를 한다 
. 정상 데이터의 클래스 번호는 0으로 한다. 실험에 사용한 클래스는 정상, 내부자공격 (Infiltrating the network from inside), HTTP 서비스 거부 공격, IRC bonet을 사용한 분산 서비스 거부 공격과 Brute Force SSH 공격의 5가지이다. 

클래스 별 인스턴스 수 [Table 2] 

The number of instances according to class number 
0 Normal 2,002,747 
3 Infiltrating the network from inside 20,358 
4 HTTP Denial of Service 3,776 
5 Distributed Denial of Service using an IRC Botnet 37,460 
7 Brute Force SSH 5,219

데이터셋 분할은 StratifiedRemoveFolds 알고리즘을 사용하여 각 서브 데이터셋 간에 중복되는 인스턴스가 없도록 한다 [11, 12]. 클래스 불균형을 완화하기 위해 SpreadSubsample 알고리즘을 사 용하여 정상 클래스의 인스턴스 수를 가장 적은 수를 갖는 4번 클래스의 20배 정도로 조절한다  
SVM은 일반화 기능이 높은 편이나 학습을 할 때 학습 데이터의 부분 집합에만 의존하는 특성이 있어 인스턴스의 수가 적은 클래스 4의 분류 성능이 낮은 것으로 보인다. 
. 의사결정 트리는 SVM 보다 좋은 성능을 보이나 훈련 데이터에 지나치게 의존하는 경향을 보여서 자료 예측이 불안정할 때가 종종 있는 편이다. 
