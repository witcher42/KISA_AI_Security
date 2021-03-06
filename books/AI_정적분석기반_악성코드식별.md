# 정적 분석 기반 기계학습 기법을 활용한 악성코드 식별 시스템 연구  
김수정 ‖ 호서대학교  
하지희 ‖ 호서대학교  
오수현 ‖ 호서대학교  
이태진 ‖ 호서대학교  
💼📜  
  
- 시그니처 기반 탐지의 대응만으로는 악성코드 탐지에 한계가 존재  
- 또한, 난독화, 패킹, Anti-VM 기법의 적용으로 분석 성능이 저하   
  - 유사성 해시 기반의 패턴 탐지 기술과 패킹에 따른 파일 분류 후의 정적 분석 적용으로 기계학습 기반 악성코드 식별이 가능한 시스템을 제안  
  - 악성코드의 식별에 강한 패턴 기반 탐지와 신규 및 변종 악성코드 탐지에 유리한 기계학습 기반 식별 기술을 모두 활용하여 보다 효율적인 탐지가 가능함   
  
## 유사한 파일이 유사한 해시값을 가지게 하는 해시 기법   
- 해시된 데이터를 유클리드 거리 측정법과 같은 유사도 값을 도출하여 파일의 유사한 정도를 비교하는 방식  
- 도출된 유사도 값을 비교하여 어느정도 유사한지 판단할 수 있으며, 적정 threshold를 지정하여 악성코드의 탐지가 가능   
- `유사성 해시를 이용한 악성코드 탐지는 유사한 파일을 찾기 위해 사전에 분석한 데이터를 기반으로 유사도를 분석하기 때문에 신규 악성코드 발생 시 탐지에 어려움을 겪게된다` 
- 기계학습 기법의 supervised learning 방식을 이용하면 기존에 보유한 데이터의 특성을 나타내는 feature를 이용하여 모델링을 할 수 있다  
- 이때, 기존 데이터의 label이 주어진 상태로 학습하기 때문에 새로운 데이터의 결과는 학습된 label 중 하나로 나타나게 된다
- 새로운 데이터가 접근하면 학습된 모델을 이용하여 기존 데이터의 악성코드와 유사한 신규·변종 악성코드의 탐지가 가능하다  
  - 유사성 해시 알고리즘을 사용한 악성코드 분석방법은 기존에 준비한 학습데이터와 다른 유형의 데이터일 경우 판단할 수 없다
    - 유사도 값은 설정한 threshold를 악성 판단에 사용
  
1. 학습데이터의 feature를 추출 및 가공 후 유사성 해시 알고리즘으로 해시값을 추출하여 저장한다  
1. supervised learning 기법인 기계학습 알고리즘의 training을 통해 모델을 생성한다    
1. 다음으로 테스트데이터가 입력되면 학습데이터와 동일한 방법으로 feature를 추출 및 가공하고 유사성 해시 알고리즘과 기계학습 알고리즘으로 악성코드를 탐지한다  
1. 유사성 해시 알고리즘마다 판단 가능한 유사도 값에 대한 threshold를 지정하고 악성코드, 정상파일, 탐지 불가로 판단한다  
1. 탐지가 불가능한 데이터를 대상으로 기계학습 알고리즘을 ensemble한 결과를 도출한다   

- 파일이 입력되면 롤링 해시를 사용하여 해시한 후 생성된 해시값들을 연결한다  
  - __롤링 해시는 파일을 슬라이딩 윈도우 방식으로 해시한다__
  - `슬라이딩 윈도우 방식은 일정한 윈도우의 크기를 유지한 채 바이트씩 이동하며 읽기 때문에 파일의 시작 부분에 문자열이 삽입되더라도 전체 해시 결과가 변경되지 않아 기존 해시방식의 취약점을 보완함`     
- 이렇게 생성된 해시는 공통된 내용을 가진 파일에서 어느 정도의 유사성을 나타낼 수 있다  
- 동일하거나 매우 유사한 파일은 100의 유사도를 가지게 되고 유사하지 않을수록 0과 가깝다

## PE(Portable Executable) 파일 포맷  
- windows 운영체제에서 정의한 포맷으로 실행파일, DLL, 오브젝트 등을 위한 파일 형식  
  - PE 파일에서 실행에 필요한 정보는 PE 구조의 헤더와 섹션에 존재  
  - 실행 코드에 대한 정보는 모두 섹션 영역에 존재  
  - 섹션명에 따라 담고 있는 내용이 다르므로 섹션명에 기반한 특징도 파악이 가능  
- PE 파일에 import된 DLL, API 정보는 악성 행위의 특징을 가지고 있으며, 섹션명, entropy는 파일에 적용된 난독화 기술에 대해 규칙성을 가지고 있다  
- 파일 전체에서 추출한 DLL, API 목록 entropy 값은 파일의 섹션마다 존재하여 0~8 사이의 값으로 복잡도 및 무질서한 정도를 나타낸다  
  - entropy를 이용하면 파일이 패킹으로 인해 압축이나 암호화되어있는지 알 수 있다
- 패킹기법은 파일을 압축하는 기법으로 파일의 용량을 줄이고, 데이터의분석을 어렵게 만든다  
- 패킹기법이 적용되지 않은 PE 파일은 중간의 코드 영역을 제외하고는 대부분 0x00 바이트로 이루어지기 때문에 높지 않은 수치의 entropy를 가지게 된다  
- 패킹기법이 적용된 파일의 섹션은 원래 코드가 다른 코드로 대체되어 변경되며, 예를 들어 UPX 패커 사용 시 패킹된 바이너리의 기본 헤더는 변경되지 않았으나 섹션은 UPX0,
UPX1, UPX2로 변경되고, ASPack 패커 사용 시 기존 섹션들은 그대로 존재하지만 .aspack 섹션과 .adata 섹션이 추가된다  
- 섹션명의 규칙적인 변경에 따라 변화하는 entropy 값을 이용하여 악성코드와 정상파일 사이의 섹션별 entropy의 경향성을 가진 유의미한 feature를 추출하기 위해 feature 해시 기법을 적용하였다  
- entropy의 경우 섹션별 entropy 값이 의미가 있는 것이기 때문에 entropy 값과 섹션명을 각각 16개의 feature로 가공하여 16 * 16으로 총 256개를 feature를 생성하였다  
  

  
  
