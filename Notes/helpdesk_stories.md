# From the Helpdesk story – Docker

**Author**: Adrian Smułkowski

- [LinkedIn](https://www.linkedin.com/in/adrian-smu%C5%82kowski/)

## First clash

Containerized systems are a relatively new solution that is slowly starting to dominate the services market. I myself became interested in Docker in 2020 as a young, relatively inexperienced Helpdesk employee.I started to wonder what administrators were writing when they said *"The container is in an unhealthy state, it will be restarted and if restarting does not help, it will be rebuilt."*

### What is Docker? What was its history?

Docker is a software that was designed to isolate applications using containers. I would describe Docker containers themselves as a box – in this box you can find all the dependencies, add-ons that allow you to run the application in any environment that allows you to install Docker software, so one Dockerfile can be run in another environment, and developers or administrators can be sure that the application will work on another system (whether it's Linux or Windows), regardless of the operating system configuration.

The history of Docker itself begins in 2008 when Solomon Hykes founded dotCloud with the aim of offering a language-independent Platform-as-a-Service offering. The turning point for the company was the release of Docker in March 2013 as an open source solution. For many people, virtual machines and containers seem to be very similar, but there are differences that can be used to distinguish these environments. I will try to explain it in the image below:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/helpdesk_stories/hs_1.png">
</p>

[Image source](https://www.atlassian.com/microservices/cloud-computing/containers-vs-vms)

On the virtual machine, you can see three applications that run on three different virtual machines. Next to it, you can see three containers created with three applications that have been placed in the same environment. The difference is in the kernel - the container engine can start and stop containers, which is similar to the operation of a hypervisor on a virtual machine. There are also differences in the method of isolation and is a technology that has been proven in the world of computing for many years, which is why they are still more popular than containerized environments.

### How did I learn Docker?

I could write down my learning of Docker in several points - in retrospect, I know that that approach was not entirely good. I would now suggest the following approach, combining theory with practice.

1. **Understanding the idea of ​​containers** – in this step I would try to understand what containers are and how I can use them in my current work or when creating my project. If possible, I would take a piece of paper and a pen at this step to pre-design what I want to do.

2. **Preparing the environment** - for learning, I would suggest setting up a virtual machine with Linux and installing Docker.

3. **Practice, practice, practice** – eventually the moment must come to launch the first container. The standard example used is hello-world, but you can go a step further and design a small, simple Dockerfile, which will be a further phase in the development of the project.

### What is Dockerfile?

**Dockerfile** is a configuration file that does not accept any extension - it is simply called Dockerfile. In this file we put what Docker needs to do (specific instructions) that Docker uses to build the image. A Dockerfile starts by specifying a base image and then contains a series of instructions that modify that image by adding new layers. Each instruction creates a new layer in the image.

An example Dockerfile might look like this:

```
# Build phase
FROM golang:1.16-alpine AS build

WORKDIR /src
COPY . .
RUN CGO_ENABLED=0 go build -o /app main.go

# Launch phase
FROM alpine:3.14 AS execute
RUN addgroup -S app && adduser -S app -G app
USER app
COPY --from=build /app /app
CMD ["/app"]
```

This Docker image consists of two phases: the build phase and the launch phase. Here's what each layer does:

### Build Phase

**FROM golang:1.16-alpine AS build** - The FROM instruction tells Docker where to get information about the image used, in this case golang:1.16-alpine as the basis for the build stage. This image contains Go version 1.16 on Alpine Linux.

**WORKDIR /src** - Sets /src as the current working directory in the image.

**COPY . .** - Copies all files from the current directory on the host to the current working directory in the image.

**RUN CGO_ENABLED=0 go build -o /app main.go** - Compiles the main.go file into an executable named /app in the image.

### Launch Phase

**FROM alpine:3.14 AS execute** - This line downloads the alpine:3.14 image as the basis for the execution step. This image contains Alpine Linux version 3.14.

**RUN addgroup -S app && adduser -S app -G app** - Creates a new group and user named app in the image.

**USER app** - Sets app as the current user for the next instructions.

**COPY --from=build /app /app** - Copies the /app executable from the build stage to the execution stage.

**CMD ["/app"]** - Sets the default command that will be run when starting the container on /app, i.e. it starts our compiled application.

---

## Stories about Docker-Compose

### What is Docker-Compose?

Docker-Compose was developed for defining and running multi-container applications in Docker. Docker-Compose takes YAML as its file format. This allows us to easily define multiple containers, networks, volumes, etc. This approach makes it an ideal approach for building and running small applications that require several related containers.

In Docker-Compose, unless we define otherwise, the containers will go to the same bridge network - this network will be created automatically and the containers specified in Docker-Compose will be automatically added to it.

Docker-Compose by default assumes the file name as docker-compose.yml, but there is nothing stopping you from using the `docker-compose -f file_name_in_form_yaml.yml` command

Please remember that on Linux systems, Docker-Compose is not installed automatically and must be installed manually.

### How does Docker-Compose work?

In the case of Docker-Compose, there is functionality that allows you to automatically build images (for example using a previously created Dockerfile) 

I will try to explain it with an example.

In the system, I create a new directory for the project and using any text editor we create the docker-compose.yml file, which will be completed with the following content:

```
version: '3.9'
services:
  webapp:
    build:
      context: ./web_app
      dockerfile: webapp_dockerfile
    ports:
      - "80:80"
  api:
    build:
      context: ./api
      dockerfile: api_dockerfile
    ports:
      - "8080:8080"
```

This seems a bit complicated, but if you look closely you can see some dependencies that may be familiar when working with Dockerfile.

The **version** command indicates the use of a specific Docker-Compose file syntax. For example, the version 3.X format was used, allowing work with both Docker-Compose and Docker Swarm.

In the **services** command we start defining services. Two services were given as an example - webapp, which provides a web application, and API, which I don't think I need to explain this.

The **build** and **context** commands are connected to each other - in the build command we define how the image will be built, and the context indicates the location where the Dockerfile file was placed.

The **ports** command specifies port mapping - here we will use ports 80 and 8080 in the container, which will be redirected to exactly the same ports on the host.

After entering the `docker compose up -d` command, i.e. running the application with all its components, it remains to verify whether the application works as intended.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/helpdesk_stories/docker-compose.png">
</p>

To check whether everything started correctly, just check whether our application runs on port 80

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/helpdesk_stories/curl.png">
</p>

## Where to learn from?

* Polish channel Programator, where you can get many basics (PL) - [link](https://www.youtube.com/watch?v=wFcAa28kjVQ&list=PLkcy-k498-V5AmftzfqinpMF2LFqSHK5n)
* TechWorld with Nana (ENG) - [link](https://www.youtube.com/watch?v=3c-iBn73dDE)
* Learning Docker in 7 steps (ENG) - [link](https://www.youtube.com/watch?v=gAkwW2tuIqE)
* Docker documentation - [link](https://docs.docker.com/)
* Materials about docker on NTHW - [link](https://github.com/notthehiddenwiki/NTHW/tree/nthw/DevSecOps/Docker)
* Practice, practice and even more practice. Developing your projects can develop our skills and give you a new perspective when changing jobs!


A slightly different, paid approach will be to take paid courses. I can recommend the Docker Maestro course from Damian Naprawa - we will go through all stages of learning and have the opportunity to build new projects.

Sources:
* Adrian Mouat, Using Docker: Developing and Deploying Software with Containers
* Joseph Muli, Beginning Devops with Docker 
* Adrian Smułkowski, Analysis of the possibilities of ensuring the security of Docker containers against selected attack methods (engineering work)
* [https://docs.docker.com/](https://docs.docker.com/)
* [https://www.baeldung.com/ops/docker-dockerfile-docker-compose](https://www.baeldung.com/ops/docker-dockerfile-docker-compose)
* [https://stackoverflow.com/questions/37966552/what-is-the-difference-between-docker-and-docker-compose](https://stackoverflow.com/questions/37966552/what-is-the-difference-between-docker-and-docker-compose)