### 배치처리
- 느린 IO를 통해 읽는 횟수가 줄어든다  
- 큰 배열을 한꺼번에 계산하는 것이 분할된 작은 배열을 여러번 계산하는 것보다 빠르다   
  - range(0,10,batch_size==3) : 0, 3, 6, 9  
### 정확도 불연속 vs 손실함수 연속지표  
### Affine  
- 신경망의 순전파때 수행하는 행렬의 곱  
  - input --> Affine --> ReLU --> Affine --> ReLU  ...  Affine --> Softmax --> output  
### 최적화
- 확률경사하강법 SGD  
  - 지그재그 탐색은 본래의 최솟값과 다른 방향  
  - 무작정 기울어진 방향으로 진행하는 단점
- Momentum  
  - 운동량과 속도 도입  
  - 가중치 매개변수 업데이트  
- AdaGrad  
  - 학습을 진행하면서 학습률을 줄여나감  
  - Learning Rate항을 (기울기값의 제곱의 합들의 제곱근)으로 나누어줌  
  - 학습률 감소가 가중치 매개변수마다 다르게 적용됨  
  - 많이움직인, 크게 갱신된 매개변수는 학습률이 낮아짐  
- Adam  
  - Momentum + AdaGrad  
### 신경망 구현 규칙  
- 모든 계층은 forward()와 backward() 메서드를 가진다  
- 모든 계층은 인스턴스 변수인 params와 grads를 가진다  
- self.params[] = self.params + layer.params  
- 신경망의 성능을 나타내는 척도는 Loss(Cross Entropy Error)  
  -  매개변수에 대한 손실의 기울기를 얻어 매개변수를 갱신한다  
### 신경망 구현 순서
- class TwoLayerNet: init
- 가중치와 편향 초기화  
- 계층 생성  
  - self.layers = [Affine(W1,b1), Sigmoid, Affine(W2,b2)]  
  - self.loss_layer = SoftmaxWithLoss()  
- 모든 가중치와 기울기를 리스트에 모은다  
  - self.params, self.grads = [], []
- 메서드 생성
  - 추론을 
  
### 가중치 초기값을 모두 0으로 하면?
- 옳지 못한 방법으로 학습이 제대로 이루어지지 않음   
- 오차역전파법에서 모든 가중치가 똑같이 갱신되어 버림   
### 변수의 메모리 주소를 고정하기
- a = b 하면 b의 주소가 기억  
- a[...] = b 하면 a의 주소에 b값이 기억    

