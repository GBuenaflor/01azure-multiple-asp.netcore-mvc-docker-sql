# 01azure-multiple-asp.netcore-mvc-docker-sql
2 asp.net core mvc with docker implementation. 1 connects to sql database and 1 is stand alone.
 
# Run Container using docker-compose

cd C:\_5\GBDockerPOC 
  
docker-compose up -d
docker logs web1
docker container list -a

# View the container

docker container list -a
docker exec <ContainerID> ipconfig

open browser using the IP Address

# Run Specific Container Manually

cd C:\_5\GBDockerPOC\Web1
docker build -t web1 .
docker image list
docker system prune

docker run -d --name web1 web1
docker logs web1

 
# Running Docker in Specific PORT (Windows Container)

cd C:\_5\GBDockerPOC\
docker-compose up -d
docker-compose down

cd C:\_5\GBDockerPOC\Web1
docker run -it -p 8080:8080 -d web1
docker ps
docker exec <ContainerID> ipconfig

Browse using the IP http://172.18.9.122:8080

# Edit connectionstring from the code

string connectionString = "Server=tcp:gbdockerdbserver.database.windows.net,1433;Initial Catalog=gbdockerdb;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;";



