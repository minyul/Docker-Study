# Docker-Study

인프런 강의를 보며 도커, 도커컴포즈를 공부해보자

![우악](https://user-images.githubusercontent.com/86240112/133885418-b46857b8-d112-4d21-8590-e48d1a377608.png)

----

# 도커 강의 시작 

도커 : 컨테이너 기반의 오픈 소스 가상화 플랫폼
어떤 문제를 어떻게 해결했는지 부터 공부해보자 !

서버관리란 ?  Node 로쓰기로 했다 Python으로 쓰기로했다 Ruby를 쓰기로했다!
이렇게 개발환경이 계속 바뀐다.

도커가 등장하고 서버관리/ 개발방식이 완전히 바뀌게 된다.

# 도커 컨테이너 실행 데모

젠킨스 : 소프트웨어 개발 시 지속적 통합 서비스를 위해 제공하는 툴.

원래는 !
유저를 추가하고 환경변수, 방화벽, 네트워크 .. 등등 깃클론 하고 패키지 설정하고 데이터베이스만들고 프록시 서버만들고
해야 프로그램이 뜨는거다


Mysql 도 컨테이너, Redis도 컨테이너! 래빗업큐, 젠킨스 전부 컨테이너로 만들수있어 ( 서로 다른 프로그램들이 ! )

이 컨테이너가 아마존이든 어디든 클리우드에서 전부 실행이 가능하다!

가상머신처럼 독립적으로 실행되지만 !!
가상머신보다 빠르고 쉽고 효율적이다
리눅스 부팅부터도 안하고 그냥 명령어 치면되고 docker compose-up 으로 실행가능 !


# 도커의 등장

원래는 PPT 에 서버 배포하는 방법이 있고 그걸 계속 따라서 했다.
뭐가 문제일까 !

1. 
이 문서가 정확한 걸까?
다른 OS에는 어떻게 설치할까?
왜 똑같이 따라했는데 왜 안되지!?

음... 문서는 부족해

2. 
CHEF , PUPPET 등의 상태관리 도구를 쓰자! 
즉, 설정파일로 관리를 해서 이 설정파일을 돌리는거지 상태관리 도구를 써서!

3.
한 서버에 다른 버전 여러개 설치는 어떻게할까?
러닝커브가 너무 높네..
코드로 작성하면 협업도 하고 버전관리도 되겠네?

4.
가상머신을 만들자! 각자 독립적으로! MYsql , Jenkins 등등!
한서버에 여러개 설치도 쉽네.
근데 왜이렇게 느림?
처음부터 다시 셋팅하려면...? 처음 셋팅한 사람의 정보를 알아야함.. 레전드.. 공유도 어려움

5. 
가상 머신을 만드는게 아니라 나누는거다. 파일 디렉토리 프로세스 등등 !!! 걍 프로그램을 같은곳에있는데 뭐 다르게!!분리
CPU.MEMORY.I/O도 그룹별로 제한 !  ( 리눅스의 커널 기능을 사용해서 )
리눅스 기능을 이용한 빠르고 효율적인 서버관리

어렵네....... 이론은 괜찮은데 말이지.. 어떻게해야할까?


두두등장 ! '도커'
설정파일을 이용하여 컨테이너를 만드는것


# 도커란

VM 과 Docker 차이! Hypervisor Guest OS가 Overhead 부분이다 !
그래서 너무 느리다 도커는 이 부분이 없기 때문에 성능에 문제가 없다.

좀 더 추가로 설명하면... Hypervisor 이게 Guest OS 즉, 가상머신을 생성해주기 위한 프로그램인데 이게 되게 성능을 안좋게해

도커의 특징! 확장성/ 이식성 ! 도커가 설치되어있으면 어디서든 컨테이너를 실행할 수 있어!
표준성 : 도커를 사용하지않으면 ruby, nodejs. go.php 으로 만듣ㄴ 서비스의 배포방식은 제각각 다르다 .

도커 이미지 ? 도커 컨테이너를 실행하기 위한 압축 파일이라고 생각하면된다
도커 파일 이라는 것을 이용해서 이미지를 생성한다.

이미지 저장소에 이미지를 저장하고 그 저장소에서 이미지를 갖고와서 ! 컨테이너로!

설정 관리 !
설정은 환경변수로 제어함. MYSQL_PASS=password 와 같이 컨테이너를 띄울때 환경변수를 같이 지정
하나의 이미지가 환경변수에 따라 동적으로 설정파일을 생성하도록 만들어져야함

자원 관리 : 컨테이너는 삭제 후 새로 만들면 모든 데이터가 초기화됨
오픈소스기 때문에 회사에 종속되어 있지가 않다


이미 유명한 것들은 이미지 저장소에 있고 우리가 만들 프로그램은 이미지를 만들어서 컨테이너로 만들고 실행시키면된다!

1번서버에 애플리케이션이 떠있고 2번 서버에 mysql 떠있으면 연결해줘야하는데
이 어디 서버에있는지 찾아주는 '서비스 디스커버리' 기능도 있다.


# 도커 실무

설치
curl -s https://get.docker.com/ | sudo sh : 명령어를 입력하고 패스워드를 입력하면 리눅스 배포판에 따라 자동으로 최신버전의
도커를 설치
sudo usermod -aG docker ubuntu : ubuntu 유저 권한 추가 
유저 모드를 변경해서 그룹을 설정
![image](https://user-images.githubusercontent.com/86240112/133890584-f7667083-fd05-49c7-afde-9ce7c6a31be6.png)

프로세스 상태를 보는 용도 : ps aux
ps aux | grep docekr 

https://velog.io/@weekbelt/%EB%8F%84%EC%BB%A4%EB%8D%B0%EB%AA%ACDocker-Daemon

도커는 도커 클라이언트, 도커 데몬(host) 클라이언트 서버 구조로 되어있따.

docker run ubuntu:20.04
자 - 여기서 run 명령어를 사용하면 사용할 이미지가 저장되어 있는지 확인하고 없다면 다운로드(pull) 한 후 컨테이너를
생성(create) 하고 시작(start) 합니다. 

컨테이너는 정상적으로 실행됐지만 뭘 하라고 명령어를 전달하지 않았기 때문에 컨테이너는 생성되자마자 종료됩니다.
컨테이너는 프로세스이기 때문에 실행중인 프로세스가 없으면 컨테이너는 종료됩니다.

docker run --rm -it ubuntu:20.04 /bin/sh 우분투 이미지 컨테이너를 실행하고 그 우분투의 쉘 접속 

![image](https://user-images.githubusercontent.com/86240112/133894441-e7f65f1d-7a85-4f11-8520-62b15a82371c.png)
![image](https://user-images.githubusercontent.com/86240112/133894450-7b3cb151-230e-4baa-94d6-af078e73e0ef.png)

docker run --rm -p 5678:5678 hashicorp/http-echo -test="hello world"
나의 5678 포트에서 hashicorp/http-echo 컨테이너의 5678 포트

curl localhost:5678

exec 명령어 : run 명령어와 달리 실행중인 도커 컨테이너에 접속할 때 사용하며 컨테이너 안에 ssh server등을 설치하지 않고
exec 명령어로 접속한다.

![image](https://user-images.githubusercontent.com/86240112/133894957-7607e8cc-8f54-4f7e-8732-45fe0355a6d9.png)


# 도커 기본 명령어 - ps, stop, rm, logs, images 

프로세스 
docker ps : 쭉 나오는데 IMAGE 에 mysql, redis 등등 나옴. 
docker ps -a : 중지된 것도 전부 나온다.

docker stop 컨테이너 이름 or ID
docker stop 00dc5634634c0a 

docker rm : 중지된 컨테이너가 삭제가 안될수있다. 즉 찌꺼기가 있음 그래서 삭제를 해줘야함
docekr rm 00dc5634634c0a

띄어쓰기로 여러개 가능  docekr rm 00dc5634634c0a 00dc5634141a0e

Mysql 에 대한 로그를 알아볼까?
docekr logs 00dc5634634c0a
하면 mysql에 대한 로그들이 쭉 나옴!!

docker logs -f 00dc5634634c0a : 이렇게 -f 옵션을 주면 실시간으로 대기하면서 로그가 나오면 나오게한다.

docker images : 있는 이미지를 쫙 나오게한다. PC에 저장되어있는 이미지들이다. 만약 없으면 pull로 다운로드가 된다!
run할때 자동으로 없으면!! pull 이 실행됨

docekr rmi 이미지명 : 컨테이너가 아닌 이미지를 삭제할떄 !

# 도커 기본 명령어 - volume : 데이터가 유실되지않도록

docker ps
docekr stop mysql
docker rm mysql 
docekr run -d -p 3306:3306

이렇게 중지하고 지우고 다시 run 할때 기존에 있었떤 데이터는 어떻게 될까?

조금 전에 만들었던 데이터는 다 없어진 것! 컨테이너가 종료될때 사라진것 
그럼 -v(volume) 옵션을 주면 데이터가 없어지지않음!


# 도커 컴포즈 (docker compose)

명령어들이 굉장히 조심스럽고 띄어쓰기나 글자나 하나하나 것들을 제대로 입력안하면 안되기에
도커 컴포즈가 있는 것. ( 프로그램 : 도커컴포즈 )

![image](https://user-images.githubusercontent.com/86240112/133914935-b7e2e1d1-d563-4623-a276-6d50c7e00610.png)


docker-compose up : 실행
docker-compose down  : 중지

쉘스크립트로 직접 설정했던 것을 docker-compose.yml에 저장해서 실행하면 됨.
docker-compose.yml 에 있는 곳에 docker-compose up 하면 yml 을 읽어서 컨테이너를 읽음!

restart : 만약 컨테이너가 죽게되면 항상 도커가 자동으로 !
einvironment : 환경변수 


# 도커 이미지 만들기

이미지란 : 프로세스가 실행되는 파일들의 집합(환경) 
이미지가 합쳐져서 또 다른 이미지를 만들수 있음.

Base Image : 우분투, Mysql  - 원본테이터를 수정할순없지만 데이터를 추가 삭제를 할 수 있다.

docker images : 많은 이미지가 나온다

docker run -it --name git ubuntu:lastest bash : 도커 실행을 할거고 이름은 git으로할거고 image는 ubuntu고 bash를 곧바로 실행
이제 우분투 컨테이너에 들어간거고!

git을 쳐서 git이 있는지확인하고
없으면 apt 을쳐서 git을 설치!

docker commit git ubuntu:git : git이라는 컨테이너를 ubuntu:git 이라고 바꾼것
docker run -it --name git2 ubuntu:git bash

여기서 만약 git 을 쳐보면!?
git이 포함되어있기에 git 이 있는 컨테이너다!!!!

새로운 상태를 이미지로 저장한다는 뜻이야. 뭔말인지 알쥐!?

docker images 
하고 나서 한줄씩 딱 나오는데

/ 기준으로 왼쪽은 아이디!

만들어보자!!

IDE 에 Dockerfile 만들고!

FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y git

docker build -t ubuntu:git-dockerfile .

이렇게 도커파일로 관리를 하게 되면 최초에 어떻게 설치가 되었는지 기록으로 확인을 할수 있따는 장점이 있다.

정리!!!!
그러니까 예를들어보자.

우리는 컨테이너를 실행하고 거기에 실행을 해서 git을 깔아!
그리고 그걸 commit 으로 이름을 바꾸고 이제 실행하면 그 이미지는 git이 깔려있는!
이미지인거야. 

그럼 이건.. 컨테이너에 접속해서 (sh) 그 누군가가 git을 깔았다는 그 히스토리는 자기만알잖아.

그렇기에 docker file을 미리 만들어 놓고 그 도커파일을 이용해서 build ! 를하면 
dockerfile에 히스토리도 알기때문에 좋다 이거지!!


# 도커이미지만들기 - 웹애플리케이션

mkdir web
npm init - 초기화
npm ifastify --save

app.js 에 코드 복사 
node app.js 해서 서버를 실행

이제 이 디렉토리에다가 
dockerfile 을 만들자


![image](https://user-images.githubusercontent.com/86240112/133917459-4c8813f1-49ec-416a-a6fb-6c33e32cb196.png)
![image](https://user-images.githubusercontent.com/86240112/133917462-d6fa7f18-948e-46d0-98b9-50397392a2e1.png)
![image](https://user-images.githubusercontent.com/86240112/133917468-c44765cd-aed8-4018-96ac-87e57c452774.png)
![image](https://user-images.githubusercontent.com/86240112/133917472-1ca0fb39-f13e-4f4f-8781-d2f5071f8852.png)
![image](https://user-images.githubusercontent.com/86240112/133917474-3201b9aa-9ce4-417d-9940-5ee3daef0bdd.png)

도커 이미지를 만들 때, 캐시를 쓴다. 즉슨 한번 만들어본 이미지는 캐시가 먹어서 빠르다.

# 도커 허브 ( 이미지 저장소 )

이미지저장명령어

docker login
docker push {ID}/example : 내가만든 이미지를 저장소에 저장!
docker pull  : 갖고오는거

docker hub 

나의 PC에서 만들어진 이미지를 도커허브에 저장하고 거기에 push 와 pull을 이용하서 공유를하는거쥐
간단간단!! 이러한 관계 즉, 프로토콜을 설정해놧움













































