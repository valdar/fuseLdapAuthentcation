# Jboss Fuse Ldap authentication lab

This is a simple script that run for you 3 docker images:
- OpenLdap with preloaded users/groups data: valdar/ldapfuseusers:1.0.0
- PhpLdapAdmin (just to have a convenient way to visualize/modifiy ldap contents): osixia/phpldapadmin:0.5.0 
- Jbosse fuse (you need to build this image yourself): https://github.com/paoloantinori/dockerfiles/tree/master/centos/fuse

After that it creates a fabric and update the configuration to authenticate using the openldap server. In this way you will be able to log in in to karaf console or hawtio using credentials stored in openldap:
- user: fuseldap password: fuseldap groupe: admin
- user: notfuseldap password: notfuseldap groupe: none

when the script finish you should be able to check fuse container's local ports with:
```
$ docker ps
CONTAINER ID        IMAGE                        COMMAND                CREATED             STATUS              PORTS                                                                                                                                                  NAMES
9e996ab8e080        fuse6.1:latest               "/bin/sh -c 'service   About an hour ago   Up About an hour    0.0.0.0:49153->44444/tcp, 0.0.0.0:49154->61616/tcp, 0.0.0.0:49155->8101/tcp, 0.0.0.0:49156->8181/tcp, 0.0.0.0:49157->1099/tcp, 0.0.0.0:49158->22/tcp   root                
398aa9b12fc8        osixia/phpldapadmin:0.5.0    "/sbin/my_init"        About an hour ago   Up About an hour    80/tcp, 0.0.0.0:443->443/tcp                                                                                                                           phpldapadmin        
38b8e0885dbf        valdar/ldapfuseusers:1.0.0   "/sbin/my_init"        About an hour ago   Up About an hour    0.0.0.0:389->389/tcp                                                                                                                                   openldap 
```
## NOTE Before launching the script:
Before launching the script you need to build fuse6.1 image yourself by download JBoss Fuse distribution from 

http://www.jboss.org/products/fuse

The build process will extract in the Docker image all the zip files it will find in your working folder. If it finds more than a file it will put all of them inside the  Docker it's going to be created. Most of the time you will want to have just a single zip file. 

## To build your Fuse image:
    # download docker file
	wget https://raw.github.com/paoloantinori/dockerfiles/master/centos/fuse/fuse/Dockerfile
    
    # check if base image has been updated
	docker pull pantinor/fuse
	
    # build your docker fuse image. you are expected to have either a copy of jboss-fuse-full-6.1.0.redhat-379.zip or a link to that file in the current folder.
    docker build -rm -t fuse6.1 .





	

