# CI-CD_project

<h1>Angular - Dockerfile</h1>

FROM node:alpine3.14 as build <br>
RUN mkdir -p /app

WORKDIR /app

COPY package.json /app/ <br>
RUN npm install

COPY . /app/ <br>
RUN npm run build --prod 

FROM nginx:alpine <br>
COPY --from=build /app/dist/angular-frontend /usr/share/nginx/html

------------------------------------------------------------------------------------------
docker build --tag angular-front .

docker run -d -p 4200:80 --name angular-frontend angular-front

------------------------------------------------------------------------------------------
<h2> SpringBoot - Dockerfile</h2>

FROM openjdk:17-jdk-alpine <br>
ARG JAR_FILE=target/*.jar <br>
COPY ./target/springboot-backend-0.0.1-SNAPSHOT.jar app.jar <br>
ENTRYPOINT ["java", "-jar", "/app.jar"] <br>

------------------------------------------------------------------------------------------
docker build -t springboot-back .

docker run -p 8000:8088 springboot-back

------------------------------------------------------------------------------------------
