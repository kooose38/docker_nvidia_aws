### docker install in aws ec2 
```
 $ sudo apt-get update 
 $ sudo apt-get install docker.io 
 $ sudo gpasswd -a ubuntu docker 
 $ docker --version 
```
### nvidia install  
参照公式ページ  
+ [#nvidia/document](https://docs.nvidia.com/datacenter/tesla/tesla-installation-notes/index.html)を参考にec2インスタンスでインストールする  
+ [#github.com/document](https://github.com/NVIDIA/nvidia-docker)
```
  $ sudo apt-get install linux-headers-$(uname -r) 
  $ distribution=$(. /etc/os-release;echo $ID$VERSION_ID | sed -e 's/\.//g')
  $ wget https://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64/cuda-$distribution.pin
  $ sudo mv cuda-$distribution.pin /etc/apt/preferences.d/cuda-repository-pin-600
  $ sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64/7fa2af80.pub
  $ echo "deb http://developer.download.nvidia.com/compute/cuda/repos/$distribution/x86_64 /" | sudo tee /etc/apt/sources.list.d/cuda.list
  $ sudo apt-get update
  $ sudo apt-get -y install cuda-drivers
  $ nvidia-smi  #Check gpu in the environment 
```
### Setting up Docker 
```
  $ curl https://get.docker.com | sh \
  && sudo systemctl --now enable docker
  $ distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list
   
  $ sudo apt-get update
  $ sudo apt-get install -y nvidia-docker2
  $ sudo systemctl restart docker
  $ docker run  --gpus all nvidia/cuda:11.0-base nvidia-smi
```