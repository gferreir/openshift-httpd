# Httpd Dockerfile instalation to Openshift
 
## This project has the objective to show how to install a Apache server from Dockerfile to deploying on Openshift.

### The Dockerfile
```
1. FROM rhel:latest
2. EXPOSE 8080
3. LABEL io.openshift.expose-services="8080:http"
4. RUN yum install httpd -y && \
    yum clean all -y
5. COPY src/index.html /var/www/html/
6. RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf && \
    chgrp -R 0 /var/log/httpd /var/run/httpd && \
    chmod -R g=u /var/log/httpd /var/run/httpd
7. USER 1001
8. CMD ["usr/sbin/httpd", "-D", "FOREGROUND"]
```
### The explanation

***Line 1*** -> Inform that our project start from a RHEL image base

***Line 2*** -> Specific port 8080 to expose on Openshift enviroment

***Line 3*** -> Metadates to Openshift

***Line 4*** -> Bash commands which run in execution time inside the conatainer with objective install the Apache server

***Line 5*** -> Copying the frontend file which we will expose to Apache path

***Line 6*** -> Configuring Apache port and permissions

***Line 7*** -> Generic userid

***Line 8*** -> Starting Apache server
