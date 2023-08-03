# CI-CD_project

<h1>Angular - Dockerfile</h1>

FROM node:alpine3.14 as build
RUN mkdir -p /app

WORKDIR /app

COPY package.json /app/
RUN npm install

COPY . /app/
RUN npm run build --prod 

FROM nginx:alpine
COPY --from=build /app/dist/angular-frontend /usr/share/nginx/html

<h2> SpringBoot - Dockerfile</h2>

FROM openjdk:17-jdk-alpine
ARG JAR_FILE=target/*.jar
COPY ./target/springboot-backend-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]

<br>
<br>

docker build --tag angular-front .
docker run -d -p 4200:80 --name angular-frontend angular-front

docker build -t springboot-back .
docker run -p 8000:8088 springboot-back
