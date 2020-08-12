### 배치처리
- 느린 IO를 통해 읽는 횟수가 줄어든다  
- 큰 배열을 한꺼번에 계산하는 것이 분할된 작은 배열을 여러번 계산하는 것보다 빠르다   
  - range(0,10,batch_size==3) : 0, 3, 6, 9  
### 정확도 불연속 vs 손실함수 연속지표  
### Affine  
- 신경망의 순전파때 수행하는 행렬의 곱  
  - input --> Affine --> ReLU --> Affine --> ReLU  ...  Affine --> Softmax --> output  
### 오차 역전파
- 
