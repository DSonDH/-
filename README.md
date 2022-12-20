# Docker memo
Docker를 써봅시다 삐약삐약
  
 기본 흐름 : ./Dockerfile -> Docker image -> Docker container  
 (데 container로 image 생성도 가능)
   
   
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
   
   
   
   
첫 container? process ? 지정  
port 80은 쓰고잇대서 800으로 (임의로)해봄  
```docker run -d -p 800:800 docker/getting-started```  
* -d 백그라운드에서 분리 모드로 컨테이너를 실행.
* -p 80:80 호스트의 포트 80을 컨테이너의 포트 800에 매핑.
* docker/getting-started 사용할 이미지를 지정.
<br/>
  
   
docker image : container를 만드는데 사용되는 read-only 템플릿  
컨테이서 실행에 필요한 파일과 설정값 등을 포함하고 있는 Dockerfile을 만든 후 Dockerfile을 빌드하여 이미지를 만듬.  
  
docker image 생성  
``` docker image build -t example/echo:latest```  
-t 옵션은 이미지명을 지정할 때 사용
   
docker image <none> 제거  
```docker rm $(docker ps --filter status=exited -q)```  
  
  
process 도는지 확인, container ID확인  
```docker ps (-a)``` 
  
  
 docker build  
 ```docker build --help```  
 ``` docker build -t getting-started .```  
docker build 명령의 끝에 있는 .는 현재 디렉터리에서 Dockerfile을 찾도록 Docker에 지시.
  
  
 docker run  
 ```docker run -dp 800:800 getting-started```  
 -d 매개 변수는 백그라운드에서 분리된 모드로 컨테이너를 실행 중임을 나타냅니다.  
 -p 값은 호스트 포트 3000과 컨테이너 포트 3000 간에 매핑을 만듭니다.  
 포트 매핑이 없으면 애플리케이션에 액세스할 수 없습니다.
  
  
container 중지  
```docker stop <container-id>```
<br/>
<br/>
container 제거  
```docker rm <container-id>```  
  
멈춘 container 제거  
```docker rm $(docker ps --filter status=exited -q)```  
  
