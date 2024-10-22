# 네이버 클라우드 캠프 AWS 사전 강의 - 5일차

| 10/21(월) 네이버 클라우드 캠프 AWS 사전강의 학습 내용


## Auto Scaling
AWS Auto Scaling은 애플리케이션의 수요에 맞춰 컴퓨팅 리소스를 자동으로 확장하거나 축소하는 서비스이다. 예를 들어 웹사이트에 접속하는 사용자가 갑자기 많아질 때 서버를 자동으로 추가하거나 트래픽이 줄어들면 불필요한 서버를 줄이는 등의 작업을 수행한다. 이 기능을 통해 애플리케이션은 언제나 적절한 성능과 비용 효율성을 유지할 수 있다.

### API 생성

EC2 인스턴스를 생성하고 아파치 서버까지 설치한다. 그리고 해당 인스턴스를 기준으로 시작 템플릿으로 적용할 AMI를 생성한다.

<img width="573" alt="스크린샷 2024-10-21 오전 9 46 55" src="https://github.com/user-attachments/assets/9e317033-1c58-4d06-902e-b12366427764">

인스턴스를 생성하고 작업 → 이미지 및 템플릿 → 이미지 생성을 선택해 인스턴스를 이미지화 시킨다.

<br/>

<img width="1126" alt="스크린샷 2024-10-21 오전 9 48 57" src="https://github.com/user-attachments/assets/d821474c-29de-4507-b4a9-4b1ac07a1458">

이미지 이름을 지정해준다.

<br/>

<img width="1145" alt="스크린샷 2024-10-21 오전 9 49 44" src="https://github.com/user-attachments/assets/5e633bff-23f4-465f-b12f-fa4bbe586a5c">

생성된 이미지가 있는지 확인한다.

<br/>

### 시작 템플릿 생성

시작 템플릿은 AutoScaling을 통해 EC2 인스턴스를 어떻게 구성하여 올릴지 설정하는 템플릿이다. 

<br/>

<img width="803" alt="스크린샷 2024-10-21 오전 9 52 38" src="https://github.com/user-attachments/assets/80c7876b-fc32-4187-ad8e-3c5738743614">

템플릿 이름과 Auto Scaling 지침을 선택했다.

<br/>

<img width="796" alt="스크린샷 2024-10-21 오전 9 52 53" src="https://github.com/user-attachments/assets/6a3f49ce-62da-4e01-8f52-e7af0ca606d2">

기존에 생성한 AMI를 선택한다.

<br/>

<img width="804" alt="스크린샷 2024-10-21 오전 9 53 51" src="https://github.com/user-attachments/assets/01dac30e-827a-4068-8d02-672cd3bba966">

애플리케이션 및 OS 이미지 설정 → 기존 EC2 인스턴스를 생성하던 것과 같은 방식으로 구성해주면 된다. AutoScaling으로 인스턴스가 추가될 때 해당 인스턴스의 구성을 설정하는 과정이다. 

<br/>

<img width="802" alt="스크린샷 2024-10-21 오전 9 55 53" src="https://github.com/user-attachments/assets/4f4daf97-0544-4d4f-be9c-31fb08789fa3">

보안그룹 설정

<br/>

<img width="743" alt="스크린샷 2024-10-21 오전 9 56 53" src="https://github.com/user-attachments/assets/b05d0838-d14a-4efa-a445-861ed3d90f72">

사용자 데이터에는 AutoScaling에 의해서 인스턴스가 생성되면 실행시킬 명령어를 입력한다. 여기서는 아파치 서버가 실행되도록 입력했다.

<br/>

### AutoScaling 그룹 생성

태그에서 Key(name) Value(auto-group)으로 설정하면 ec2 인스턴스관리가 편리하다고 한다. 

<img width="1018" alt="스크린샷 2024-10-21 오전 9 50 21" src="https://github.com/user-attachments/assets/2ecf706c-2d90-4139-b27b-c8047b1ae177">

<img width="827" alt="스크린샷 2024-10-21 오전 9 52 04" src="https://github.com/user-attachments/assets/14cb543d-ce71-4017-a542-9e3f09242b44">

시작템플릿으로 기존에 생성한 템플릿을 선택한다.

<br/>

<img width="828" alt="스크린샷 2024-10-21 오전 10 05 01" src="https://github.com/user-attachments/assets/61b5900b-4644-4b86-881e-a635f118e6fc">

3일차에 생성해둔 로드밸런서를 선택한다. 

<br/>

<img width="783" alt="스크린샷 2024-10-21 오전 10 07 02" src="https://github.com/user-attachments/assets/3bc8c87e-a1d0-4dbd-9773-a40b9ed5ae55">

조정정책에서는 AutoScaling 그룹을 조정하는 옵션들을 설정한다. 평균 CPU 사용률을 10으로 설정해 바로 인스턴스의 증설을 확인할 수 있도록 설정했다.

<br/>

<img width="784" alt="스크린샷 2024-10-21 오전 10 07 09" src="https://github.com/user-attachments/assets/03c6b091-8264-47cc-86f6-913d61f0ffb1">

크기를 설정하는 곳에서 원하는 용량, 최소 용량, 최대 용량을 설정해줄 수 있다. Auto Scaling을 통해 유지할 인스턴스의 수, 늘릴 인스턴스의 수를 정할 수 있다.

AutoScaling 그룹생성을 마치면 CPU 설정에서 대상 값을 10을 줬기 때문에 바로 인스턴스를 생성하는 것을 보고 잘 동작하는 것을 확인할 수 있다.

<br/>

## Light Sail

AWS의 LightSail과 WordPress를 사용하여 블로그 웹 사이트를 아주 손쉽게 만들어볼 수도 있다.

<img width="1099" alt="스크린샷 2024-10-21 오후 7 50 38" src="https://github.com/user-attachments/assets/5a94225c-4f98-4127-8eb1-86a8ff11fe7e">

<img width="937" alt="스크린샷 2024-10-21 오전 10 17 27" src="https://github.com/user-attachments/assets/b4e4b3d1-9cf4-4cbc-b0c3-e814d7d15efc">

<img width="906" alt="스크린샷 2024-10-21 오전 10 17 33" src="https://github.com/user-attachments/assets/0648c809-15a0-49d9-abb2-913847bb5d35">

리눅스 플랫픔과 WordPress를 선택하고 5$의 요금을 선택한다. 3달동안은 무료이므로 만들고 삭제하면 과금의 걱정은 없다.

<br/>

<img width="1347" alt="스크린샷 2024-10-21 오후 7 54 53" src="https://github.com/user-attachments/assets/197853f9-d41b-440e-911c-7b607765044f">

<img width="478" alt="스크린샷 2024-10-21 오후 7 55 11" src="https://github.com/user-attachments/assets/403fea66-b90b-4740-8635-a266e2802996">

생성하고 부여된 Ip주소로 접속을 해보면 블로그형태의 웹사이트를 만나볼 수 있다. 해당 IP주소에 `/login`을 붙여 접속해보면 로그인할 수 있는 창이 나오는데 아이디와 비밀번호가 필요하다.

<br/>

<img width="1079" alt="스크린샷 2024-10-21 오후 7 53 19" src="https://github.com/user-attachments/assets/dd50b294-e8d9-4df8-ad91-23a325dea2fe">

비밀번호를 알아내기 위해서 인스턴스로 들어가 connect를 선택한다.

<br/>

<img width="991" alt="스크린샷 2024-10-21 오후 7 56 08" src="https://github.com/user-attachments/assets/1cabe3d1-9de7-43b3-bc1e-3a75d4155080">

그러면 콘솔창이 나오게 되는데 `cat bitnami_application_password`를 입력하면 비밀번호를 알아낼 수 있다. 로그인창에 아이디는 ‘user’, 비밀번호에는 방금알아낸 비밀번호를 입력하고 로그인한다.

<br/>

<img width="2532" alt="스크린샷 2024-10-21 오후 8 01 06" src="https://github.com/user-attachments/assets/80c6cfb2-3a75-4452-bce0-ab087dda16de">

그러면 이렇게 블로그 관리 화면으로 들어갈 수 있다.

<br/>

### Code Commit
---

Code Commit은 깃허브와 같이 리포지토리를 생성하여 소스 코드를 버전관리할 수 있다.

<img width="835" alt="스크린샷 2024-10-21 오전 10 54 01" src="https://github.com/user-attachments/assets/6bc9d376-02d2-498d-8c7d-890d6e350c05">

먼저 리포지토리 이름을 지정하여  리포지토리를 생성한다.

<br/>

<img width="1039" alt="스크린샷 2024-10-21 오전 10 54 35" src="https://github.com/user-attachments/assets/d18b90c2-3ecd-482a-8481-1119f2f36d57">

<img width="1046" alt="스크린샷 2024-10-21 오전 10 55 13" src="https://github.com/user-attachments/assets/b16c2acb-2a26-4acb-8335-fee6935f2ad8">

생성한 리포지토리안에 아무 내용의 파일을 생성해본다.

<br/>

<img width="1041" alt="스크린샷 2024-10-21 오전 10 55 18" src="https://github.com/user-attachments/assets/d48e0dcf-507e-4069-99e6-6c584416f50c">

깃허브처럼 커밋 메시지를 입력하여 변경사항을 커밋할 수 있다.

<br/>

<img width="1068" alt="스크린샷 2024-10-21 오전 10 55 57" src="https://github.com/user-attachments/assets/e10ab1c8-289b-4185-9143-1919a65bcc97">

리포지토리를 보면 방금 작성한 txt 파일이 생성된것을 볼 수 있다.

<br/>

<img width="1364" alt="스크린샷 2024-10-21 오전 10 58 08" src="https://github.com/user-attachments/assets/afee61af-b6a3-44e3-af78-290bd4e59b3c">

리포지토리를 생성하면 기본브랜치로 main브랜치가 자동으로 생성된다. 다른 브랜치를 생성하고 해당 브랜치에 변겨사항을 입력하고 병합을 시도해보자.

<br/>

<img width="1048" alt="스크린샷 2024-10-21 오전 11 04 28" src="https://github.com/user-attachments/assets/296d6c1b-058f-41f6-a274-6f2633ec170a">

<img width="1070" alt="스크린샷 2024-10-21 오전 11 04 38" src="https://github.com/user-attachments/assets/edeebda4-d0c9-4e79-93ac-90e39db46561">

<img width="1068" alt="스크린샷 2024-10-21 오전 11 04 46" src="https://github.com/user-attachments/assets/a8247d48-ec72-4b56-8832-8357ecfe603c">

변경사항을 작성하고 Pull Request를 요청할 수 있다. 해당 브랜치 →main을 가리키게 하고 풀 요청을 병합까지 해본다.

<br/>

<img width="1076" alt="스크린샷 2024-10-21 오전 11 04 58" src="https://github.com/user-attachments/assets/8eb5a6c2-b32f-4b6e-81cc-9ec253c2609e">

<img width="1079" alt="스크린샷 2024-10-21 오전 11 05 17" src="https://github.com/user-attachments/assets/f47c6e9b-a306-4189-9023-d0a4b088879f">

이제 리포지토리로 들어가 보면 새롭게 만든 브랜치에서 변경한 내용이 메인 코드에 적용된것을 볼 수 있다.

<br/>

## CodeDeploy
AWS CodeDeploy는 애플리케이션을 자동으로 배포할 수 있게 해주는 배포 서비스이다. 사용자는 CodeDeploy를 통해 서버, 컨테이너, Lambda 함수 등 다양한 환경에 애플리케이션을 쉽게 배포할 수 있다. 이 서비스를 사용하면 배포 프로세스를 자동화하고, 애플리케이션 배포 중 발생할 수 있는 다운타임을 줄이며, 오류를 방지할 수 있다.

### 2개의 역할 생성

먼저 2개의 역할을 생성해준다. 하나는 S3의 모든 접근 권한을 가지고 하나는 Code Deploy의 모든 접근 권한을 가지도록 한다.

각각 AmazonS3FullAccess 권한과 AWSCodeDeployRole 권한을 부여해주었다. 

### EC2 인스턴스 생성

위에서 만든 S3의 접근 권한을 부여한 EC2 인스턴스를 생성한다. 이 인스턴스에 CodeDeploy-agent를 설치하고 이 프로그램을 사용해서 EC2에 존재하는 S3에 웹 애플리케이션 프로젝트를 저장한다. 

<img width="803" alt="스크린샷 2024-10-21 오후 9 25 27" src="https://github.com/user-attachments/assets/ecb491e7-c739-42f6-aceb-e9076ec2fb52">

위와 같이 인스턴스를 생성하는 화면의 ‘고급 세부 정보’에서 IAM 인스턴스 프로파일로 앞서 만든 S3 권한을 가지고 있는 역할을 선택해준다.

<br/>

<img width="841" alt="스크린샷 2024-10-21 오후 9 33 31" src="https://github.com/user-attachments/assets/587da80f-8387-44f1-84ef-6b4d5a0ced35">

인스턴스를 생성한 후 태그 관리로 들어가서 AppName의 태그 (원하는 키, 값)를 부여했다. 

이제 인스턴스로 접속해서 CodeDeploy-agent를 설치할 환경을 구성한다.

```bash
# 운영체제 업데이트
yum update -y

# CodeDeploy에서 사용하는 Ruby 설치
yum install ruby -y

# CodeDeploy 설치파일을 다운로드 받기 위해 파일다운로드 패키지 wget 설치
yum install wget -y

# CodeDeploy-agent 설치
wget https://aws-codedeploy-ap-northeast-2.s3.amazonaws.com/latest/install

# install 파일에 실행권한 부여
chmod +x install

# 자동 설치 시작
./install auto

# CodeDeploy-agent 설치 확인
service codedeploy-agent status
```

EC2인스턴스의 운영체제를 최신화하고 CodeDeploy에서 사용하는 Ruby를 설치한다. 그리고 CodeDeploy-agent의 설치파일을 다운로드하기 위해 파일다운로드 패키지인 wget을 설치한다. wget을 통해 CodeDeploy-agent의 설치파일(install)을 다운로드하고 이 파일에 실행권한을 부여한다. `./install auto` 명령어를 통해 설치를 자동으로 진행시키고 마지막으로 설치가 잘되었는지 `service codedeploy-agent status`를 통해 확인한다.

<br/>

<img width="620" alt="스크린샷 2024-10-21 오후 10 17 11" src="https://github.com/user-attachments/assets/d91b68f3-3bf3-4486-97f3-6eb57d941777">

마지막 명령어를 통해 PID 번호를 보여주면 설치를 완료한것이다.

<br/>

### 사용자 액세스키 발급

이제 IAM 사용자를 생성하고 액세스키를 발급한다. 사용자의 권한으로는 AmazonS3FullAccess와 AWSCodeDeployFullAccess 권한을 부여한다.

<br/>

<img width="2163" alt="스크린샷 2024-10-21 오후 10 27 17" src="https://github.com/user-attachments/assets/233bbd8c-ecac-4eea-b48b-8da310c03f5d">

보안 장격 증명 → 액세스 키 만들기 선택

<br/>

<img width="1766" alt="스크린샷 2024-10-21 오후 10 27 40" src="https://github.com/user-attachments/assets/602e1625-a50a-4199-bb23-401dfdf86a31">

AWS 컴퓨팅 서비스(EC2에서 사용할것이므로)에서 실행되는 애플리케이션 선택

다음을 누르면 액세스키와 비밀 액세스키를 발급해주는데 둘다 꼭 복사해둔다. 

<br/>

### EC2에 IAM 사용자 등록

<img width="452" alt="스크린샷 2024-10-21 오후 10 34 34" src="https://github.com/user-attachments/assets/d6212d90-2193-49a1-97a1-a4cddaa930be">

EC2 서버에 aws configure 명령어를 입력하면 AWS 사용자 정보를 입력하라고한다.

1. 액세스 키
2. 비밀 액세스 키
3. 지역 (ap-northeast-2)
4. Default output format : 입력하지 않아도 된다.

<br/>

```bash
aws deploy create-application --application-name {웹앱이름}
```

위 명령어를 통해서 내 웹 프로젝트를 AWS로 배포할 웹 애플리케이션으로 만든다.

<br/>

```bash
aws deploy push --application-name {웹앱이름} |
	--s3-location s3://{버킷명}/{파일명}.zip --ignore-hidden-files
```

기존의 S3 버킷에 현재 웹 애플리케이션을 배포한다. 이제 S3의 DNS 주소를 통해 내 웹사이트로 접속해볼 수 있다.