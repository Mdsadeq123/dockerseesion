
# Stage 1: Build Spring Boot application

FROM eclipse-temurin:21-jdk AS builder

WORKDIR /app

COPY .mvn/ .mvn/

COPY mvnw pom.xml ./

RUN chmod +x mvnw

RUN ./mvnw -B -ntp dependency:go-offline

COPY src ./src

RUN ./mvnw -B -ntp clean package -DskipTests


# Stage 2: Runtime image

FROM eclipse-temurin:21-jre

WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
