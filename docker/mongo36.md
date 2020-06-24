#Mongo 3.6

**For Ubuntu 20.04**

First, checking if docker exists

`sudo service docker status`

`sudo systemctl status docker`

Start docker daemon if it isn't already started

`sudo systemctl start docker`

`sudo service docker start`

Pull the mongo image

`sudo docker pull mongo:3.6`

Create a data folder for mongo, for instance

`/home/user/mongodata`

Create the docker container, with the mongo image, data folder and container name

`sudo docker create -v {$data_folder_location}:/data/db -p {$local_port}:{$image_port} --name {$container_name} -d {$mongo_image_tag}`

`sudo docker create -v /home/user/mongodata:/data/db -p 27019:27017 --name mongo36-test -d mongo:3.6`

Start the container, can add `-it` for interactive mode

`sudo docker start mongo36-test`

If there is a mongodump archive, mongorestore can be run. Or, if mongorestore binary is accessible to the host machine, just mongoretore to the appropriate port

`sudo docker exec -i mongo36-test sh -c 'mongorestore --db $db_name --gzip --archive' < dump.gzip`

`mongorestore --host $address --port $port --db $db_name --archive dump.gzip`











