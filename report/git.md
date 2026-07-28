# GIT 실습

## Organization 생성 및 repository 만들기 
### organization 만들기 
1. GitHub 로그인 > 우측 상단 프로필 클릭 > Settings(설정) 
2. `New organization`  > 요금제 Free 선택 > `Create a free organization` > 조직 정보 입력
### repository 만들기 
   1. Repositories 탭으로 이동  > `New Repository` > 레포지토리 이름 입력 후 생성

![git-1.png](/resources/image/git-1.png)

### 로컬에 GIT 설치 후 연동하기
1. homebrew 설치하기 (homebrew: Mac OS 터미널에서 프로그램을 다운로드할 수 있게 해주는 프로그램)
    ```shell
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
2. git 설치
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
4. git 설정 확인하기 
    ```shell
    git config --list
    ```
    ![git-3](/resources/image/git-3.png)

## SSH 설정하기 

