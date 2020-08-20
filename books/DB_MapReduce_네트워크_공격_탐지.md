# MapReduce 환경에서 네트워크 공격 탐지를 위한 실시간 로그 분석 시스템 개발   
  
장진수 ‖ 전북대학교  
신재환 ‖ 전북대학교  
장재우 ‖ 전북대학교 
💼📜  
  
- 대규모의 네트 워크 트래픽이 발생함에 따라, 보안 로그의 처리 및 분석에 많은 시간이 소요된다  
- Hadoop의 MapReduce를 통해 보안 로그의 속성을 추출하고 대용량의 보안 로그를 분산 처리한다 
  - 처리된 보안 로그를 분석함으로써 실시간으로 발생하는 네트워크 공격 패턴을 탐지   
    -      패턴1 Port Scanning  
    -      패턴2 Host Scanning  
    -      패턴3 DDoS   
    -      패턴4 Worm  
    -      패턴5 Network Error    
  - 시각적으로 표현함으로써 사용자가 네트워크 상태를 보다 쉽게 파악할 수 있도록 한다  
    - 침입 탐지 시스템인 Snort를 이용하여 보안 로그를 수집  
    - 분석 시간을 단축시키기 위하여 MapReduce를 이용하여 수집된 보안 로그로부터 분석에 필요한 요소만 추출  

- Source IP, Destination IP, Destination Port를 추출하여 각각의 비율에 대한 RGB색을 이용하여 시각화  
  - 그러나 RGB색의 변화를 통해 네트워크 로그의 상태만을 시각화하여 보여주기 때문에 네트워크 공격을 사용자가 직접 판단해야 한다는 한계점이 존재   
  
### MapReduce 실시간 로그 분석 시스템  
- 로그 수집기는 다양한 속성의 네트워크 정보를 포함하고 있는 네트워크 로그를 실시간으로 수집하고 Log Storage인 HDFS에 삽입한다  
  - 침입 탐지 시스템인 Snort를 이용하여 해당 서버에 실시간으로 들어오는 네트워크 로그를 수집  
  - Time, type, Source IP, Port, Destination IP, Port, ID, Len 등   
  - 수집된 네트워크 로그는 Shell Script를 통해 n개의 데이터 노드에 분산되어 처리된다  
  - n개의 노드에서 처리된 결과는 HDFS에 저장된다  
- 로그 추출기는 HDFS에 저장되어 있는 로그에서 필요 요소만을 추출한 후 Hive에 저장한다  
  - 네트워크 로그 중 Time, Source IP, Destination IP, Destination Port 정보만을 추출  
  - Hadoop 기반의 MapReduce를 사용하여 추출요소 중 Time을 Key로 하고, 나머지 요소들을 Value로 하여 추출한다  
  - 추출된 각 요소인 Source IP, Destination IP, Destination Port값을 Count 요소 추출단계의 입력 데이터로 사용한다  
  - 추출된 요소 및 전체 로그의 양을 Key로 하고 각각의 Count 값을 Value로 하여 HDFS에 저장한다  
  - 추출 데이터 Hive 저장 단계에서 HDFS에 저장된 데이터 및 Count 값을 Hive에 테이블 형식으로 저장한다  
- 로그 분석기는 Hive에 저장되어 있는 데이터를 로드(Load)한 후 주요 공격 패턴 분석을 수행한다  
  - 서버를 기준으로 각각의 threshold 값을 설정  
- 분석 결과를 시각화하여 사용자에게 웹 인터페이스 형태로 제공한다  

