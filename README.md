sudo apt update
sudo apt-get install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo apt install git -y
sudo apt install nano -y
sudo docker –version

git clone https://github.com/facultyname/maven-web-java.git
cd maven-web-java
ls
nano Dockerfile

FROM tomcat:9-jdk11
COPY target/*.war webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]


FROM openjdk:17
COPY target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]


pwd
sudo docker build -t maven-java-app .
sudo docker images
sudo docker run -d --name app-demo -p 6060:8080 maven-java-app
sudo docker ps
http://18.200.147.174:6060

sudo docker stop app-demo
sudo docker rm app-demo
sudo docker rmi maven-java-app
