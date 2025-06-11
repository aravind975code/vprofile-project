FROM maven:3.9.9-eclipse-temurin-21-jammy AS BUILD_IMAGE
WORKDIR /vprofile-project
RUN git clone https://github.com/hkhcoder/vprofile-project.git  . && \
    git checkout containers
ENV MAVEN_OPTS="-Xmx2048m"
# Build project
RUN mvn clean install

# Runtime Stage
FROM tomcat:10-jdk21

# Remove default webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy built WAR file from build stage
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose port
EXPOSE 8080
