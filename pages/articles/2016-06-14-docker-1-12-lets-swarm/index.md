---
title: Docker 1.12 - Let's swarm! 
date: "2016-06-14"
layout: post
path: "/docker-1-12-lets-swarm"
category: "docker"
description: "Docker 1.12 is probably the most important release since 1.0. Docker 1.12 has added features to make multi-host and multi-container orchestration available for everyone who wants or needs it."
---

Docker 1.12 is probably the most important release since 1.0. Docker 1.12 has added features to make multi-host and multi-container orchestration available for everyone who wants or needs it.

This option was once available to those who had time, resources and money to maintain a distributed platform, but not anymore.

## Let's swarm

<img src="https://i.giphy.com/RHJsqvHsbfyak.gif" width="500" height="500"/>

1. Install Docker on multiple servers

2. Create your swarm on your main server ! 
```
docker swarm init
```

3. Join your master Server 
```
docker swarm join \
       --token SWMTKN-xxxxx \
       {internalIp}:2377
 ```

4. Check that everything is ok ! 
```
docker node ls
```

<img src="./nodes.png" width="500" height="500" />

5. Create your overlay network :  
```docker network create -d overlay test```

6. Let's create a service  
```docker service create --name nginx --network test --replicas 5 -p 8001:80/tcp nginx```

7. docker service ps nginx
<img src="./services.png" width="500" height="500" />

Your service is now replicated across multiple servers and load balanced automatically !

<img src="http://i.giphy.com/13qhDFqjZwIIve.gif" width="500" height="500" />
