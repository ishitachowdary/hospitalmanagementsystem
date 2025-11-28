# -------- BUILD STAGE --------
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app

# copy pom and source
COPY pom.xml .
COPY src ./src

# build jar (skip tests to speed up)
RUN mvn -q -DskipTests package

# -------- RUNTIME STAGE --------
FROM eclipse-temurin:17-jdk-jammy
WORKDIR /app

# !! adjust jar name if yours is different !!
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]