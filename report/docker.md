# Docker 실습
> **Docker란?**
> 
> | 용어 | 설명 | 
> | :--- | :--- | 
> | **Docker** | 컨테이너 기반 가상화 플랫폼 
> | **Image** | 컨테이너 실행에 필요한 모든 것이 담긴 파일 (변경 불가) | 
> | **Container** | 이미지를 실행한 독립된 프로세스 공간 | 
> | **Daemon** | 도커의 명령을 처리하는 백그라운드 서비스 | 
> | **Volume** | 데이터를 영구적으로 보관하기 위한 공유 저장소 | 
> | **Registry** | 도커 이미지를 보관하고 공유하는 저장소 (예: Docker Hub) | 
![docker-2](/resources/image/docker-2.png)
## 도커를 설치한다.  
### 도커를 설치하고 버전을 확인한다
```shell
brew install docker # 도커 설치 
docker --version # 도커 버전 확인
```
![docker-1](/resources/image/docker-1.png)
### 도커 기본 운영 명령을 수행한다
ubuntu linux 또는 Nginx 이미지를 다운로드한다. 
```shell
docker pull ubuntu 
```
> **nginx**
> 
> 웹 서버 소프트웨어로 서버에서 부담을 주지 않도록 정적 자료를 서빙하거나, 리버스 프록시, 로드 벨런싱 기능을 제공한다. 
>
> 리버스 프록시: 사용자에게 내부 서버 구조를 숨긴다. 사용자의 요청을 nginx가 받아서 내부 서버로 전달한다. 
도커 데몬이 꺼져있으면 실행되지 않는다. 이땐, docker desktop을 먼저 실행한다. 
```text
Cannot connect to the Docker daemon at unix:///Users/~~/.docker/run/docker.sock. Is the docker daemon running?
 ```
다운로드 받은 이미지 목록을 확인한다. 
```shell
docker images
```
![docker-4.png](/resources/image/docker-4.png)
컨테이너를 실행하고 중지한다. 그리고 컨테이너 목록을 확인한다.
```shell
docker run -d -p 8080:80 --name my-nginx nginx ## 실행
```
-d (Detached): 컨테이너를 백그라운드에서 실행한다. 
-p 8080:80 (Port): 내 컴퓨터의 8080 포트와 컨테이너의 80 포트를 연결한다
--name : 컨테이너에 이름을 붙인다. (이름이 없으면 도커가 랜덤하게 지어준다.)
![docker-7.png](..%2Fresources%2Fimage%2Fdocker-7.png)
```shell
docker ps ## 실행중 목록 확인
docker stop my-nginx ##  중지
docker start my-nginx ## 재실행
```
![docker-8.png](..%2Fresources%2Fimage%2Fdocker-8.png)

컨테이너를 삭제한다. 
```shell
docker rm -f my-ubuntu
```
![docker-6.png](..%2Fresources%2Fimage%2Fdocker-6.png)
- [ ] Docker
    - [ ] 로그 확인
    - [ ] 리소스 확인
- [ ] 컨테이너 실행 후 간단한 명령을 수행한다.
    - [ ] `docker run hello-world`
    - [ ] ubuntu 설치 후 접속해서 `ls`, `echo` 실행
    - [ ] 컨테이너 종료(attach)/유지(exec)
- [ ] 커스텀 이미지 생성 (ubuntu)
    - [ ] 사용자 계정을 추가한다.
    - [ ] 헬스체크 기능을 추가한다.
- [ ] 포트 맵핑, 접속 후 결과를 기록한다.
- [ ] 볼륨을 생성하고 컨테이너에 연결한다. 컨테이너 삭제 후 재기동해서, 데이터 영속성을 확인한다.
- [ ] docker-compose.yml 파일을 생성한다.
    - [ ] 컨테이너 2개를 띄워 서로 통신한다.
    - [ ] `up`, `down`, `ps`, `logs`를 사용해 실행/종료/상태/로그를 관리한다.
    - [ ] 환경변수를 주입해 서버 포트/모드를 바꿔본다.
