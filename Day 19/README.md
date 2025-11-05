# OpenROAD Installation

**Cloning below the git repository**
```
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
```
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2019/Images/img1.png)  

**Running setup script**
```
cd OpenROAD-flow-scripts
sudo ./setup.sh
```
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2019/Images/img2.png)   

**Build OpenRoad**  
* Using Docker to run the build of OpenLane
* Docker installation
```
sudo apt update
sudo apt install ca-certificates curl gnupg
# Docker's official GPG (security) key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

#setting up docker
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
#installing docker
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
sudo usermod -aG docker $USER
```
* Logging out and in for Docker installation
* Building OpenRoad using Docker.
```
df -h # checking free space
docker system prune -a -f
rm -rf tools/OpenROAD/build
sudo apt clean
cd ~/OpenROAD-flow-scripts
./build_openroad.sh
```
![img3_1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2019/Images/img3_1.png)  

**Verify Installation**
```
cd flow
util/docker_shell make
```
![img2_1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2019/Images/img2_1.png)  
![img2_2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2019/Images/img2_2.png)  

**Visualize final layout in GUI**
```
util/docker_shell make gui_final
```
![img1_1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2019/Images/img1_1.png)

**Issue**
* "No space left on device" Error
    * Adding more space to the virtual machine using gpart
```
# First, navigate to the VirtualBox folder
cd "C:\Program Files\Oracle\VirtualBox"

#  run the resize command
.\VBoxManage.exe modifymedium disk "C:\Users\Dhruvi\VirtualBox VMs\Ubuntu 24.04\Ubuntu 24.04.vdi" --resize 81920
```
