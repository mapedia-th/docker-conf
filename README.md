# Docker Cheat Sheet
Docker Cheat Sheet WSL 2 and Hyper-V
## Change the location of docker images when using Docker Desktop on WSL 2

#### 1. The WSL 2 docker-desktop-data vm disk image would normally reside in:
```
 %USERPROFILE%\AppData\Local\Docker\wsl\data\ext4.vhdx
```

#### 2. Shut down your docker desktop and Quit Docker Desktop
```
wsl --shutdown
```

Then, open your command prompt:
```
wsl -l -v
```
You should be able to see, make sure the STATE for both is Stopped.
```
  NAME                   STATE           VERSION
* docker-desktop-data    Stopped         2
```


#### 3. Export docker-desktop-data into a file
```
wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
```

#### 4. Unregister docker-desktop-data from wsl, note that after this, your ext4.vhdx file would automatically be removed (so back it up first if you have important existing image/container):
```
wsl --unregister docker-desktop-data
```
#### 5. Import the docker-desktop-data back to wsl, but now the ext4.vhdx would reside in different drive/directory:
```
wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
```
#### 6. Start the Docker Desktop again and it should work :)

#### 7. You may delete the D:\Docker\wsl\data\docker-desktop-data.tar file (NOT the ext4.vhdx file) if everything looks good for you after verifying

# Alternative choice to Change the location
```
1. Stop Docker Desktop

2. Relocate Docker folder from C:\Users\chingchaih\AppData\Local\Docker to new path

3. Make sure C:\Users\chingchaih\AppData\Local\Docker is no longer there

4. Open a cmd in administrator mode

5. Run the following command that will create a symbolic link in the cmd window with the appropriate from and to path

    mklink /j "C:\Users\chingchaih\AppData\Local\Docker" "D:\Docker"

6. Restart Docker Desktop

7. Remove junction link
    rmdir "C:\Users\chingchaih\AppData\Local\Docker"

```

# Docker Cheat Sheet
#### จัดการ Docker Images
```
docker images #View docker images
docker image ls #View docker images
docker build -t {name}:{tag} . #Build image
docker image rm {docker image name/ image id} #remove image
docker run -p {server port}:{docker port} -d {image name}:{image tag} #Run image
```
#### จัดการ Docker Container
```
docker ps #List running containers
docker ps -a #List all containers
docker start {docker container id} #start container
docker stop {docker container id} #stop container
docker rm {docker container id} #remove container
docker container rm -f $(docker ps -aq) #remove all container
```
#### จัดการ Docker Compose
```
docker-compose start #start docker compose
docker-compose stop #stop docker compose
docker-compose pause #pause running containers
docker-compose unpause #unpause running containers
docker-compose ps #List containers
docker-compose up
#Builds,creates,starts,attaches to containers
docker-compose down
#Stops containers and removes containers, networks, volumes, and images created by up
```
#### Links
[Docker Cheat Sheet](https://www.docker.com/sites/default/files/d8/2019-09/docker-cheat-sheet.pdf)
