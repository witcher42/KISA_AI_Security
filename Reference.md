# 인공지능을 활용한 보안기술 개발 동향  
국경완 ‖ 국방통합데이터센터 실장  
공병철 ‖ 한국사이버감시단  
https://www.iitp.kr/kr/1/knowledge/periodicalViewA.it?searClassCode=B_ITA_01&masterCode=publication&identifier=1095  
- 머신러닝은 오버피팅 오류와 성향적 오류가 있어 보안전문가로서 완벽한 역할을 할 수 없다.  
- 이를 극복하기 위해서는 먼저 방대한 보안 데이터를 인간의 경험과 지식을 토대로 장기간 분석해 온 분야를 인공지능이 학습할 수 있도록 해야 하며  
- 이러한 선행 과정을 거친 후에야 날로 지능화되고 있는 보안 위협을 보다 효율적으로 빠르게 탐지하고 민첩하게 대응할 수 있을 것이다.  
  
# AI 보안관제 미션: 나쁜 놈은 신속하게, 이상한 놈은 정확하게 찾아라 – 2편  
신윤섭 ‖ 이글루시큐리티 인공지능개발팀장  
https://byline.network/2020/05/19-109/  
- 먼저 보안정보이벤트관리(SIEM), 침입방지시스템(IPS), 위협관리시스템(TMS), 웹애플리케이션방화벽(WAF) 등을 통해 수집한 이벤트 기반 정보 가운데 탐지 룰셋을 통해 식별·차단된 데이터를 샘플링하고 이벤트의 영향도·심각도를 기준으로 삼아 데이터에 레이블을 붙인다.  
- 다음은 레이블된 데이터에서 공격의 특징을 뽑아낸 피처(feature)를 추출할 차례다. 출발지 IP, 포트 등 단위 보안 장비에서 제공하는 기본 정보만으로는 AI 알고리즘이 의미 있는 분석을 하기 어렵기 때문에 피처를 선정하고 이에 맞게 데이터를 변환하는 과정을 거쳐야만 양질의 학습 데이터를 축적할 수 있다.  
- AI 알고리즘은 피처 추출을 통해 전처리된 데이터셋을 학습하는 과정을 기반으로 새로운 데이터를 판단하기 위한 기준을 스스로 만들게 된다.  
- AI 알고리즘이 만든 탐지 모델에 새로운 데이터를 주입해 나온 결과에 대한 피드백을 주는 과정을 반복함으로써, 탐지 모델의 정확성을 끌어올리게 된다.  
  
# <기계학습 개론> 실습
이현도 ‖ 서울대학교 Biointelligence Laboratory  
최원석 ‖ 서울대학교 Biointelligence Laboratory  
김윤성 ‖ 서울대학교 Biointelligence Laboratory  
https://bi.snu.ac.kr/Courses/ML2019/lab_slides/Lab1.pdf  
  
◼ Pytorch를 활용한 딥러닝 프로그램의 기본 구조  
- Model(nn.Module) : Class  
  - 전체적인 인공신경망의 구조를 선언하는 부분  
  - __init__, forward 등의 method는 꼭 필요함  
- Dataset : Class   
  - 학습에 필요한 데이터셋을 선언하는 부분  
  - __init__, __len__, __getitem__의 method는 꼭 필요함  
- Training   
  - 학습을 진행하는 부분  
- {Validation & Test}  
  - 학습된 결과를 확인하는 부분  
   
# ADVERSARIAL MACHINE LEARNING AT SCALE  
Alexey Kurakin ‖ Google Brain  
Ian J. Goodfellow ‖ OpenAI  
Samy Bengio ‖ Google Brain  
https://arxiv.org/pdf/1611.01236.pdf


  

