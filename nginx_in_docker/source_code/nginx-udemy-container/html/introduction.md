## **nginx as a web server**
* start a nginx container in local machine
* first build the docker image for the application
    * docker build -t nodeapp .
* then spin the container
    * docker run -p 8080:80 nodeapp