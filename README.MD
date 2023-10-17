To build docker images on Local and run them, Run the following on COmmand Prompt:

    docker network create mynetwork

    In DB directory: docker build -t sqldb .
    docker run --name mysql-container -p 3307:3306 --network mynetwork -d sqldb

    In Host directory: docker build -t host . 
    In Request directory: docker build -t request .  
    In RequestAutomate directory: docker build -t requestautomate .  

    docker run -it --rm -d --name uploader --network mynetwork -p 5000:5000 host

    Manual Input:
    docker run -it --rm --name listener --network mynetwork  request
    Automation:
    docker run -it --rm --name automate --network mynetwork  requestautomate


From DockerHub:
    docker stop uploader (for mysql-container, listener too)
    //docker rm uploader (for mysql-container, listener too)
    docker rmi deepikapavundoss/nssf1-sqldb (for deepikapavundoss/nssf1-request, deepikapavundoss/nssf1-host)
    docker pull deepikapavundoss/nssf-db
    docker pull deepikapavundoss/nssf-request
    docker pull deepikapavundoss/nssf-host
    docker network create mynetwork
    docker run --rm --name mysql-container -p 3307:3306 --network mynetwork -d deepikapavundoss/nssf-db
    docker run -it --rm -d --name uploader --network mynetwork -p 5000:5000 deepikapavundoss/nssf-host
    docker run -it --rm --name listener --network mynetwork deepikapavundoss/nssf-request
    docker run -it --rm --name automate --network mynetwork deepikapavundoss/nssf-automate



Grafana datasource:
    //host: host.docker.internal:3307
    host: localhost:3307
    Database: nssf
    User: root
    Password: password

Grafana dashboard:
    select datetime as time, value as val from nssf.Network

