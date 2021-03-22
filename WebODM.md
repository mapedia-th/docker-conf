# Install WebODM on Docker Desktop
<img alt="WebODM" src="https://user-images.githubusercontent.com/1951843/34074943-8f057c3c-e287-11e7-924d-3ccafa60c43a.png" width="180">

## 1. การติดตั้งโปรแกรม Git
### 1.1 ดาวน์โหลดโปรแกรมได้ที่ [Git](https://git-scm.com/downloads)
<img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/1.PNG"/>

### 1.2 ดับเบิลคลิกที่ไฟล์ Git-2.31.0-64-bit.exe เพื่อเริ่มติดตั้งโปรแกรม

### 1.3 ติกถูกเลือกทั้งหมด แล้วคลิกที่ OK
<img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/1.PNG"/>


## 2. การติดตั้งโปรแกรม Docker
### 2.1 ท่านสามารถดาวน์โหลดโปรแกรม docker ได้ที่ [Docker](https://www.docker.com/)

### 2.2 ดับเบิลคลิกที่ไฟล์ Docker Desktop Installer.exe เพื่อเริ่มติดตั้งโปรแกรม

### 2.3 ติกถูกเลือกทั้งหมด แล้วคลิกที่ OK
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/1.PNG"/>

### 2.4 เริ่มติดตั้งโปรแกรม docker กรุณารอสักครู่
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/2.PNG"/>

### 2.5 จากนั้นคลิกที่ปุ่ม Close and restart
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/4.PNG"/>

### 2.6 หลังจากที่ restart เครื่องแล้ว docker จะมีการแจ้งเตือนว่ายังติดตั้ง WSL2 ไม่สมบูรณ์ ให้คลิกที่เว็บ https://aka.ms/wsl2kernel
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/5.PNG"/>

### 2.7 ให้ทำการเปิด PowerShell แบบ Administrator เพื่อ Enable the Windows Subsystem for Linux ด้วยคำสั่งด้านล่าง:
  ```
  dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
  ```
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/6.PNG"/>

### 2.8 จากนั้นก็ให้ทำการเปิด Enable Virtual Machine Platform ด้วยคำสั่งด้านล่าง:
  ```
  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
  ```
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/7.PNG"/>

### 2.9 ดับเบิลคลิกที่ไฟล์ wsl_update_x64.msi เพื่ออัพเดท WSL2 Linux kernel update package for x64 machines หรือ [ดาวน์โหลดได้ที่](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/8.PNG"/>

### 2.10 การติดตั้งเพื่ออัพเดท WSL2 Linux kernel update package for x64 machines สำเร็จ
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/9.PNG"/>

### 2.11 จากนั้นก็จะสามารถเปิดใช้งาน docker ได้
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/10.PNG"/>

## 3. ขั้นตอนการตั้งค่า Switch ระหว่าง WLS 2 กับ Hyper-V ใน Docker
### 3.1 วิธีสลับไปใช้ Hyper-V สามารถทำได้โดย ติกเครืองหมายถูกออกในช่อง Use the WSL 2 based engine จากนั้นกดที่ Apply and Restart
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/11.PNG"/>

### 3.2 จากนั้น docker จะเริ่มที่การ Switching และทำการปิด WSL 2 ให้
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/13.PNG"/>

### 3.3 จะเห็นว่าเมื่อ Switch มาใช้งานในฝั่งของ Hyper-v แล้วจะสามารถปรับ Resource ได้
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/14.PNG"/>

### 3.4 ซึ่งปกติแล้วไฟล์ image จะอยู่ที่ C:\ProgramData\DockerDesktop\vm-data
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/12.PNG"/>

### 3.5 แต่ถ้าเราอยากจะกลับไปใช้แบบ WSL 2 ก็ให้ติกถูกที่ช่อง Use the WSL 2 based engine กลับคืน จากนั้นกดที่ Apply and Restart
  <img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/10.PNG"/>


## 4. ขั้นตอนการติดตั้งโปรแกรม WebODM
### 4.1 ให้เปิด Git Bash หรือ Powershell แล้วพิมพ์ชุดคำสั่งด้านล่างนี้:
```bash
git clone https://github.com/OpenDroneMap/WebODM --config core.autocrlf=input --depth 1

```
<img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/18.PNG"/>

### 4.2 จากนั้นเราจะได้โฟลเดอร์ WebODM ดังภาพด้านล่าง
<img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/16.PNG"/>

### 4.3 ทำการเข้าไปที่ไดเร็กทอรี่ WebODM ด้วยคำสั่ง:
```bash
cd WebODM
```
<img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/19.PNG"/>

### 4.4 ทำการ Start WebODM ด้วยคำสั่ง:
```bash
./webodm.sh start
```
<img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/20.PNG"/>

<img width="700" src="https://github.com/mapedia-th/docker-conf/blob/main/img/21.PNG"/>

* If you face any issues at the last step on Linux, make sure your user is part of the docker group:
```bash
sudo usermod -aG docker $USER
exit
(restart shell by logging out and then back-in)
./webodm.sh start
```
* Open a Web Browser to `http://localhost:8000` (unless you are on Windows using Docker Toolbox, see below)

Docker Toolbox users need to find the IP of their docker machine by running this command from the Docker Quickstart Terminal:

```bash
docker-machine ip
192.168.1.100 (your output will be different)
```

The address to connect to would then be: `http://192.168.1.100:8000`.

To stop WebODM press CTRL+C or run:

```
./webodm.sh stop
```

To update WebODM to the latest version use:

```bash
./webodm.sh update
```

We recommend that you read the [Docker Documentation](https://docs.docker.com/) to familiarize with the application lifecycle, setup and teardown, or for more advanced uses. Look at the contents of the webodm.sh script to understand what commands are used to launch WebODM.

### 4.5 จากนั้นใน docker เราจะเห็นว่ามีไฟล์ Images และ Containers/Apps ที่เป็นของ webodm แสดงขึ้นมาดังภาพ
<img width="800" src="https://github.com/mapedia-th/docker-conf/blob/main/img/22.PNG"/>

<img width="800" src="https://github.com/mapedia-th/docker-conf/blob/main/img/23.PNG"/>

## License

WebODM is licensed under the terms of the [GNU Affero General Public License v3.0](https://github.com/OpenDroneMap/WebODM/blob/master/LICENSE.md).
