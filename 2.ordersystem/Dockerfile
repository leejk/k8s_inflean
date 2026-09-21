# 필요프로그램 설치
FROM eclipse-temurin:17-jdk AS stage1
# 파일 복사 (stag1 이라는 가상의 리눅스 공간의 app 폴더에 copy)
WORKDIR /app
COPY gradle gradle
COPY src src
COPY build.gradle .
COPY settings.gradle .
COPY gradlew .
# 빌드
RUN chmod +x gradlew
# bootJar 생성
RUN ./gradlew bootJar

# 두번째 스테이지 (가상의 stage2)
# FROM eclipse-temurin:17-jdk
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
# jar 만 복사하여 여기 스테이지에 있는 java와 jar로 이미지 만든다
COPY --from=stage1 /app/build/libs/*.jar app.jar

# 실행 : CMD 또는 ENTRYPOINT를 통해 컨테이너를 배열 형태의 명령어로 실행
# java -jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
