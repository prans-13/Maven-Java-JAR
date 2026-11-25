mkdir -p /c/DockerProjects/custom-nginx
cd /c/DockerProjects/custom-nginx


FROM redis:latest
CMD ["redis-server"]

FROM tomcat:9.0-jdk17-temurin
COPY app/target/*.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]


FROM python:3.12-alpine
WORKDIR /app
COPY app.py .
EXPOSE 5000
CMD ["python", "app.py"]


FROM nginx:latest
COPY index.html /usr/share/nginx/html/

docker build -t carimage1234 . 
docker images
docker run -d --name carcontainer -p 8080:8080 carimage1234
docker ps
docker login
docker tag carimage1234 chandrayani2007/carimage1234:latest
docker push chandrayani2007/carimage1234:latest

FROM openjdk:17
WORKDIR /app
COPY Hello.java .
RUN javac Hello.java
CMD ["java", "Hello"]

docker --version
docker pull mysql:8.0
docker pull wordpress:latest
mkdir Library-Management
cd Library-Management
notepad docker-compose.yml
docker network create library-network
docker compose up -d
docker compose ps

services:
  db:
    image: mysql:8.0
    container_name: library-db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root123
      MYSQL_DATABASE: library
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin123
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - library-network
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-uroot", "-proot123"]
      interval: 10s
      timeout: 5s
      retries: 5

  wordpress:
    image: wordpress:latest
    container_name: library-wordpress
    restart: always
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: admin
      WORDPRESS_DB_PASSWORD: admin123
      WORDPRESS_DB_NAME: library
    depends_on:
      db:
        condition: service_healthy
    networks:
      - library-network

volumes:
  db_data:

networks:
  library-network:
    external: true




script
node {

    stage('1. Git Checkout') {
        echo 'Downloading source code from GitHub'

        git branch: 'master',
            url: 'https://github.com/archanareddyse/OLTRS.git'
    }

    stage('2. Maven Build') {
        echo 'Building project'

        bat 'mvn clean compile'
    }

    stage('3. Testing') {
        echo 'Running tests'

        bat 'mvn test'
    }

    stage('4. Package') {
        echo 'Packaging application'

        bat 'mvn package'
    }

    stage('5. Archive Artifacts') {
        echo 'Archiving generated files'

        archiveArtifacts artifacts: 'target/*.war',
                         fingerprint: true
    }

    echo 'Pipeline completed successfully!'
}


minikube start
kubectl get nodes
kubectl create deployment food-managements --image=wordpress
kubectl get deployments
get pods
kubectl scale deployment food-managements --replicas=4
>kubectl get pods
kubectl get deployments
kubectl expose deployment food-managements --type=NodePort --port=80 --target-port=80
>kubectl get services
minikube service food-managements

*Naigos*
docker pull jasonrivers/nagios:latest
docker run -d --name nagios -p 8999:80 jasonrivers/nagios:latest
docker ps
to run: http://localhost:8999/nagios
Username: nagiosadmin
Password: nagios

Aws:
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


services:
  mysql:
    image: mysql:8.0
    container_name: mysql-db
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: Root@12345
      MYSQL_DATABASE: library_db
      MYSQL_USER: library_user
      MYSQL_PASSWORD: Library@123
    volumes:
      - mysql_data:/var/lib/mysql
    networks:
      - library-network

  wordpress:
    image: wordpress:latest
    container_name: wordpress-app
    restart: unless-stopped
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: mysql:3306
      WORDPRESS_DB_USER: library_user
      WORDPRESS_DB_PASSWORD: Library@123
      WORDPRESS_DB_NAME: library_db
    volumes:
      - wordpress_data:/var/www/html
    depends_on:
      - mysql
    networks:
      - library-network

volumes:
  mysql_data:
  wordpress_data:

networks:
  library-network:
    driver: bridge



Nginx:

services:
  mysql:
    image: mysql:8.0
    container_name: mysql-db
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: Root@12345
      MYSQL_DATABASE: library_db
      MYSQL_USER: library_user
      MYSQL_PASSWORD: Library@123
    volumes:
      - mysql_data:/var/lib/mysql
    networks:
      - library-network

  nginx:
    image: nginx:latest
    container_name: nginx-server
    restart: unless-stopped
    ports:
      - "8080:80"
    networks:
      - library-network

volumes:
  mysql_data:

networks:
  library-network:
    driver: bridge





