## Prerequisite
* Intellij latest - https://www.jetbrains.com/idea/download/#section=mac
* Docker Desktop - https://hub.docker.com/editions/community/docker-ce-desktop-mac/ 

Note: After you clone this repository, you may want to import airflow code as module so that intellij do not give you errors in those files. Follow [this](https://drive.google.com/a/thoughtworks.com/file/d/1VmFpmOVta7u0qqcMT2cnTm53RKS-9uuD/view?usp=sharing) video to do so.

## Command to build jar
`sbt clean assembly`

## Command to build and deploy containers
`cd docker`
`docker-compose down && docker-compose build && docker-compose up --force-recreate`

Note: Make sure docker is running in your machine. if not installed, follow https://docs.docker.com/docker-for-mac/install for mac
### This will deploy following containers
* spark master with two worker nodes (spark is in stand alone mode). spark master will also contain livy server in it
* postgres db for airflow metadata
* airflow webserver
* aiflow scheduler

### How to access these services?
* spark master web ui - localhost:8080
* spark history server - localhost:18080
* livy server - localhost:8998
* airflow web ui - localhost:8090

### Add livy connetion in airflow to run the dag
    1. Set the Conn Id as "livy_http_conn"
    2. Set the Conn Type as "http"
    3. Set the host as spark-master
    4. Set the port as 8998
    5. Save
