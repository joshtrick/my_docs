# Install Nvidia driver

```
sudo apt-get install build-essential gcc-multilib dkms xorg xorg-dev
sudo apt-get install libsm6 libxext6 libxrender1
```

```
sudo echo "blacklist nouveau" >> /etc/modprobe.d/blacklist-nouveau.conf
sudo echo "options nouveau modeset=0" >> /etc/modprobe.d/blacklist-nouveau.conf
cat /etc/modprobe.d/blacklist-nouveau.conf

sudo update-initramfs -u
```

reboot

after reboot

```
sudo systemctl stop lightdm
sudo systemctl stop gdm
sudo systemctl stop kdm
```

install the driver

```
sudo ./NVIDIA-Linux-x86_64-384.69.run --dkms -s
```


# Install docker-ce for Ubuntu

```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) \
    stable”
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

# Install nvidia-docker for Ubuntu

```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit

sudo systemctl restart docker
```
