# Docker memo
Docker어린이의 공부 노트!  
🐣🐤삐약삐약
  
-------------------------------------------------------------  
 기본 흐름 : ./Dockerfile -> Docker image -> Docker container  
-------------------------------------------------------------  
   
   
 전체 흐름  
 1. source code 작성
 2. ./Dockerfile 작성
 3. docker build -t ~~~  # 이미지 생성 완료  
 ```docker build --tag scinet-tmp .```  # 이미지 이름은 scinet-tmp, 끝에 .은 현재 디렉터리에서 Dockerfile을 찾도록 Docker에 지시  
 5. docker push ~~~  # 서버에 전송
 6. docker pull ~~~  # 서버에서 다운
 7. docker run -d -it -p ~~~  # 명령어 자유롭게, 컨테이너 생성되서 돌아감  
 ```docker run scinet-tmp```  
  
  
[docker docs](https://docs.docker.com/engine/reference/builder/)  
[docker docs python example](https://docs.docker.com/language/python/build-images/)
    
[Guide](https://learn.microsoft.com/ko-kr/visualstudio/docker/tutorials/docker-tutorial)
  
[guide2-1](https://tech.cloudmt.co.kr/2022/06/29/%EB%8F%84%EC%BB%A4%EC%99%80-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%9D%98-%EC%9D%B4%ED%95%B4-1-3-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EC%82%AC%EC%9A%A9%EB%B2%95/)    
[guide2-2](https://tech.cloudmt.co.kr/2022/06/29/%EB%8F%84%EC%BB%A4%EC%99%80-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%9D%98-%EC%9D%B4%ED%95%B4-2-3-%EB%B3%BC%EB%A5%A8%EA%B3%BC-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/)  
[guide2-3](https://tech.cloudmt.co.kr/2022/06/29/%EB%8F%84%EC%BB%A4%EC%99%80-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%9D%98-%EC%9D%B4%ED%95%B4-3-3-docker-image-dockerfile-docker-compose/)  
   
 windows에서 linux에서 추출한 이미지 실행  
 https://trytoso.tistory.com/1587
   
   
   Do not confuse RUN with CMD. RUN actually runs a command and commits the result; CMD does not execute anything at build time, but specifies the intended command for the image.
   
   
# Dockerfile 만들기  
* FROM : 운영체제 이미지, 베이스 이미지 지정  
* RUN : 실행할 명령어  
* COPY  : 파일 복사  
* ENV : 환경 변수 설정  
* ADD : 파일/디렉토리 추가  
* USER : 사용자 지정  
* WORKDIR : 작업 디렉토리  
* ARG : Dockerfile안 변수  
* LABEL : 라벨 설정  
* EXPOSE : 컨테이너 공개포트 지정, 컨테이너가 대기하는 포트 알려줌  
* ENTRYPOINT : 컨테이너 실행 명령 (CMD와 무슨차이?)  
* VOLUME : 볼륨 마운트   
* ONBUILD : 빌드 완료 후 실행되는 명령  
   (다른 이미지 생성 시 이 Dockerfile로 생성한 이미지를 참고하면 그제서야 ONBUILD
   명령어 실행되는 것)
* STOPSIGNAL : 종료 시그널 설정  
* HEALTHCHECK : 컨테이너 상태 체크  
* SHELL : 기본 쉘 설정

   
<br/>
<br/>

# Docker Image 만들기  
docker image : container를 만드는데 사용되는 read-only 템플릿  
컨테이서 실행에 필요한 파일과 설정값 등을 포함하고 있는 Dockerfile을 만든 후 Dockerfile을 빌드하여 이미지를 만듬.  
  
docker image 생성  
``` docker image build -t example/echo:latest```  
-t 옵션은 이미지명 지정에 사용
   
docker image none 일괄 제거  
```docker rm $(docker ps --filter status=exited -q)```  
  
# Docker Container 만들기  
 docker build  
 ```docker build --help```  
 ``` docker build -t getting-started .```  
docker build 명령의 끝에 있는 .는 현재 디렉터리에서 Dockerfile을 찾도록 Docker에 지시.
  
  
--------------------------------------------------------------------------  
 docker container life-cycle   
 생성(create) -> 시작(start) -> 실행(run) -> 중지(stopped) -> 삭제(deleted)  
--------------------------------------------------------------------------  
  
process 도는지 확인, container ID확인  
```docker ps (-a)``` 
     
docker run  
 ```docker run -dp 800:800 getting-started```  
 --name : container 별명 지어주기. container id일일이 안찾아도 되서 편함.  
 -d : 백그라운드에서 분리된 모드로 컨테이너를 실행 중임을 나타냄  
 -e : docker container 환경변수 설정, Dockerfile의 ENV설정 덮어씀  
 ``` docker run -e FOO=bar python:3.8-alpine env```  
   
 -i : 사용자가 입출력 할 수 있는 상태  
 -t : 가상 터미널 환경을 에뮬레이션 함  
 (-it : 컨테이너를 종료하지 않은체로, 터미널의 입력을 계속해서 컨테이너로 전달하기 위해서 사용)  
 -p : 호스트 포트 3000과 컨테이너 포트 3000 간에 매핑을 만듬  
 포트 매핑이 없으면 애플리케이션에 액세스할 수 없음  
 -v : host, container간 volumne설정. host시스템 특정 경로를 container 시스템 특정 경로로 mount해줌  
 host 컴퓨터의 현재 디렉터리를 container의 /etc경로로 mount한 뒤 뒤에 명령어 수행  
 ```docker run -v `pwd`:/etc python:3.8-alpine cat /etc/test.txt```  
   
 -w : Working directory inside the container  
 작업 디렉터리를 /etc로 변경  
 ```docker run -w /etc python:3.8-alpine pwd```   
   
 --shm-size=8G (컨테이너 내부 통신 시 공유메모리 조절. default 4mb 밖에 안된다네?)  
   
 
container 중지  
```exit``` 치거나 Ctrl+C 누르기  
```docker stop <container-id>``` # 그동안 하던 작업들 완료하고 컨테이너 중지  
```docker kill <container-id>``` # 작업 기다리지 않고 강제 중지
  
container 제거  
```docker rm <container-id>```  
  
멈춘 container 일괄 제거  
```docker rm $(docker ps --filter status=exited -q)```  
  
멈춘 container 다시 실행  
``` docker restart <container-id>```  

docker container 에 접속  
```docker attach <container-id>```  

<br/>
<br/>

## docker container command line based (실험 중)  
docker pull continuumio/miniconda3  
```
(
docker run \
-it \
--name ripdet \
-w /home/sdh/mmdetection_nc/ \
-v $PWD:/home/sdh/mmdetection_nc/ \
continuumio/miniconda3
)

conda activate /home/sdh/mmdetection_nc/venv
apt-get update
apt-get -y install libgl1-mesa-glx
pip install python-dateutil

python ./NIA_workdir_50p/test_NIA_newcon.py 
exit
```  

  
* 도커 호스트에서 컨테이너로 파일 전송  
```docker cp /~경로~/text123.txt 225051b687b3:/home```  
 
 
* 도커 컨테이너에서 생성한 파일/폴더를 도커 밖에서 변경하려고 할 때 permission denied error  
[guide](https://sweethoneybee.tistory.com/28)  
컨테이너에서 생성한 파일owner가 root라서 root 권한으로 파일 제어가 가능하다 : sudo로 하면 처리됨.  
sudo권한 안쓰고 해결하는 방법 : ???  
(참고로 docker에서 생성된 파일은 host에서 root으로 잡히는데, dockerfile에서 user를 새로 만드는 방법이나 docker container 내부에서 chown 자신uid 파일명을 통해 변경할 수 있다고 함)  

  
