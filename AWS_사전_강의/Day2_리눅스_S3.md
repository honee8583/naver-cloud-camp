# 네이버 클라우드 캠프 AWS 사전 강의 - 2일차
| 10/16(수) 네이버 클라우드 캠프 AWS 사전강의 학습 내용
<br/>

## 리눅스 명령어

- `pwd` : 현재 위치를 확인
- `clear` : 창에서 삭제
- `mkdir` : 디렉토리 생성(make directory)
- `cd` : 디렉토리 이동(change directory)
    - `cd ..` : 상위 디렉토리 이동
- `ls` : 디렉토리 파일 리스트 조회 (list)
    - `ls {경로명}` : 경로에 있는 파일리스트 조회
    - `-al`, `-alh` : 숨김파일을 포함한 모든 파일 및 폴더 조회
- `touch` : 파일 생성
    - `touch .{파일명}` : ‘.’을 붙이면 숨김 파일로 생성
- `tree` : 파일 구조 확인 (별도로 설치해야함)
    - `-d` : 디렉토리만 파일 구조 확인
    - `-a` : 숨김파일까지 “
- `cp` : 디렉토리/파일 복사 (copy)
    - `cp -r` : 디렉토리 복사
- `&&` : 명령어를 이어서 사용가능
(ex: touch file1 && touch file2)
- `mv` : 파일/디렉토리 이동 (move) 혹은 파일명 변경
    - `mv file1 file2` : file1의 이름을 file2로 변경
- `find` : 파일/디렉토리 찾기
- `rm` : 파일/디렉토리 삭제
    - `-r` : 디렉토리 삭제
    - `-rf` : 파일/디렉토리 강제 삭제
- `cat` : 파일 내용 확인
- `grep` : 출력 내용 검색
    - ex) cat Dockerfile | grep CMD : Dockerfile 파일에서 ‘CMD’가 포함된 문장들 검색
- `>` : 기존 파일이 있을 경우 덮어쓰기
    - ex) tree /etc | grep sh > result.text : result.text에 출력내용 저장
- `>>` : 기존 파일이 있을 경우 이어쓰기
- `tar -cvf [결과파일] [디렉토리]` : 결과파일을 아카이브해 디렉토리에 저장
    - tar : 아카이브 파일(하나의 파일로 묶음)
    - zip : 압축(데이터 크기도 줄어듬)
- `tar -xvf [tar파일]` : 아카이브 해제

### vi 편집기

- `vi {파일명}` : vi 편집기 열기
    - `i` : insert 모드 전환
    - `esc` : 명령어 모드 전환
    - `:wq` : 저장 및 종료
    - `:q` : 종료
- `dd` : 줄 삭제
- `yy` : 복사
- `p` : 붙여넣기
- `u` : 되돌리기
- `:set number` : 라인 번호 출력
- `/{찾을단어}` : 단어 찾기
    - 명령모드에서 `n` : 다음 단어로 이동
    - enter → i : 찾은 단어 위치에서 편집 가능

## S3

Amazon S3(Simple Storage Service)는 AWS에서 제공하는 클라우드 스토리지 서비스이며 인터넷에서 데이터를 안전하게 저장, 관리, 액세스할 수 있도록 설계된 확장이 가능한 객체 스토리지 서비스이다. 사용자는 이미지, 비디오, 문서, 백업 파일 등 다양한 형태의 데이터를 손쉽게 저장하고 필요한 때에 불러올 수 있다.

S3를 사용하여 웹 애플리케이션의 정적 파일을 저장하고 호스팅하는 것도 가능하다.

<br/>

### 버킷 생성

<img width="846" alt="스크린샷 2024-10-16 오후 4 46 31" src="https://github.com/user-attachments/assets/b0b022f9-79bc-46ef-a856-a05e4220027b">

AWS에서 S3 → 버킷 → 버킷 만들기로 들어가 버킷 이름을 입력

<br/>

<img width="819" alt="스크린샷 2024-10-16 오후 4 46 50" src="https://github.com/user-attachments/assets/65f70eeb-6549-4339-bc1b-cd8991bd59cc">

업로드한 객체에 접근해야 하므로 ‘모든 퍼블릭 액세스 차단’을 해제해주고 아래의 경고문 체크

<br/>

<img width="832" alt="스크린샷 2024-10-16 오후 4 47 34" src="https://github.com/user-attachments/assets/a4c3ed9e-cd45-40ec-a889-6517300fe369">

나머지는 기본상태로 두고 ‘버킷 만들기’ 선택. 이제 생성한 버킷에 이미지나 파일들을 업로드할 수 있다.

<br/>

### 정적 웹 사이트 호스팅 활성화

<img width="832" alt="스크린샷 2024-10-16 오후 4 47 34" src="https://github.com/user-attachments/assets/67d0f9b3-11cd-4b67-8e73-abfc107c0ae3">

버킷의 ‘속성’탭에서 정적 웹 사이트 호스팅을 활성화해준다. 편집으로 이동

<br/>

<img width="835" alt="스크린샷 2024-10-16 오후 4 57 21" src="https://github.com/user-attachments/assets/19e75251-a6e1-4467-9761-6e8b3bd5bd22">

정적 웹사이트 호스팅을 ‘활성화’로 변경해주로 웹사이트로 보여줄 파일명을 입력해준다.

<br/>

<img width="2175" alt="스크린샷 2024-10-16 오후 4 58 09" src="https://github.com/user-attachments/assets/5c37b87f-cf6c-49c8-8f9e-d808a0c149c9">

변경 사항을 저장해주면 바뀐모습을 확인할 수 있다.

<br/>

### 버킷 정책 편집

<img width="2186" alt="스크린샷 2024-10-16 오후 4 58 27" src="https://github.com/user-attachments/assets/08cef032-a5cd-449f-ae6b-464b55ddf190">

버킷 정책을 편집하기 위해 ‘권한’ 탭으로 들어가 버킷 정책에서 ‘편집’을 선택

<br/>

<img width="2181" alt="스크린샷 2024-10-16 오후 5 03 21" src="https://github.com/user-attachments/assets/4716296e-8f59-4ccf-832f-cb95c1596482">

보다 쉽게 정책을 Json 형식으로 생성하기 위해 ‘정책 생성기’ 선택. 위의 버전 ARN은 복사해둔다.

<br/>

![화면 캡처 2024-10-16 125657](https://github.com/user-attachments/assets/076ecb49-607b-4a6d-94cf-32d9e6e28c01)
- ‘S3 Bucket Policy’ 선택
- 모든 권한을 부여하기 위해 에스터리스크(*) 선택
- 복사해둔 ARN을 붙여넣은 후 ‘/*’을 뒤에 입력
- Add Statement 선택

<br/>

<img width="804" alt="스크린샷 2024-10-16 오후 5 04 13" src="https://github.com/user-attachments/assets/2d7c44af-6fe7-4385-b811-1c4c3e97a4c7">

위에서 생성한 정책에 대한 Json 형식의 문자열을 보여준다. 복사해둔다.

<br/>

<img width="2191" alt="스크린샷 2024-10-16 오후 5 04 26" src="https://github.com/user-attachments/assets/73de87d1-6e3f-4d3d-b742-30d5c913361d">

다시 정책으로 들어가 복사해둔 Json을 붙여주고 저장해준다.

이제 버킷에 정적 웹사이트 호스팅 설정에서 지정한 문서의 이름(ex: index.html)의 파일을 업로드하면 해당 문서를 웹사이트에서 볼 수 있다.