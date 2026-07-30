# GIT 실습
> **GIT & GitHub** 
> 
> GIT은 코드의 변경사항을 기록하는 분산형 버전관리 시스템이다. 
> 
> GitHub는 깃으로 관리하는 코드를 올릴 수 있는 클라우드 웹 서비스다.
> 
> 기본 개념 
> 
> | 용어         | 설명                                   | 
> |------------|--------------------------------------|
> | repository | 코드의 형상이 저장되는 공간                      |
> | branch | main 코드에 영향을 주지 않고 독립적으로 작업할 수 있는 가지 |
> | commit | 코드 변경 내용에 대한 기록 (저장)하는 단위            |
> | merge | 여러 브랜치의 작업내역을 한 브랜치로 합치는 행위 |
## Organization 과 Repository를 만든다
### organization을 만든다 
1. GitHub 로그인 > 우측 상단 프로필 클릭 > Settings(설정) 
2. `New organization`  > 요금제 Free 선택 > `Create a free organization` > 조직 정보 입력
### repository를 만든다 
   1. Repositories 탭으로 이동  > `New Repository` > 레포지토리 이름 입력 후 생성

![git-1.png](/resources/image/git-1.png)

### 로컬에 GIT을 설치하고 GitHub을 연동한다
1. homebrew를 설치한다 (homebrew: Mac OS 터미널에서 프로그램을 다운로드할 수 있게 해주는 프로그램)
    ```shell
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
2. git을 로컬에 설치한다
    ```shell
    brew install git
    ```
3. clone repository
 - 방법 1: IDE(intelliJ)에서 New Project from Version Control
![git-2](/resources/image/git-2.png)
 -  방법 2: 터미널에서 실행하기
    ```shell
    git clone  https://github.com/~~~
    ```
 - GitHub에서 private token 발급 (프로필 > Settings > Developer Settings > Personal access tokens > Generate new token)
4. git 설정을 확인하기 
    ```shell
    git config --list
    ```
    ![git-3](/resources/image/git-3.png)

## SSH 설정하기 
> **SSH(Secure Shell)** 
> 안전하게 외부 서버에 접속하기 위한 통로를 만드는 규약이다. 외부 서버에 공개키를 저장하고, 내부에는 개인키를 저장한다. 공개키, 개인키를 이용한 비대칭 암호화 방식으로 인증한다.  
> 내부서버: 통신 요청 > 외부서버: 공개키로 암호화한 값 전송 > 내부서버: 개인키로 복호화 후 전송 > 인증 성공
1.  ssh-key를 생성한다. 
    ```shell
    ssh-keygen -t ed25519 -C "****@gmail.com"
    ```
2. 공개키 값을 복사한다. 
    ```shell
    pbcopy < /Users/username/.ssh/id_ed25519.pub
    ```
3. github에 ssh key를 등록한다.
    ![git-ssh-1](/resources/image/git-ssh-1.png)
    ![git-ssh-2](/resources/image/git-ssh-2.png)
4. github repository로 이동해 ssh 접속용 주소를 복사한다. 
    ![git-ssh-3](/resources/image/git-ssh-3.png)
5. 로컬의 remote origin을 복사한 ssh 접속용 주소를 복사한다.
    ![git-ssh-4](/resources/image/git-ssh-4.png)
