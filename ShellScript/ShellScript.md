# 1. 쉘 스크립트
- Unix 나 Linux, POSIX를 지원하는 운영체제인 macOS등에서 일반적으로 사용하는 명령어들, if, for같은 프로그래밍적인 요소로 이루어진 인터프리터 기반 스크립트 언어이다.
- 본셸(/bin/sh), C셸(/bin/csh), TC셸(/bin/tcsh), 콘셸(/bin/ksh), bash셸(/bin/bash), Z셸(/bin/zsh) 등 다양한 셸 스크립트 언어가 존재한다.  
![image](https://user-images.githubusercontent.com/99636945/214742357-9078d5d4-eadd-4d75-9ad0-b6343c1a762a.png)
- 리눅스나 유닉스가 설치되어 있는 곳이라면 어디든 사용할 수 있다. 물리서버, 가상서버, 컨테이너 등 장소에 구애받지 않는다.
- 시스템을 사용하여 환경 설정, 앱 설치할 때, 매일 점검해야 하는 시스템 상태를 체크할 때, 여러 시스템에 동일한 작업을 해야할 때 등의 상황에 사용한다.
- 시스템, 데브옵스 엔지니어들이 주로 사용한다.

# 2. 기본 문법
- Linux 내부의 에디터를 사용해서 편집한다. 일반적으로 sh 확장자를 사용한다.
- 파일 내부에 시작 시 #!/bin/bash를 추가하여 bash셸 스크립트임을 명시해야 한다.
- 다음과 같은 예시 소스를 작성한다.  
![image](https://user-images.githubusercontent.com/99636945/214746507-cdc415bf-8fb9-46a7-a96a-fc49bd754a38.png)
- 실행하는 방법은 sh명령어, chmod로 권한 조정, 명령어와 함께 실행과 같이 3가지가 있다.
### 2-1. sh 명령어
- sh 명령어를 사용하여 쉘 스크립트를 실행할 수 있다.
- 사용 형식은 sh [실행하고자 하는 스크립트 파일명]이다.
### 2-2. chmod 명령어
- chmod 명령을 이용하여 파일에 실행 권한을 준 후(root 권한이 필요하다.) 
- 실행할 때에는 ./[스크립트 파일명]으로 파일을 호출하면 된다.
- ./는 상대경로를 작성할때 주로 사용하며, 현재 디렉토리 내부 이후의 내용들을 명시하면 된다.
### 2-3. 그 외 방법
- 쉘 스크립트는 다른 스크립트 언어와 다르게 명령어와 함께 프롬프트에서도 바로 실행할 수 있다는 특징이 있다.

# 3. 기본 문법 확장
### 3-1. 변수 사용하기
- 변수 타입을 선언하지 않고 [변수명 = 변수값] 형식으로 선언하면 된다.
- 쉘 스크립트에서 선언한 변수를 사용할때는 $변수명 또는 ${변수명}(시스템의 변수명 인식 용이성을 위함)을 사용한다.
- 예를 들어 language = "Korea English Japan"으로 변수 선언 후 mkdir $language라고 입력하면 디렉터리 3개가 생성되는 방식이다.
### 3-2. 변수의 종류
- 단순 선언 변수, 함수 내부에서만 사용하는 변수, 함수 밖에서도 사용이 가능한 변수 등이 있다.
- 그 외에 파라미터로 넘길 때 사용하는 변수를 예약변수 혹은 환경 변수라고 부른다.
- 쉘 스크립트에서 함수를 만들때는 function 함수명() { 내용 } 으로 정의한다.
- 함수 밖에서 선언하는 전역변수, 함수 내부에 선언하는 지역 변수(변수 앞에 local을 붙여줘야 한다.), 예약 변수 및 환경 변수등이 있다.
- 예약 변수 및 환경 변수의 종류는 다음과 같다.  
![image](https://user-images.githubusercontent.com/99636945/214755408-e0245fa7-5b49-4768-8182-cc8a9236bf27.png)
- 예약 변수나 환경 변수는 프롬프트에서 echo "$[환경변수명]"을 사용하여 값을 확인할 수 있다.
- 위치 매개변수를 포함한 특수 매개변수는 다음과 같다.  
![image](https://user-images.githubusercontent.com/99636945/214765456-5c5d1a83-1c85-4154-9fc0-7eb5ffb77c2c.png)
- 추가로 아래와 같은 것도 있다.(자주 쓰지 않는 것으로 추정됨)  
![image](https://user-images.githubusercontent.com/99636945/214768544-c15c6e86-140b-4fba-8119-e33027e3429c.png)
### 3-3. 변수 초기화 확장자
- 개발을 하다보면 특정함수를 호출하거나 쉘 스크립트를 실행할 때 함께 넘겨받는 파라미터에 의해 변수의 값을 초기화 하는 경우, 
변수가 선언된 위치에서 변수의 값을 설정해서 사용하는 경우가 많음.
- 쉘 스크립트는 변수 초기화를 위한 확장자를 지원한다.
- 아래 표에서 :는 Null 값을 의미하고, :-는 null이 아닌것, :=는 null인 것을 의미한다.
![image](https://user-images.githubusercontent.com/99636945/214769644-c9bf2db3-48c5-46fb-b032-8ddb20d5d3ca.png)
- +와 ?도 변수 초기화 확장자에서 사용할 수 있는 연산자이다.
![image](https://user-images.githubusercontent.com/99636945/214770111-f3802358-fd89-4d39-9cdb-829260d930dc.png)
- 또한 다른 프로그래밍 언어처럼 문자열 슬라이싱이 가능하다.(인덱스는 0부터 시작하며 Python과 방식이 유사한 편)  
![image](https://user-images.githubusercontent.com/99636945/214770198-50943703-2dae-4228-a1dc-50bb0d5c11d0.png)
### 3-4. 문자열 값 변경 확장자
- 변수의 값이 문자열일 경우 사용할 수 있는 확장자이며, 사용하면 값을 변경할 수 있다. 
- #은 전방 탐색을 의미하고, %는 후방 탐색을 의미한다.
![image](https://user-images.githubusercontent.com/99636945/214771581-b692464b-4885-4d9e-bbf2-2360a668bb32.png)
- 문자열의 길이를 알고싶을 땐 다음을 사용한다.  
![image](https://user-images.githubusercontent.com/99636945/214771775-c0e13d09-b574-4eba-a317-8ff8d44e527c.png)
- #과 %은 해당되는 부분을 완전히 지워버렸다면, /을 같이 사용하면 문자열을 교체하는 동작을 한다.(new가 비어있다면 역시나 문자열을 제거하는 동작을 한다.)
- //은 문자열 전체에서 패턴과 일치하는 문자열을 교환하는 동작을 한다.
![image](https://user-images.githubusercontent.com/99636945/214771927-0375c86c-6db9-4450-b8e2-f0b68b34d3d5.png)

# 4. 조건문
- 셀 스크립트 뿐만이 아니라 개발할 때 가장 많이 쓰이는 기본 문법 중 하나
- if는 정말 많이 사용되며, switch-case문도 사용할 수 있음
### 4-1. if문
- 다른 언어와는 형식이 좀 많이 다르다.(개인적으로는 기괴하다고 생각함)  
![image](https://user-images.githubusercontent.com/99636945/214772817-069c4f6b-8a8c-4ecc-b7ff-9191abf01056.png)
- if의 기본 형식은 위와 같고, if이후 elif를 사용하더라도 위의 형식과 똑같다.(if와 elif만 다름)
- 조건을 만족시키지 못해 아무것도 할 수 없을 경우, else문으로 진입하게 해줘야 한다.
![image](https://user-images.githubusercontent.com/99636945/214773040-3ef6dae5-a2bf-464e-ac2b-7fb6ef2999a5.png)
- 비교구문에 사용되는 형식은 다음과 같다.  
![image](https://user-images.githubusercontent.com/99636945/214773390-2d617f44-bc43-41fd-9a1a-0fbb596ec571.png)
![image](https://user-images.githubusercontent.com/99636945/214773464-5130884d-f6e9-47c1-9169-0aaf6bcd3c69.png)
- 그 외의 파일 관련 연산자가 존재한다.
- -L [파일이름]: 변수 유형이 파일이면서 심볼릭 링크이면 참
- -O [파일이름]: 변수 유형이 파일이거나 디렉터리
### 4-2. switch-case문
- 쉘 스크립트에서는 기괴하게도 case ~ esac 로 표현되는게 switch-case문이다.
- 기본 형태는 다음과 같다.  
![image](https://user-images.githubusercontent.com/99636945/214778527-43b15125-fa16-4e15-890c-8f3c7e361b0b.png)

# 5. 반복문
### 5-1. for문
- 리스트나 배열같이 다수의 값을 이용하여 동일한 작업을 처리할 경우에 주로 사용
- 쉘 스크립트에서는 두 가지 방법으로 이용할 수 있도록 제공된다.
- 첫 번째 방법은 파이썬처럼 in을 사용하여 리스트 및 배열, 특정 범위의 값들을 범위로 지정하여 반복을 수행하며 가장 많이 사용하는 방법이다.    
![image](https://user-images.githubusercontent.com/99636945/215002600-6c60cf70-10ee-413f-8a6d-8e2027728712.png)
- 두 번째 방법은 java 또는 C언어 처럼 초기값을 증가시켜 수행문을 계속 반복하는 방식이다.
- 아래 예제에서 괄호안에 아무것도 적지않으면 무한루프 반복문을 만들 수도 있다.  
![image](https://user-images.githubusercontent.com/99636945/215002778-92dbad48-7a24-4a52-bdbe-74eb496f3b4a.png)
- 쉘 스크립트는 문자 또는 배열의 원소를 띄어쓰기를 통해 구분하도록 한다.
- 사용 예제는 아래 몇 가지 사례를 통해 파악한다.  
![image](https://user-images.githubusercontent.com/99636945/215003091-daed40db-a984-4254-97dd-31aa12e02600.png)  
![image](https://user-images.githubusercontent.com/99636945/215003177-e7c7ff9d-9fef-48b3-bdcf-b46b549135cd.png)  
![image](https://user-images.githubusercontent.com/99636945/215003219-1fd8b459-2051-4871-886c-7a0f4c9cdea9.png)  
![image](https://user-images.githubusercontent.com/99636945/215003369-1db99b25-4776-4ea8-9323-56c83fa48242.png)  
![image](https://user-images.githubusercontent.com/99636945/215004040-eb27e050-78b7-41de-af4c-985065b26d6f.png)
### 5-2. while문
- 조건식을 바로 사용하고 조건에 맞을 때 까지 계속 반복함
- 기본 형식은 다음과 같다.  
![image](https://user-images.githubusercontent.com/99636945/215004520-16549a6f-cfe3-491c-99cb-489b132290f0.png)
- 조건, 반복문에서 사용할 수 있는 디테일한 조건 및 비교 연산자들은 다음과 같다.  
![image](https://user-images.githubusercontent.com/99636945/215004780-77065451-d9fe-4aa6-8780-c3bd2af329ad.png)
- 비교 연산자들 중에서도 >, >=같은 기호 연산자를 사용할 수 있는데, 그럴때는 if (( $변수1 >= $변수2 )) 처럼 중첩소괄호를 사용해야 한다.

# 6. 연산자
- 위에서 언급된 여러 연산자들을 제외하고, 문자 비교 연산자, 논리 연산자 등이 있다.
- 문자열 비교 연산자는 문자형 연산자가 아닌 기호 연산자를 사용하고 중첩 대괄호를 사용해주면 된다.(리눅스의 리다이렉션 기호와 헷갈리지 않도록 시스템에 명시하기 위함)  
![image](https://user-images.githubusercontent.com/99636945/215019117-0884102b-3408-46ec-8f75-0e81b404d55c.png)
- 논리 연산자는 프로그래밍 언어와 비슷한 형태를 띄며 다음과 같이 사용한다.  
![image](https://user-images.githubusercontent.com/99636945/215021064-845c1391-0e6c-47c6-a1d7-0407373a2ba1.png)

# 7. 정규 표현식
- 리눅스나 유닉스에 특별한 특징을 부여하는 문자들과 메타 문자들의 집합
- 텍스트 탐색, 문자열 조작에 쓰이고 하나의 문자와 일치하거나 혹은 문자열의 일부분이나 전체 문자열 중 특정 문자 집합을 표현할 때 사용된다.
### 7-1. POSIX
- 정규 표현식은 일치하는 텍스트를 찾기 위한 패턴을 표현하기 위해 사용되는 특정 표준 텍스트의 문법을 의미함.
- 패턴을 기술하는 문자열 내의 각 문자들은 메타문자나 정규 문자로 이해된다. 메타문자의 종류들은 다음과 같다.  
![image](https://user-images.githubusercontent.com/99636945/215024580-b28f454e-b5c7-4faf-af62-d8db56f7ebe9.png)  
![image](https://user-images.githubusercontent.com/99636945/215024669-a8b81a14-200f-486a-a76c-8d61d222e5ca.png)  
![image](https://user-images.githubusercontent.com/99636945/215024767-f955631b-a510-4c17-bf13-efdcdb2c81c5.png)
- 메타문자 외에도 POSIX(이식 가능 운영체제 인터페이스)로 정의된 문자 클래스를 정규 표현식에서 사용하기도 한다.
- POSIX란 서로 다른 UNIX OS의 공통 API를 정리하여 이식성 높은 유닉스 응용 프로그램을 개발하기 위한 목적으로 IEEE가 책정한 애플리케이션 인터페이스 규격이다.
- POSIX 규격에선 다음과 같은 문자 클래스를 지원하며 알파벳 대소문자, 숫자, 특수문자가 있다.  
![image](https://user-images.githubusercontent.com/99636945/215025191-124d1b3d-4cfe-4623-b90b-6586b7ab9ba3.png)
- POSIX 사용 예시는 grep 'X[[:upper]][[:digit]]' list.txt 같이 사용하여 list.txt 내부의 X로 시작하는 대소문자, 숫자를 모두 찾는 행위를 할 수 있다.















