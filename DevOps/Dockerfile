# Use a base image with OpenJDK 8
FROM openjdk:8-jdk AS BUILD

# Set environment variables for Maven
ENV MAVEN_VERSION=3.5.4 \
    MAVEN_HOME=/usr/share/maven \
    PATH=$PATH:/usr/share/maven/bin

# Install Maven
RUN apt-get update && \
    apt-get install -y wget && \
    wget https://archive.apache.org/dist/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz && \
    tar -xvzf apache-maven-3.5.4-bin.tar.gz && \
    mv apache-maven-3.5.4 /usr/share/maven && \
    rm apache-maven-3.5.4-bin.tar.gz && \
    apt-get remove --purge -y wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set the default working directory
WORKDIR /app

# Add instructions for your app (optional)
 COPY ./game-of-life /app
 RUN mvn clean install

FROM tomcat:9.0
COPY --from=BUILD  /app/gameoflife-web/target/gameoflife.war /usr/local/tomcat/webapps
EXPOSE 8080
CMD ["catalina.sh", "run"]
