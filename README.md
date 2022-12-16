# -
Docker를 써봅시다 삐약삐약

[Guide](https://learn.microsoft.com/ko-kr/visualstudio/docker/tutorials/docker-tutorial)
  
  
첫 container? process ? 지정  
port 80은 쓰고잇대서 800으로 (임의로)해봄  
```docker run -d -p 800:800 docker/getting-started```  
* -d 백그라운드에서 분리 모드로 컨테이너를 실행.
* -p 80:80 호스트의 포트 80을 컨테이너의 포트 800에 매핑.
* docker/getting-started 사용할 이미지를 지정.
<br/>

  
process 도는지 확인, container ID확인  
```docker ps (-a)```
<br/>
<br/>
container 중지  
```docker stop <container-id>```
<br/>
<br/>
container 제거  
```docker rm <container-id>```
  
  
 docker build
 ``` docker build -t getting-started .```  
docker build 명령의 끝에 있는 .는 현재 디렉터리에서 Dockerfile을 찾도록 Docker에 지시.
