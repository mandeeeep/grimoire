Checking docker status

`sudo service docker status`

`sudo systemctl status docker`

Starting docker daemon if it isn't already started

`sudo systemctl start docker`

`sudo service docker start`

Download docker image

`sudo docker pull {$image_name}:{$tag_version}`

Clean all dockers image, containers, volumes and networks; unused ones only. Also, prune can be called specifically

`sudo docker system prune`

`sudo docker system prune --volumes` 

List docker containers

`sudo docker container ls -a`

Start containers

`sudo docker start {$container_name}`

Stop containers

`sudo docker stop {$container_name}`

Removing containers; cannot remove running containers though

`sudo docker container rm {$container_id}`




