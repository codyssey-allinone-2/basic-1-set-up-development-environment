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
## 컨테이너를 실행하고 명령을 수행한다. 
도커 로그를 확인한다
```shell
 docker logs my-nginx
```
![docker-9.png](..%2Fresources%2Fimage%2Fdocker-9.png)
도커 리소스를 확인한다. 
```shell
docker stats my-nginx #리소스 사용량 확인 (CPU, 메모리, 네트워크, 디스크 I/O 사용량)
```
![docker-10.png](..%2Fresources%2Fimage%2Fdocker-10.png)
```shell
docker inspect my-nginx # 컨테이너 리소스 및 상세정보 확인
```
![docker-11.png](..%2Fresources%2Fimage%2Fdocker-11.png)
```shell
docker run hello-world
```
도커가 정상적으로 동작하는지를 테스트하는 튜토리얼 과정이다.
hello-world라는 이미지를 다운로드하고 컨테이너를 실행한다. 정상적으로 실행되면 곧바로 종료된다. 

![docker-12.png](..%2Fresources%2Fimage%2Fdocker-12.png)
도커 컨테이너에 접속해  `ls`, `echo` 실행한다. 
```shell
docker run -it ubuntu bash ## 도커 컨테이너 실행 후 바로 접속 
docker exec -it ubuntu bash ## 실행중인 도커 컨테이너 접속
echo <message> # 입력한 메세지를 그대로 출력 
ls # 현재 위치에서 디렉토리와 파일 확인
exit # 컨테이너 접속 종료
```
  - it 옵션: 표준 입출력을 이용해 터미널에서 컨테이너에 접속할 수 있게 해준다. 
  - bash : 컨테이너에서 bash 쉘로 명령어를 실행한다. 
  - d 옵션: 데몬으로 실행하겠다는 옵션이다. 옵션을 주지 않으면 exit로 터미널을 빠져나오면 컨테이너가 바로 종료된다. 
![docker-13.png](..%2Fresources%2Fimage%2Fdocker-13.png)
![docker-14.png](..%2Fresources%2Fimage%2Fdocker-14.png)

### 커스텀 이미지를 만든다. 
사용자 계정을 추가한다. 
```shell
adduser <username> # user 를 생성한다
passwd <username> # 비밀번호를 설정한다.
```
![docker-15.png](..%2Fresources%2Fimage%2Fdocker-15.png)
사용자 계정으로 접속한다. 
```shell
docker exec -it -u my-user my-nginx bash
```
`docker exec` 는 도커 관리자가 컨테이너 내부로 들어가는 관리용 우회 경로이므로 비밀번호를 입력하지 않는다. 
헬스 체크 기능을 추가한다. 
```shell
docker run -d \
  --name my-nginx \
  --health-cmd="curl -f http://localhost/ || exit 1" \
  --health-interval=30s \
  nginx
```
> **Health Check** 
> 
> 컨테이너가 실제로 정상 동작 중인지 확인하는 기능이다. 도커 엔진이 정해진 시간 간격으로 컨테이너에 요청을 보낸다. 

헬스 체크 기능을 추가할 때, 이미 띄워둔 컨테이너라면 아래와 같은 오류가 뜬다. 이땐 커스텀 이미지(현재 상태)로 저장하고, 컨테이너를 삭제한 후 다시 실행한다. 
> docker: Error response from daemon: Conflict. The container name "/my-nginx" is already in use by container "8034ef72bd9734ba47357457eb43909f5dd2385a4dc75baeb280ef3b22873505". You have to remove (or rename) that container to be able to reuse that name.
```shell
# 1. 현재 실행 중인 컨테이너를 'my-custom-nginx'라는 새 이미지로 저장
docker commit my-nginx my-custom-nginx

# 2. 기존 컨테이너 중지 및 삭제
docker rm -f my-nginx

# 3. 방금 만든 이미지로 헬스체크 옵션을 붙여 실행
docker run -d \
  --name my-nginx \
  --health-cmd="curl -f http://localhost/ || exit 1" \
  --health-interval=30s \
  my-custom-nginx
```
![docker-16.png](..%2Fresources%2Fimage%2Fdocker-16.png)
![docker-18.png](..%2Fresources%2Fimage%2Fdocker-18.png)
헬스 체크 기능을 추가하면 docker ps 명령을 실행했을 때 status가 아래처럼 나온다. 
>  Up 3 seconds (health: starting)

### 포트를 맵핑하고 접속한다. 
```shell
docker run -d -p 8081:80 --name my-nginx my-custom-nginx  # 내 로컬의 8081 포트를 컨테이너의 80포트와 맵핑
curl localhost:8081 ## 접속 확인
```
> **Port**
> 
> 서버에서 특정 프로그램을 찾아가기 위한 경로. 도메인주소나 IP가 서버를 지칭한다. 포트는 그 서버의 특정 프로그램을 찾는 고유번호다.   
![docker-17.png](..%2Fresources%2Fimage%2Fdocker-17.png)

### 볼륨을 생성하고 컨테이너에 연결한다. 
> Volumn
> 
> 볼륨은 도커가 관리하는 '외장 하드디스크'로 컨테이너의 데이터를 외부에 저장해두는 장치다. 컨테이너를 지웠다가 새로 띄워도 데이터가 유지된다. 
> 
```shell
docker volume create nginx-vol # 도커 볼륨 생성하기
docker volume ls #생성된 볼륨 확인하기
docker run -d \
  --name my-nginx \
  -p 8080:80 \
  -v nginx-vol:/usr/share/nginx/html \ # 컨테이너 내부의 이 위치에 볼륨을 연결한다.
  nginx

docker inspect my-nginx # Mounts 항목으로 확인하기 
```
![docker-19.png](..%2Fresources%2Fimage%2Fdocker-19.png)
![docker-20.png](..%2Fresources%2Fimage%2Fdocker-20.png)
컨테이너를 삭제하고 다시 기동할 때, -v 옵션 (경로)를 사용하면 그 위치는 볼륨에서 데이터를 가져온다. 
![docker-21.png](..%2Fresources%2Fimage%2Fdocker-21.png)

### docker-compose.yml 파일을 생성한다.
[docker.md](docker.md)
![docker-22.png](..%2Fresources%2Fimage%2Fdocker-22.png)
```shell
#docker 실행하기 
docker compose up -d
# 상태 확인하기 
docker compose ps
# web1 컨테이너 안에서 web2(80번 포트)로 요청 보내기
docker compose exec web1 curl -I http://web2
```
![docker-23.png](..%2Fresources%2Fimage%2Fdocker-23.png)
![docker-24.png](..%2Fresources%2Fimage%2Fdocker-24.png)
> **Docker Compose**
> 
> 여러 개의 도커 컨테이너를 하나의 설정 파일로 묶어서 한 번에 관리해 주는 도구다.
