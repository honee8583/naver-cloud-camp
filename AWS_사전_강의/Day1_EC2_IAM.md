# 네이버 클라우드 캠프 AWS 사전 강의 - 1일차
| 10/15(화) 네이버 클라우드 캠프 AWS 사전강의 학습 내용
<br/>

## IAM 사용자 추가

<img width="2150" alt="스크린샷 2024-10-15 오후 3 26 53" src="https://github.com/user-attachments/assets/a4abe94c-f92c-4637-9643-19e245041021">

AWS → IAM → 사용자 생성으로 들어가 사용자 등록을 시작한다. 

<br/>

<img width="1244" alt="스크린샷 2024-10-15 오후 3 27 59" src="https://github.com/user-attachments/assets/6f1438a9-a4b0-4e5f-ac45-ee24dd06adc3">

원하는 사용자 이름과 사용자 지정 암호를 입력해주고 나머지 사항을 선택해준다.

<br/>

<img width="2174" alt="스크린샷 2024-10-15 오후 3 31 23" src="https://github.com/user-attachments/assets/4acaf426-a685-4cb7-b981-eda8fe9c9fdd">


그룹에 사용자를 추가하고 싶은 경우 권한 옵션에서 ‘그룹에 사용자 추가’를 선택하고 밑에서 추가할 사용자 그룹을 선택하고 다음을 누른다.

추가하고 싶지 않을 경우 사용자 그룹을 선택하지 않고 다음을 누른다.

<br/>

<img width="2166" alt="스크린샷 2024-10-15 오후 3 32 18" src="https://github.com/user-attachments/assets/3868efd7-750e-4deb-907e-5fa9ca3c3492">

위에서 사용자 그룹에 추가했을 경우 권한 요약에서 사용자 그룹을 확인해볼 수 있고 기본적인 권한으로 `IAMUserChangePassword` 권한이 들어가있다.

<br/>

<img width="2175" alt="스크린샷 2024-10-15 오후 3 41 14" src="https://github.com/user-attachments/assets/83cd6328-8997-46a6-b372-60962e0f81de">

사용자에게 권한 정책을 부여해보기 위해 원하는 사용자로 들어가서 ‘직접 정책 연결’로 들어가 dynamoDB관련 정책을 부여한다. 여기서는 `AmazonDynamDBReadOnlyAccess` 정책을 부여해준다.

<br/>

<img width="2200" alt="스크린샷 2024-10-15 오후 3 37 35" src="https://github.com/user-attachments/assets/64be0625-94b9-418f-baf5-d81451382d09">

사용자에게 부여된 정책을 확인해보기 위해 IAM → 대시보드 → 도구 → 정책 시뮬레이터로 들어간다.

<br/>

<img width="403" alt="스크린샷 2024-10-15 오후 3 47 24" src="https://github.com/user-attachments/assets/7fd60c1d-ab69-4394-b1c4-12cfd4f95f26">

정책 시뮬레이터에서 드롭 다운에서 Users로 들어가 확인하고자 하는 사용자를 선택해준다.

드롭 다운에는 Users, Groups, Roles 세가지가 있는데 Groups로 들어가 사용자 그룹의 정책을 확인해볼 수도 있다.

<br/>

<img width="398" alt="스크린샷 2024-10-15 오후 3 51 24" src="https://github.com/user-attachments/assets/83a29704-c0a3-425c-8282-37da169263bc">

이전에 추가한 AmazonDynamoDBReadOnlyAccess 권한 정책이 잘 들어가있는 모습이다.

<br/>

<img width="1228" alt="스크린샷 2024-10-15 오후 3 52 22" src="https://github.com/user-attachments/assets/50f430d7-57fd-4789-8b64-878e7fb3448d">

정책 시뮬레이터의 오른쪽의 Policy Simulator에서 더 자세한 사항을 확인해볼 수 있다. 확인할 사용자를 클릭한 상태로 DynamoDB관련 정책의 세부사항을 확인해보기 위해 ‘DynamDB’를 검색한후 Select All → Run Simulation을 선택한다.

<br/>

<img width="1224" alt="스크린샷 2024-10-15 오후 3 54 01" src="https://github.com/user-attachments/assets/bf51f7ec-6a21-4294-b998-96c705382ba3">

사용자의 DynamDB관련 권한을 더 세부적으로 확인할 수 있다. 위에서 DynamDB에 대한 읽기권한만 부여해줬기 때문에 읽기가 아닌 다른 권한에 대해서는 denied가 뜨는 것을 볼 수 있다.

<br/>

### 📌 IAM을 사용하는 이유?

IAM에 대해서 배웠지만 IAM을 사용하는 이유에 대해서는 잘 와닿지 않아 검색해보았다. 

[팀 프로젝트에서 AWS 관리하기 (1) - IAM 사용자](https://dev-jaesoon.tistory.com/entry/AWS-IAM-사용자-만들기)

IAM을 사용하게 되면 팀프로젝트를 하게 될 때 하나의 AWS 계정을 공유하면서 관리하는 것이 아닌 IAM 사용자에 권한을 부여해 발급하면 개발자들이 접근할 수 있게 할 수 있었다. 

관리자용, 개발자용 IAM 으로 나뉘게 되며 관리자용은 루트 계정의 소유자가 사용하게 되고 개발자용은 나머지 개발자들이 사용하게 된다. 루트 계정은 가급적 사용하지 않게 된다고 한다.

관리자용 계정에는 AdministratorAccess 권한을 부여하고 개발자용 계정에는 PowerUserAccess  권한을 부여해 모든 서비스에는 접근이 가능하되 유저 관리에만 접근이 불가능하도록 한다.

이렇게 계정들을 생성하고 나오는 로그인 URL과 초기 비밀번호를 개발자들에게 전달해주면 해당 URL로 로그인을 하고 비밀번호를 다시 지정해 사용할 수 있게 된다.

로그인을 해보면 루트 계정의 EC2 인스턴스, S3 버킷 등등 모든 서비스에 접근이 가능했다. 

<br/>

## EC2 인스턴스 생성 및 접속

EC2 인스턴스 생성하는 방법은 기존에 알던것과 같아 작성하지 않는다.

### putty로 원격 접속하는 방법 (Windows)

[Download PuTTY: latest release (0.81)](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

putty 다운로드 사이트로 접속해 putty와 puttygen을 다운받는다. putty는 실제로 서버로 접속을 도와주는 프로그램이고 puttygen은 putty로 서버로 접속하기 위해 필요한 pem 키를 ppk 파일로 변환해주는 프로그램이다.

<aside>
💡 Mac 환경에서는 putty와 mobaexterm을 지원하지 않아 기존에 사용하던 termius를 사용하기로 했다.
</aside>

## 기본세팅 및 아파치 테스트해보기

EC2 서버에 접속해 아래와 같이 아파치 서버를 세팅해보고 접속 테스트 해본다.

```bash
# 운영체제 업데이트
yum update -y

# 아파치 설치
yum install httpd -y

# 아파치 시작
service httpd start

# 서버를 재부팅하면 아파치 서버도 같이 자동으로 시작하도록 설정
chkconfig httpd on

# index.html 파일 새성 및 파일 작성 시작
vi index.html
```

1. `yum update -y` : 생성한 EC2 서버의 운영체제를 최신버전으로 업데이트한다.
2. `yum install httpd -y` : 테스트할 아파치 서버를 설치한다.
3. `service httpd start` : 아파치 서버를 실행시킨다.
4. `chkconfig httpd on` : 서버를 재부팅할 때 아파치 서버 또한 같이 실행되도록 설정한다.
5. `vi index.html` : `index.html` 파일을 생성해 서버를 통해 아파치 서버의 동작을 확인해볼 수 있도록 한다.

<br/>

```html
<html>
	<body>
		<h1>Hello</h1>
	</body>
</html>
```

`index.html`안에는 간다한 코드를 넣어주었다.

<br/>

### 인바운드 규칙 편집

EC2 인스턴스의 인바운드 규칙을 설정해주지 않으면 위에서 설치한 아파치 서버로 접속이 불가능하다. 따라서 인바운드 규칙을 설정해 접속을 허용시켜준다.

<img width="683" alt="스크린샷 2024-10-15 오후 4 10 01" src="https://github.com/user-attachments/assets/58d5f274-9dc4-4d55-a82a-0174d43c45ea">

EC2 대시보드로 이동해서 실행하고 있는 ec2 인스턴스를 선택하고 보안 탭으로 이동해 보안그룹으로 이동한다.

<br/>

<img width="2238" alt="스크린샷 2024-10-15 오후 4 24 15" src="https://github.com/user-attachments/assets/cca1fae6-00c8-4624-8a00-0a7f55340d7c">

인바운드 규칙 → 인바운드 규칙 편집으로 들어간다.

<br/>

<img width="1405" alt="스크린샷 2024-10-15 오후 4 25 24" src="https://github.com/user-attachments/assets/1b36140b-5839-4e67-b2b3-df274e4cec5d">

‘규칙 추가’를 선택해 http와 https에 ‘내 IP’를 선택해 각각 추가해준다. 내 IP는 현재 내가 사용하고 있는 Ip 주소를 자동으로 입력해준다.

이제 EC2 서버의 public IP주소를 브라우저에 입력해서 접속해보면 내가 작성한 `index.html`의 내용이 뜨는 것을 볼 수 있다.