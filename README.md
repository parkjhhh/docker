# Docker에 jar파일 배포하고 Docker HUB에 등록하기

목표 : VScode를 이용해 dockerfile에 기존에 가지고 있던 jar파일을 실행시키는 docker image를 생성하고, 이를 컨테이너에 올린 후 docker hub에 push하기 

## **step1**
**VScode와 Ubuntu 연동시키기**

✔️VScode의 Extension에서 Remote - SSH  v0.118.0 다운로드 받기
![Image](https://github.com/user-attachments/assets/97648a9f-b5b1-4bf1-8a92-24227de4df80)
✔️Remote explore에 들어가서  ubuntu와 연동한 새로운 창 열기<br>
![Image](https://github.com/user-attachments/assets/94e5f989-42a6-4761-8761-e9e1f0effb9b)<br>
✔️ubuntu 비밀번호 입력<br>
![Image](https://github.com/user-attachments/assets/8ec9e034-a190-40da-a445-333d755dd31d)

<br><br>

## **step02**
**dockerfile 만들기**

✔️dockerfile을 만들 경로를 만들어준 후 dockerfile이름의 new file을 생성해주면 자동적으로 dockerfile생성
<br>
✔️Remote explore에 들어가서  ubuntu와 연동한 새로운 창 열기
<br>
✔️ubuntu 아래내용 입력
![Image](https://github.com/user-attachments/assets/ef81c2c9-ee2d-43cc-90aa-13f16d90d772)
```
# base image: eclipse-temurin 17 JRE
FROM eclipse-temurin:17-jre-alpine
# JAR 파일을 컨테이너의 /app 디렉토리로 복사
COPY cs.jar /app/cs.jar
# 컨테이너 실행 시 JAR 파일을 실행
CMD ["java", "-jar", "/app/cs.jar"]
```

## **step03**
**docker HUB에 등록하기**<br>

✔️docker 컨테이너 NAME 확인후 태그를 설정한 후 커밋하기
```
jihye@ubuntu:~/dockerfile$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                            PORTS     NAMES
ea4871a738f7   4303d70aa21b   "/__cacert_entrypoin…"   2 minutes ago   Exited (130) About a minute ago             beautiful_payne

jihye@ubuntu:~/dockerfile$ docker commit beautiful_payne parkjihye1226/springapp:1.0
sha256:44ddb0c35593ddffd28200372d20c330c87cf804a8e58b00850b68e6b00815e4
jihye@ubuntu:~/dockerfile$ docker images
REPOSITORY                TAG       IMAGE ID       CREATED              SIZE
parkjihye1226/springapp   1.0       44ddb0c35593   About a minute ago   208MB
parkjihye1226/springapp   latest    418296f3a469   About a minute ago   208MB
<none>                    <none>    366dc4be02a4   About a minute ago   208MB
<none>                    <none>    1b4fe55e02c9   2 minutes ago        208MB
```

✔️push하기
```
jihye@ubuntu:~/dockerfile$ docker push parkjihye1226/springapp:1.0
The push refers to repository [docker.io/parkjihye1226/springapp]
761b51948cf7: Pushed 
4975644a971e: Pushed 
872b4640f1c3: Mounted from library/eclipse-temurin 
b1bdb6e103f3: Mounted from library/eclipse-temurin 
30e00ad713b7: Mounted from library/eclipse-temurin 
1cd01d0f38a4: Mounted from library/eclipse-temurin 
08000c18d16d: Mounted from library/eclipse-temurin 
1.0: digest: sha256:2a6cd340e3ea36e4236c74f4933c816bdee51045c7808a2f55e4f568ca9129cd size: 1786
```
