## Recap
``` bash
docker build . -t flask-app:v2
docker run -dp 8080:8080 flask-app:v2
docker ps -a
docker stop <containerID>
docker rm <containerID>
```

## Images
Pull the following images and compare them
- alpine
- ubuntu
- nicolaka/netshoot

``` bash
docker images
docker pull <imageName>
# Task: Show all images, and comment on the effect of image sizes. How would it affect container start up time?
```

## Exec
``` bash
docker run nicolaka/netshoot
docker run -d nicolaka/netshoot sleep 99999
docker exec -it <containerID> sh
```

## Run Binaries
``` bash
docker run nicolaka/netshoot curl www.google.com
docker run nicolaka/netshoot whois www.google.com
docker run nicolaka/netshoot dig www.google.com
```

## Volumes
``` bash
docker volume ls
# create shared volume
docker volume create demo
# create container
docker run --mount type=volume,src=demo,target=/tmp -d alpine sleep 99999
docker run --mount type=volume,src=demo,target=/tmp -d alpine sleep 99999
docker exec -it <containerID> sh

# Task: Verify that /tmp directory in the containers are empty
# Task: Exec into either container, create a file to the /tmp. Then verify on the other container.
# Task: Stop and remove containers
# Task: Remove volume
```

## Networks
``` bash
docker network ls
# create shared network
docker network create demo
# create containers
docker run --network demo -d -p 8080:8080 flask-app
docker run --network demo -d nicolaka/netshoot sleep 99999
docker exec -it <containerID> sh

# Task: Using netshoot, make a curl request to flask app (Hint: How do you get the ip for a machine)
# Task: View the logs of flask app
# Task: Create netshoot container in detached mode. It should to make a request to flask app (every 1 second)
# Task: Stop and remove containers
# Task: Remove network
```

## Docker Compose
``` bash
docker compose up -d
# Task: Exec into netshoot container and make a curl request to http://app:8080. What is happening? (Hint: Investigate compose.yaml)
# Task: Update an environment variable in the compose file and rerun `docker compose up -d`. Do all containers get recreated?

docker compose down
```

## Clean up
``` bash
docker rm -f $(docker ps -aq) # remove all containers
docker volume prune # remove dangling volumes
docker network prune # remove dangling networks
```

## Reference
- [Docker Overview](https://docs.docker.com/get-started/overview/)
- [Docker Commands](https://docs.docker.com/engine/reference/commandline/cli/) 
- [Docker Compose](https://docs.docker.com/compose/)
