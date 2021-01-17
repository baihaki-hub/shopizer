FROM openjdk:8-jdk-alpine
RUN ls
RUN ls .
COPY . /usr/src/project/
RUN ls /usr/src/project/
RUN ls /usr/src/project/sm-shop
#COPY ./sm-shop/target/ROOT.war /usr/src/project/
#ADD ./sm-shop/target/SALESMANAGER.h2.db /usr/src/project/
#COPY ./sm-shop/target/files/ /usr/src/project/files/
WORKDIR /usr/src/project
RUN ./mvn install
RUN ls /usr/src/project/sm-shop/target

FROM tomcat:9.0.10-jre8

RUN rm -rf /usr/local/tomcat/webapps/*
RUN mkdir -p /usr/local/tomcat/files

COPY --from=0 /usr/src/project/sm-shop/target/ROOT.war /usr/local/tomcat/webapps/ROOT.war
COPY --from=0 /usr/src/project/sm-shop/SALESMANAGER.h2.db /usr/local/tomcat/
COPY --from=0 /usr/src/project/sm-shop/files/ /usr/local/tomcat/files/

ENV JAVA_OPTS="-Xmx1024m"

CMD ["catalina.sh", "run"]

EXPOSE 8080