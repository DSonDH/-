# -
Docker를 써봅시다 삐약삐약

[Guide](https://learn.microsoft.com/ko-kr/visualstudio/docker/tutorials/docker-tutorial)
  
  
첫 container? process ? 지정  
port 80은 쓰고잇대서 800으로 (임의로)해봄  
```docker run -d -p 800:800 docker/getting-started```  
* -d 백그라운드에서 분리 모드로 컨테이너를 실행합니다.
* -p 80:80 호스트의 포트 80을 컨테이너의 포트 80에 매핑합니다.
* docker/getting-started 사용할 이미지를 지정합니다.

<br/>
<br/>

-
-
-
-
-
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
