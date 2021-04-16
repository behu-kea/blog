# Tomcat



## Installing tomcat



```
sudo yum install wget
cd ~
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.44/bin/apache-tomcat-9.0.44.tar.gz
sudo mkdir /opt/tomcat
sudo tar xvf apache-tomcat-9*tar.gz -C /opt/tomcat --strip-components=1
```



## Running and stopping tomcat

You might need to be root to run the following line. If you do write 

```bash
sudo su
```



To start the tomcat server

```bash
cd /opt/tomcat/bin/
./startup.sh
```



To stop the tomcat server

```bash
cd /opt/tomcat/bin/
./shutdown.sh
```



Now you can go to http://server_IP_address:8080

