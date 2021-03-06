# 군 폐쇄망 환경에서의 모의 네트워크 데이터셋 평가 방법 연구   
  
박 용 빈 ‖ 국방과학연구소  
신 성 욱 ‖ 국방과학연구소  
이 인 섭 ‖ 국방과학연구소   
💼📜  
  
### 악성코드를 grayscale 이미지로 변환한 후에 GAN 으로 학습시켜 악성코드를 증진하는 연구나, 이미지 분류 모델을 이용하여 분류하는 연구가 많이 진행되었다  
- 이미지의 픽셀 값은 [0,255]의 정수 값을 가져야 하는데 NIDS 데 이터 셋 값의 범위는 (-∞,∞)이다   
  - 그러므로 NIDS 데이터를 어떻게 [0,255]의 정수로 치환하고 이미지로 변환하느냐에 따라 정보량이 달라진다   
  - 이는 이미지 분류 모델 학습율에 영향을 미치게 된다   
- IS  
  - GAN으로부터 생성된 이미지의 품질을 평가하기 위한 Google에서 개발한 지표    
  - Google의 InceptionV3 모델에 증폭된 이미지를 예상하여 나오는 확률 벡터를 바탕으로 평가하는 방식      
- FID  
  - IS와 마찬가지로 생성된 이미지의 품질을 평가하고 GAN의 성능을 측정하기 위한 지표     
  - FID는 IS가 실제 이미지와 비교를 하지 않는 점을 보완     
  
- D feature 값 중 ‘protocol_type’, ‘services’, ‘flag’, ‘label’ 의 데이터 값은 숫자가 아닌 문자열로 표현된다   
- 이미지로 변환하기 위해 문자열 형식의 데이터 값 을 실수 형식의 데이터 값으로 변환해야한다  
- 그러므로 각 feature 별로 문자열 값을 0부터 정수 값으로 할당한 후, 일대일 대응으로 치환한다    
  
### 이미지의 픽셀 값은 [0, 255] 범위를 가지고 있으나, 수치형 데이터는 (-∞,∞)범위에 분포해있다   
- 이미지로 변환하기 위해서 수치형 데이터를 함수를 통해 (-∞,∞) → [0,255)로 매핑한다  ] 
- (-∞,∞)에서 유한한 범위로 축소시킬 수 있는 대표적인 함수는 atan와 tanh가 있다  
-     y = tanh(x/255)*255  
-     y = atan(x*Pi/510)*(510.Pi)  
  - __atan 보다 tanh 함수를 사용했을 때 정확도가 대개 3% 내외로 증가했다__    
  - 위 함수를 거친 값은 소수이므로 __이미지 변환을 위해 이러한 값들을 정수로 변환해야 한다__  
  - 소수점 이하의 수는 정수 값에 따라 비중이 다르기 때문에 __단순한 올림이나 내림, 반올림은 많은 정보량의 손실을 발생한다__   
    - 이를 해결하기 위해 정수 부분과, 소수점 이하의 수에 255를 곱한 정수 부분의 두 정수로 표현해 최대한 정보량의 손실을 줄이고자 하였다  
- 또한 머신러닝이 학습할 수 있는 이미지의 크기로 변환해야 한다  
  - 기존 이미지 분류 모델의 최소로 요구 하는 입력 이미지 크기는 32 * 32이다  
  - 첫 번째 과정을 거치면 41개의 feature 값과 소수 처리로 22개의 정수 값이 더 생겨나므로 총 픽셀로 변환할 수 있는 값은 63개이다  
  - 그 중 하나의 값을 255 패딩 값을 넣어 총 64개로 맞추어 8 * 8 의 이미지로 변환한다   
  - 이 이미지의 픽셀 하나 당 동일한 값의 4 * 4 로 확장해서 변환하면 32 * 32 로 입력 사이즈 크기를 동일하게 만들 수 있다     
  
- 모든 epoch마다 증진된 이미지에 대하여 총 60번의 1000 epoch 학습과 6000 (2*2*5*3*10*10) 번의 FID, IS 평가가 필요하다  
  - 이 모든 평가와 학습을 진행하기에는 시간적, 물리적 자원이 부족하다  
- 5개의 이미지 분류 모델마다 각각 3개씩 dense 레이어로 커스텀을 시킨 총 15개의 모델에 atan 전단사화 함수를 사용하고  
- 32 * 32 로 생성된 이미지를 1000epoch 까지 100epoch 단위로 데이터 학습을 시킨 후 저장한다  
- 그리고 각 15개의 학습된 모델을 100 epoch 마다 이미지로 변환된 NSL-KDD 시험 셋을 분류하는 정확도를 계산한 후,  
- 이미지 분류 모델 별로 가장 정확도가 높은 데이터 학습의 epoch 와 덴스 레이어 개수를 기준으로 선택한다   
- 다음으로 기준에서 전단사화 함수 혹은 이미지 변환하는 방법에 변화를 주어 FID, IS를 평가하고 대조한다   
- 그 결과, 최대 25번의 1000 epoch 학습과 150번의 FID, IS 평가가 필요했다   
  - 32 * 32 이미지 대신 8 * 8 이미지 를 사용하게 되면 IS에서는 큰 개선이 보인다   

 
