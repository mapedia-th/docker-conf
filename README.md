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
