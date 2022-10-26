FROM manokrish12345/centos-7:jdk-11-maven-3.5

RUN mvn clean install

ENTRYPOINT [ "java", "-jar", "./target/SecondDemoProject-0.0.1-SNAPSHOT.jar", "-Dspring.profiles.active=dev", "--spring.config.location=application.properties"]