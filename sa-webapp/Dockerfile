# Stage 1: Build
FROM maven:3.8.6-jdk-8 AS builder

# Set the working directory
WORKDIR /app

# Copy the pom.xml and install dependencies first (this uses Docker's caching layer)
COPY pom.xml ./
RUN mvn dependency:go-offline

# Now copy the rest of your source code
COPY src ./src

# Run mvn install
RUN mvn install

# Stage 2: Run
FROM openjdk:8-jdk-alpine

# Set the working directory
WORKDIR /app

# Copy the built artifacts from the builder stage
COPY --from=builder /app/target/*.jar ./app.jar

# Should use container ip instead of this
# ENV SA_LOGIC_API_URL http://localhost:5000
EXPOSE 8080

# Command to run your application
ENTRYPOINT ["java", "-jar", "app.jar"]
