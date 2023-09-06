---
title: Testing Code
date: 2022-09-18T10:51:50.000+05:30
cover:
  image: "https://github.com/srkc95/sreekanthc.com/blob/main/static/Theyyam_fighting_under_vangoghs_starry_night.png"
  alt: "<alt text>"
  caption: "<text>"
  relative: false

draft: false
---

This code is a Docker Compose configuration file that defines a service called "ubuntu" using an Ubuntu base image. The service is configured with various settings such as port mappings, volume mounts, and network configurations. It also specifies a series of commands to be executed when the container is started, including updating packages, installing software, and starting the Jenkins service.

The primary purpose of this code is to create a Docker container running Ubuntu, set up Jenkins within it, and expose ports for Jenkins and other services to interact with it.

``` python
version: '3.8'

services:
  ubuntu:
    image: ubuntu:latest
    container_name: ubuntu-base
    privileged: true
    ports:
      - "8080:8080"
      - "50000:50000"
    volumes:
      - "./jenkins_home:/var/jenkins_home"
    networks:
      - jenkins
    command:
      - /bin/bash
      - -c
      - |
        apt update
        apt install -y curl
        echo ----------------------
        sleep 10
        apt install openjdk-11-jre -y
        java --version
        echo ----------------------
        sleep 10
        curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
        echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | tee /etc/apt/sources.list.d/jenkins.list > /dev/null
        echo ----------------------
        sleep 10
        apt-get update
        apt-get install jenkins -y
        jenkins --version
        echo ----------------------
        sleep 10
        echo docker is starting...
        echo ----------------------
        /etc/init.d/jenkins start

        

networks:
  jenkins:

volumes:
  jenkins_home:

```
