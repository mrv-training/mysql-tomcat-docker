FROM tomcat:9.0.70-jdk11-corretto-al2

COPY webapps/ /usr/local/tomcat/webapps/
COPY conf/ /usr/local/tomcat/conf/

EXPOSE 8080
EXPOSE 8443

CMD ["catalina.sh", "run"]
