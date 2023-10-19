# Migration To The Cloud With Containerization 1 - Docker

**Step 0 - Prerequisites**
---

- Install Docker.

*As of the time of this doc, Docker is having some issues being deployed on RHEL servers. Use ubuntu instead.*

*Docker installation steps can be found [here](https://docs.docker.com/engine/install/ubuntu/)*

**Step 1 - Creating MySQL Container For Tooling App Backend**
---

- Create a network dedicated for the MySQL database and tooling application we would containerize on docker.

*The docker network allows artifacts in that network communicate with each other*

```
docker network create --subnet=172.18.0.0/24 app_network_tooling
```

- After the network has been created, create an environment variable that would be used to store the root user password. Run `export MYSQL_PW=<yourPassword>`.

- Run the command below to pull the MySQL image and run the container.

```
docker run --network app_network_tooling -h mysqlserverhost --name=mysql-server -e MYSQL_ROOT_PASSWORD=$MYSQL_PW -d mysql/mysql-server:latest
```