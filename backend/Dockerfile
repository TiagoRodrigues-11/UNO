# Development stage - Optimized for Spring Boot development
FROM gradle:8.5-jdk21-alpine

WORKDIR /app

# Copy only gradle configuration files first (better layer caching)
COPY gradlew gradlew.bat settings.gradle build.gradle ./
COPY gradle/ gradle/

# Download dependencies (this layer will be cached if gradle files don't change)
RUN ./gradlew dependencies --no-daemon 2>&1 | grep -v "^Download"

# Copy source code
COPY src/ src/

# Expose port for Spring Boot
EXPOSE 8080

# Make gradlew executable and run Spring Boot with file watching
# spring-boot-devtools enables automatic restart on file changes
# --no-daemon prevents gradle daemon (better for Docker)
CMD ["./gradlew", "bootRun", "--no-daemon", "--continuous"]
