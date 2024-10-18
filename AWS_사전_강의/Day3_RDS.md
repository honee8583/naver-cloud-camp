# 네이버 클라우드 캠프 AWS 사전 강의 - 3일차
| 10/17(목) 네이버 클라우드 캠프 AWS 사전강의 학습 내용
<br/>

## RDS

아마존 웹 서비스(AWS)에서 제공하는 관리형 관계형 데이터베이스 서비스이다. RDS는 사용자가 직접 데이터베이스 서버를 설치, 관리, 유지보수하는 번거로움 없이 쉽고 효율적으로 관계형 데이터베이스를 설정, 운영할 수 있도록 해준다. AWS가 백그라운드에서 데이터베이스의 유지보수를 자동으로 처리해주기 때문에, 사용자들은 애플리케이션 개발에 집중할 수 있다.

### RDS 생성
먼저 RDS를 생성해본다.

<img width="840" alt="스크린샷 2024-10-17 오후 4 06 34" src="https://github.com/user-attachments/assets/e150ddf1-d31e-4665-b366-ec31ebda33c3">

‘표준생성’을 선택하고 MySQL 엔진 선택

<br/>

<img width="850" alt="스크린샷 2024-10-17 오후 4 09 44" src="https://github.com/user-attachments/assets/ef2ac833-5626-403e-81d0-41a0e1e4ab8a">

무료로 사용하기 위해 ‘프리티어’ 선택

<br/>

<img width="841" alt="스크린샷 2024-10-17 오후 4 10 08" src="https://github.com/user-attachments/assets/db865935-e6ae-44dd-8ab9-979d28c263ab">

DB 인스턴스 식별자를 지정하고 데이터베이스의 아이디와 비밀번호를 설정해준다.

<br/>

<img width="835" alt="스크린샷 2024-10-17 오후 4 15 50" src="https://github.com/user-attachments/assets/82885702-245c-4e5a-9e48-3bcce34a28e8">

스토리지 유형으로 gp2를 선택

<br/>

<img width="853" alt="스크린샷 2024-10-17 오후 4 11 27" src="https://github.com/user-attachments/assets/6eba8556-8174-427a-b02f-812dbe380986">

로컬에서 RDS로 접근하게 위해 퍼블릭 액세스를 ‘예’로 선택

<br/>

<img width="1484" alt="RDS" src="https://github.com/user-attachments/assets/d837af5f-490b-4f13-8d95-ca1dd4eb28fd">

RDS의 생성이 완료되면 RDS로 접근할 수 있는 엔드포인트를 제공해준다. 우리는 이 엔드포인트를 Mysql Workbench, DataGrip, Beaver등에서 접속해볼 수 있다. (퍼블릭 액세스 설정을 ‘예’로 해주었기 때문에) 

<br/>

접속하기 전에 EC2처럼 인바운드 규칙을 편집해 외부 접속을 허용해줘야 한다. 보안그룹으로 들어간다.

<img width="2469" alt="스크린샷 2024-10-17 오후 4 21 51" src="https://github.com/user-attachments/assets/a48c1311-36de-4b63-a6e7-b93c9d68c93a">

모든 트래픽으로 모든 IP에서의 접속을 허용시켰다. 이제 로컬에서 접속이 가능하다.

<br/>

<img width="870" alt="스크린샷 2024-10-17 오후 4 24 27" src="https://github.com/user-attachments/assets/3ba31ff0-6227-4d18-b88a-96d12dc02aba">

DataGrip에서 접속을 시도해본다. Host에는 RDS의 엔드포인트를, User, Password에는 RDS를 생성할 때 설정한 아이디와 비밀번호를 입력하고 ‘Test Connection’을 선택해 접속이 되는지 테스트해본다. Succeeded가 뜬다면 접속이 가능하다는 뜻으로 성공이다.

<br/>

### RDS 스냅샷으로 복구하기

RDS를 생성하고 데이터베이스를 생성해보자. 만약 이 상태를 다음에도 사용할 수 있게 백업같은 것을 해두고 싶다면 ‘스냅샷’을 생성할 수 있다.

<br/>

<img width="661" alt="스크린샷 2024-10-17 오후 4 25 45" src="https://github.com/user-attachments/assets/f84d34b5-1571-4d8e-80b8-92636616891c">

스냅샷을 생성하고 싶은 RDS를 선택하고 작업에서 ‘스냅샷 생성’을 선택한다. 현재 RDS에 작업했던 내용 그대로 스냅샷이 생성된다.

<br/>

<img width="843" alt="스크린샷 2024-10-17 오후 4 26 03" src="https://github.com/user-attachments/assets/395ddb5a-ab27-4093-8a04-b78d0e7ae712">

스냅샷의 이름을 설정하고 ‘스냅샷 생성’을 선택

<br/>

<img width="2212" alt="스크린샷 2024-10-17 오후 4 31 20" src="https://github.com/user-attachments/assets/fb6b22b0-4e1e-4c53-a079-f91c500530bd">

생성한 스냅샷의 목록이 보인다. 작업에서 ‘스냅샷 복원’을 선택해 RDS로 복원시켜 사용할 수 있다.

<br/>

## 리눅스 추가 명령어

- `ipconfig` : ip 확인
- `ps -al` : 프로세스 pid 확인
- `kill [PID]` : 프로세스 삭제
- `watch` : 주기적으로 명령어 실행
- `export [변수명]=[값]` : 환경변수 지정
- `alias [새로운명령어]=[기존명령어 조합]` : 명령어를 단축어로 지정
    - `unalias [alias]` : alias 삭제
- `echo $[환경변수]` : 환경변수 값 출력