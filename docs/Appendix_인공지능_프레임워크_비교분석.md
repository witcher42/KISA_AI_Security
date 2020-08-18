# 성능을 생각한다면 텐서플로우 설치는 pip가 아닌 conda로
https://antilibrary.org/2378  
![](https://www.anaconda.com/wp-content/uploads/2019/12/TensorFlowTraining.png)

- conda 설치시 pip와 비교하여 최대 8배의 성능을 보인다   
- 텐서플로우 패키지 속도를 향상시켜주는 것 이외에도 sklearn, numpy 등 주요 라이브러리의 속도 향상에도 효과가 있따  

# 사이킷런(Scikit-learn) vs 텐서플로우(TensorFlow)  
http://blog.naver.com/las1001/221720815533   

- 사이킷런 장점
  - 잘 정의된 탄탄한 학습 알고리즘  
- 사이킷런 단점
  - 딥러닝이나 강화학습을 다루지 않음  
  - GPU를 지원하지 않음  
- 텐서플로우
  - 하드웨어가 좋을때 탁월한 성능  
  - 딥러닝에서 많이 사용하는 다양한 모델과 알고리즘이 들어 있음
  - 결과를 설명하는 데이터 플로우 그래프 DFG를 표시하고 이해하기 좋음  
  
# 딥러닝 프레임워크 비교 분석 PyTorch vs Keras vs TensorFlow  
https://blog.naver.com/rlaghlfh/221494731829  

- Keras 
  - TF에 얹어서 사용하는 라이브러리  
  - PyTorch에는 못얹음 
  - 간결하며 가독성이 좋음 
  - 디버깅 강점  
- TensorFlow
  - 업계 1위
  - Google Brain 발
  - 미래가 어두움  
  - 구식 느림  
  - 장황함(verbose)  
  - 디버깅이 어려움  
- PyTorch
  - 학계 1위
  - Facebook AI Research 발
  - 편리성 때문에 잠재적인 1위
  - 빠르고 에러적음    
  - 매우 잘 짜여져있어 코드가 간결해짐
  - 프로토타이핑이 쉬움  
  - 단점
    - 알파고 못돌림ㅋㅋㅋ
