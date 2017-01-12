# Instructions for the Docker from scratch workshop

Basic Docker Commands:
  - docker run <image>
  - docker start <name|id>
  - docker stop <name|id>
  - docker ps [-a include stopped containers]
  - docker rm <name|id>

Connect to the droplet
  - ssh root@host

Login to your Docker account
  - docker login

Check that the installation is working with the official hello-world container
  - docker run hello-world

Run a web-based hello world
  - docker run tutum/hello-world

To expose the container to the world
  - docker run -p 80:80 tutum/hello-world

At this point if you run 'docker ps -a' you will see 3 or more containers, which are either stopped or running.
To get rid of them we do:
  - docker rm <containerId>
You can specify only the start of the containerId and this command will work.
I.e. ('docker rm e8' for container with Id of e8f1c0192dd8)

Let's create a couple of containers now
  - docker run -d --name app1 -p 80:80 tutum/hello-world
  - docker run -d --name app2 -p 81:80 tutum/hello-world
  - docker run -d --name app3 -p 82:80 tutum/hello-world
The -d flag runs the container on the background
The --name is self-explanatory

We can now run commands using the container's name
  - docker stop app1
  - docker start app1

To stop all containers at once we can use this command
  - docker stop $(docker ps -a -q)
The -a lists all containers, and the -q lists only their id's

Let's now run an nginx server
  - docker run -d -p 80:80 nginx

Let's get inside our new container using bash
  - docker exec -i -t <containerId> /bin/bash
The html folder is located at '/usr/share/nginx/html'

Position your terminal on the root of this project, then run
  - docker build -t <username>/do-cdmx-nginx .
The . is because we are pulling from this projects root
do-cdmx-nginx is the name we've given to our image

Then we can run our new instance by doing
  - docker run -d -p 80:80 <username>/do-cdmx-nginx

At this point, you want to create a new repository in your DockerHub account
Once you've done that, then you can push to that repo
 - docker push pablovilla83/do-cdmx-nginx

Your repo might show that there hasn't been any push. This is an open bug.
https://github.com/docker/hub-feedback/issues/301
If you got the digest confirmation of your push, your up and ready to go.
