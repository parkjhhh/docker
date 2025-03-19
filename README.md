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
![Image](https://github.com/user-attachments/assets/94e5f989-42a6-4761-8761-e9e1f0effb9b)
✔️ubuntu 아래내용 입력


```
# base image: eclipse-temurin 17 JRE
FROM eclipse-temurin:17-jre-alpine
# JAR 파일을 컨테이너의 /app 디렉토리로 복사
COPY cs.jar /app/cs.jar
# 컨테이너 실행 시 JAR 파일을 실행
CMD ["java", "-jar", "/app/cs.jar"]

```
