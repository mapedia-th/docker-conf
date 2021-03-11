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
#### 6. Start the Docker Desktop using in your Admin PowerShell
```
Get-Service LxssManager | Restart-Service
```
#### 7. You may delete the D:\Docker\wsl\data\docker-desktop-data.tar file (NOT the ext4.vhdx file) if everything looks good for you after verifying

# Memory allocation to docker containers after moving to WSL 2 in Windows
#### 1. Open Windows Terminal/CMD/PowerShell and run the commands below:
```
# turn off all wsl instances such as docker-desktop
wsl --shutdown

```
#### 2. Create/ Open .wslconfig file with notepad:
```
notepad "$env:USERPROFILE/.wslconfig"
```
#### 3. Edit .wslconfig file with notepad and write down these settings:
```
[wsl2]
memory=6GB      # Any size you feel like
processors=4    # Virtual processors
swap=0
localhostForwarding=true

```
#### 4. Read More
- [WSL commands and launch configurations](https://docs.microsoft.com/en-us/windows/wsl/wsl-config#wsl-2-settings)
- [WSL2 Tips: Limit CPU/Memory When using Docker](https://itnext.io/wsl2-tips-limit-cpu-memory-when-using-docker-c022535faf6f)
- [Docker Desktop: WSL 2 Best practices](https://www.docker.com/blog/docker-desktop-wsl-2-best-practices/)
- [Docker Desktop for Windows user manual](https://docs.docker.com/docker-for-windows/#advanced)
- [WSL 2, Docker Desktop, VS Code Remote — WSL Extension](https://ponggun.medium.com/%E0%B8%9D%E0%B8%B6%E0%B8%81%E0%B9%83%E0%B8%8A%E0%B9%89%E0%B8%87%E0%B8%B2%E0%B8%99-wsl-2-docker-desktop-vs-code-remote-wsl-extension-e42e49d37d6d)
- [ติดตั้ง WSL 2, Docker Desktop บน Windows 10 ](https://ponggun.medium.com/%E0%B8%9A%E0%B8%B1%E0%B8%99%E0%B8%97%E0%B8%B6%E0%B8%81-%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87-wsl-2-docker-desktop-%E0%B8%9A%E0%B8%99-windows-10-home-64279672703)

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

# Reclaim the space used by WSL2 's ext4.vhdx
#### 1. Remove unused images and other resources
```
docker system prune -a
```

#### 2. Remove more resources
```
docker volume rm $(docker volume ls -q -f dangling=true)
```

#### 3. Stop docker desktop, optimize image
```
#Make sure HyperV turned on / or type Hyper-V in win search

%windir%\System32\mmc.exe "%windir%\System32\virtmgmt.msc"
```

#### 4. Optimize disk in GUI > Go to VM, and check disk
```
Optimize-VHD -Path "C:\ProgramData\DockerDesktop\vm-data\DockerDesktop.vhdx" -Mode Full
```

#### 5. Start docker desktop
```
Now You will have free disk space
```
#### 6. Read more
- [Cleaning Up Docker Disk Space In WSL2](https://marcroussy.com/2020/12/01/cleaning-up-docker-disk-space-in-wsl2/)

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
