# 네이버 클라우드 캠프 AWS 사전 강의 - 4일차
> 10/18(금) 네이버 클라우드 캠프 AWS 사전강의 학습 내용
<br/>

## ELB(Elastic Load Balancer) 로드밸런서 사용해보기

### ELB란?

AWS에서 제공하는 로드 밸런싱 서비스이다. ELB는 클라우드 환경에서 애플리케이션의 트래픽을 여러 서버(EC2 인스턴스 등)로 분산하여 가용성과 확장성을 향상시키는 역할을 한다. 

- 트래픽 분산
    - ELB는 들어오는 네트워크 트래픽(HTTP, HTTPS, TCP, UDP 등)을 여러 서버 인스턴스로 분산시켜 서버의 과부하를 방지하고 애플리케이션의 가용성을 높여준다.
- 자동 확장 (Auto Scaling)
    - ELB는 AWS의 Auto Scaling과 통합되어 작동한다. 따라서 트래픽이 증가하면 더 많은 인스턴스를 자동으로 추가하고 트래픽이 줄어들면 인스턴스를 줄일 수 있다.
- 내결함성 (Fault Tolerance)
    - ELB는 여러 가용영역(AZ)에 걸쳐 애플리케이션을 배포하고 각 가용영역에 트래픽을 분산시켜 장애 발생 시에도 서비스를 유지할 수 있다.
- 헬스 체크 (Health Check)
    - ELB는 각 서버의 상태를 주기적으로 확인하여 정상적으로 작동하는 서버에만 트래픽을 전달한다. 이를 헬스 체크(Health Check)라고 한다.

### ELB의 종류

- ALB (Application Load Balancer)
    - HTTP와 HTTPS 트래픽을 처리하는 데 적합한 로드 밸런서이다.
    - 애플리케이션 계층(OSI 7계층)에서 작동하며 트래픽을 라우팅할 때 URL 경로, 헤더, 쿠키 등의 정보를 기반으로 정교한 라우팅이 가능하다.
    - 마이크로서비스 아키텍처(MSA)나 컨테이너 기반 애플리케이션에서 자주 사용된다.
- NLB (Network Load Balancer)
    - TCP, UDP, 및 TLS 트래픽을 처리하며 매우 낮은 레이턴시와 고성능이 요구되는 애플리케이션에 적합하다.
    - 네트워크 계층(OSI 4계층)에서 작동하며 트래픽을 IP 주소 및 포트에 기반하여 분산한다.
    - 대규모 트래픽이나 고속 응답이 필요한 애플리케이션에서 사용된다.
- GLB (Gateway Load Balancer)
    - Gateway Load Balancer를 사용하면 타사 가상 어플라이언스를 쉽게 배포, 규모 조정 및 관리할 수 있다.
    - 여러 가상 어플라이언스에 트래픽을 분산하는 동시에, 수요에 따라 규모를 늘리거나 줄일 수 있는 단일 게이트웨이를 제공한다. 이렇게 하면 네트워크의 잠재적 장애 지점이 줄어들고 가용성이 향상된다.
- CLB (Classic Load Balancer)
    - 이전 세대의 로드 밸런서로 HTTP(S) 및 TCP 트래픽을 처리한다.
    - 애플리케이션 계층(7계층)과 네트워크 계층(4계층)을 모두 지원하지만 현재는 주로 레거시 애플리케이션에 사용된다.

### ELB의 사용예시

- 웹 애플리케이션 서버의 트래픽 분산
    - 사용자가 웹사이트에 접속할 때 ELB가 여러 EC2 인스턴스에 요청을 분산시킨다.
    - 트래픽이 급격히 증가해도 ELB와 Auto Scaling이 자동으로 인스턴스를 추가하여 처리할 수 있다.
- 마이크로서비스 아키텍처(MSA)
    - ALB를 사용하여 각각의 마이크로서비스에 경로 기반 라우팅(Path-based routing)을 설정할 수 있다.(예를 들어 `/api/service1` 요청은 서비스1로 `/api/service2` 요청은 서비스2로 전달할 수 있다)

<br/>

### 사용해보기

먼저 1일차에서 배웠던 EC2 인스턴스를 2개 생성하고 각각 아파치 서버를 세팅하는 작업을 해준다. 그리고 각 서버의 index.html의 내용을 달리해 다른 문자열이 띄워지게끔 해준다. (예를 들어 서버1에서는 ‘Hello AWS’를, 서버2에서는 ‘Hello AWS2’를 띄우게한다)

<img width="2242" alt="스크린샷 2024-10-18 오후 4 53 35" src="https://github.com/user-attachments/assets/40e2a0ac-fa53-4663-b9cf-0c0017da8eb3">

‘로드밸런서 생성’을 선택해 로드밸런서 생성을 시작한다.

<br/>

<img width="845" alt="스크린샷 2024-10-18 오후 4 54 11" src="https://github.com/user-attachments/assets/e90182e0-3ac1-473a-b07f-1b1ad9d8661b">

여기서는 Classic Load Balancer를 생성해본다. 차례대로 앞서 살펴봤던 ALB, NLB, GLB, CLB를 나타낸다. 

<br/>

<img width="1127" alt="스크린샷 2024-10-20 오후 1 50 21" src="https://github.com/user-attachments/assets/b523479b-24a6-49bf-b51c-aff4d9295a8c">

가용영역은 모두 선택해주었다. 1개만 선택할경우 작동하지 잘 작동하지 않는다. 최소 2개의 가용영역을 선택해준다.

<br/>

<img width="1121" alt="스크린샷 2024-10-20 오후 2 02 28" src="https://github.com/user-attachments/assets/91742ba9-49fd-40d2-82eb-de1a8cd91f47">

앞서 생성한 2개의 인스턴스를 등록한다.

<br/>

<img width="1124" alt="스크린샷 2024-10-20 오후 1 50 49" src="https://github.com/user-attachments/assets/76c89d69-e9fe-43e2-9db4-536ee0ec9275">

보안그룹은 인스턴스들의 보안그룹과 동일한것으로 맞춰주었다. 

<br/>

<img width="2241" alt="스크린샷 2024-10-20 오후 2 29 20" src="https://github.com/user-attachments/assets/0b6bc38a-75cc-456a-aa7b-c2a553bb057e">

생성을 해주고 각 인스턴스들의 상태가 서비스중인지 확인해준다.

<br/>

<img width="2203" alt="스크린샷 2024-10-20 오후 2 29 50" src="https://github.com/user-attachments/assets/9e719ba1-9fca-40c5-baae-734d26bcde70">

로드밸런서의 세부정보로 접속해보면 DNS주소를 부여해주는데 이 주소를 주소창에 입력하고 접속하면 우리가 생성한 인스턴스의 index.html 내용이 보이게 되고 새로고침을 할 때마다 다른 인스턴스를 띄워주게된다. 

로드밸런서는 이렇게 트래픽을 적절히 분산시켜 접속시킨다.