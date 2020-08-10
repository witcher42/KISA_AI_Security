# 패킷 포렌식 - 악성코드 탐지 방법 및 체계구축 방법  
최경철 | 김찬중 | 김민수 | 김태완 | 황재성  
2020
📚📕📖
  
  
### 다운로드한 악성파일 분석
Follow▶TCP STREAM  
- file name, magic number 확인가능
  - magic number란? 파일의 실체를 알아볼수있는 시그니처(패턴)  
  
▶문자열 추출, 예제에서는 OFT2 메신저와 docx 문서로 구성  
▶docx의 매직넘버를 나타내는 문자열 PK의 16진수 값 검색하여 .docx 확장자임을 확인  
▶OFT2 블록의 recipe.docs가 추출대상  
▶save as RAW  
▶Hex editor로 파일 앞뒤에 OFT2 블록 제거  
|OFT2...|PK...|OFT2...|  
|:--:|:--:|:--:|  
  
▶악성파일 동적분석 가능  
### winodws 파일 시그니처  
- MZ..@...This program cannot be run in DOS mode  
- 확장자가 .exe 또는 .sys인 경우 매직넘버 4D 5A  
### C&C 서버 의심 
- 암호화된 문자열을 서버로 전송  
- 다수 도메인에 대한 많은 쿼리를 호출하는 사전작업이있다  
### 패킷 페이로드에서 img 탐지  
- alert TCP any any(content: "Content-Type|3A 20|image /";fast_pattern: only;http_header;file_Data;)
### 패킷 페이로드에서 MZ 탐지   
- alert TCP any any(content: "MZ";depth: 2;)
## Explorer Injector 작동원리 예시  
- 외부 IP주소를 확인하는 시도를 한다  
- 악의적인 실행 파일이 추출된다 (ex) PE32 악성파일, 드롭퍼
- explorer  및 원격프로세서 삽입을 시도한다
  - 바이너리가 원격프로세스 svchost.exe 실행후, 원격프로세스 explorer.exe 실행  
  -     binary.exe  
  -     ┗svchost.exe(PID:4004)  
  -      ┗explorer.exe(PID:1164)  
- 레지스트리 값을 수정하여 자동실행 기능을 설정한다
  - HKCU￦SOFTWARE￦MICROSOFT￦WINDOWS￦CurrentVersion￦RUN 에 자동실행 등록  
- 원격프로세스에 데이터를 삽입한다  
- 활성화 상태인 컴퓨터의 이름을 확인한다  
- 원격프로세스 cmd.exe를 실행하여 nslookup으로 DNS를 조회한다  
- 외부 6개의 도메인 및 3개의 호스트에 접속한다  
