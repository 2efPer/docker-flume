# docker-flume

Docker image for Apache Flume

# Supported tags and respective Dockerfile links

* 1.8.0, latest ([Dockfile](https://github.com/supermanHub/docker-flume))

# Quick reference

* **Where to get help**

  <jackie-1685@163.com>, 

* **Where to file issues**

  [Github Issue](https://github.com/supermanHub/docker-flume/issues/new)

* **Maintained by**
  
  Wenbo Wang, <jackie-1685@163.com>

# How to run

* **run with default**
  
  `docker run -d mengluo668/flume`

  > NOTE: The agent name for default configuration is '*agent*'， you can customize it by docker enviroment. please refer to blow.

* **run with customized agent name**
  
  `docker run -e AGENT=myAgent mengluo668/flume`

  > NOTE: If you run the image with a customized agent name, do remember that, the same agent name must be exist in your configuration file. e.g, flume-conf.properties. Please refer to blow.

* **run with customized configurations**

  `docker run -v /path/to/your/conf.properties:/apache-flume/conf/flume-conf.properties mengluo668/flume`

  > NOTE: If you has a different agent name than default, do remember to set docker environment for your agent.

* **run with customized log configurations**

  `docker run -v /path/to/your/log4j.properties:/apache-flume/conf/log4j.properties mengluo668/flume`

  > NOTE: You can specify where to output logs by log4j.properties

* **run with customized command**
  
  `docker run mengluo668/flume sh -c "./bin/flume-ng agent -n ${AGENT} -c conf -f conf/flume-conf.properties"`

  > NOTE: You can run flume with your preferred command!

* **stack deploy**

  ```js
  version: "3.6"
  services:
    flume1:
      image: mengluo668/flume:1.8.0
      hostname: flume1.example.com
      container_name: flume1.example.com
      restart: always
      environment:
        AGENT: fw
      volumes:
        - ${PWD}/flume/fw.properties:/apache-flume/conf/flume-conf.properties
      networks:
        webnet:
          aliases:
            - "flume1.example.com"
    flume2:
      image: mengluo668/flume:1.8.0
      hostname: flume2.example.com
      container_name: flume2.example.com
      restart: always
      environment:
        AGENT: sw
      volumes:
      - ${PWD}/flume/sw.properties:/apache-flume/conf/flume-conf.properties
      networks:
        webnet:
          aliases:
            - "flume2.example.com"
  networks:
    webnet:
  ```