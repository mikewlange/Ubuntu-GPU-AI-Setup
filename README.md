# Ubuntu-GPU-AI-Setup
Ubuntu CUDA Deep Learning GPU Setup - CUDA, cuDNN, Torch, Python 2, Python 3, TensorFlow, Theano, Keras, Pytorch, OpenCV, Dlib, and many specialised tools, frameworks and open source libraries. 

What's the point of posting another deep learning machine setup guide? To be frank, most of the ones I've read suck or are incomplete for a bare metal setup. 

There are a trillion Linux flavors, GPUs, ext.. and each have their own bs. If you've never thrown a 3000$ machine out the window setting up CUDA 8 or 9 and Nvidia kernal drivers on a Linux box you built from scratch you're not learning what you need to know.  

And if you plan to do ML commercially and not use pre-trained models (which you should never ever do for Ai you run in a production environmnet), cloud gpu processing for research/discovery/model design can be very expensive. 

This is not building an app or website or even a game, the processing power and time it takes to train commercial grade Nn's is considerable. It's not any more difficult work in any way (much easier actually - thank goodness companies think this is tough stuff - shhh :), it's just process intesive. ya gotta learn the trade offs of when and how to use GpU processor cycles in your devops. 

Build a machine for your Ai dev at least once, trust me it's worth the time invested. Ask yourself, ever had to manually disable and blacklist a Nouveau kernel driver to install software? if not, do this(or similar) before you grab an aws ami and hack away. 

Let's get too it. 

## Project Goals  

This machine is a general DeepLearning development box thats fits the industry standards for building effective Neural Nets and ML tools. We want our machine to be our local one stop shop for research and dev of commercial AI in any business sector. 

It should have the tools to easily classify genetic anomilies, discover new physics with CMS detector data, build HFT systems, design driverless tractors, teach the driver of a tractor new skills, build a web app from a napkin sketch, discover its own use with arbitrary data sets, forcast the date of and how many pitches will be thrown in the final game when the Cubs take home another world series, automate acedemic research via ocr and nlp, and write its own jokes and music. 

There will working examples of all these things in the comming weeks. The only thing i cant promise is another Cubs workd series.  

## And so it begins
To install most of the stuff, youll have to stop running lightdm/X SERVER, so you will not have access to web browser. Unless you use a txt  rowser like links2 - which is my favorite - but its a pain. I suggest you you use another puter or print this out. intalling the right Nvidia driver kernal and CUDA combo is a bitch. I've done this 100's of times and every machine/gpu has its own issues. Which is why you'll find this similar set up all over the interwebs but never the same insutruction set. 


## Step #1: Install Ubuntu system dependencies

Close all running applications.  
Press ctrl + alt + F1 .  
Login with your username and password.  
Stop X server by executing  
sudo service lightdm stop

Perform the install instructions.

### Update the machine  
sudo apt-get update  
sudo apt-get upgrade  


### Pre-requisite 
$ sudo apt-get install build-essential cmake git unzip pkg-config  
$ sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev  
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev  
$ sudo apt-get install libxvidcore-dev libx264-dev  
$ sudo apt-get install libgtk-3-dev  
$ sudo apt-get install libhdf5-serial-dev graphviz    
$ sudo apt-get install libopenblas-dev libatlas-base-dev gfortran  
$ sudo apt-get install python-tk python3-tk python-imaging-tk  
$ sudo apt-get install python2.7-dev python3-dev  

### Prepare for Linus' distain for nvidia (I'm just guessing)
$ sudo apt-get install linux-image-generic linux-image-extra-virtual  
$ sudo apt-get install linux-source linux-headers-generic  

## Step #2 CUDA 8: CUDA Toolkit - Use ALT Step #2  
This instruction set is from here https://www.pyimagesearch.com/2017/09/27/setting-up-ubuntu-16-04-cuda-gpu-for-deep-learning-with-python/ - However, it's a tedious way to do this. It works, but not nesecary for CUDA 9.1. However, they are well thought out instructions and worth a read. Plus, there is something to be said about doing something the hard way and then doing it right. 

Please pay close attention to to detail for this one or you may throw your machine out the window :) 

First disable the Nouveau kernel driver by creating a new file:  
$ sudo nano /etc/modprobe.d/blacklist-nouveau.conf  

Setup the ram file and reboot  
$ echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf  
$ sudo update-initramfs -u  
$ sudo reboot  

You will want to download the CUDA Toolkit v8.0 via the NVIDIA CUDA Toolkit website:  

https://developer.nvidia.com/cuda-80-ga2-download-archive  

Once you’re on the download page, select Linux => x86_64 => Ubuntu => 16.04 => runfile (local) .   
Make sure below is cool - and use wget just becuase  
$ wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run

### Extract and be patient on the last step
$ chmod +x cuda_8.0.61_375.26_linux-run  
$ mkdir installers  
$ sudo ./cuda_8.0.61_375.26_linux-run -extract=`pwd`/installers  

###  install the NVIDIA kernel driver:
$ cd installers
$ sudo ./NVIDIA-Linux-x86_64-390.48.run

## ALT Step #2 - CUDA 9.1 and NVIDIA kernel driver:












## old ignore!
## Java - Just because. Open jdk is fine. 

sudo apt-get update

sudo apt-get install default-jdk

## NVIDIA Drivers 
### So you don't stab yourself in the face later
sudo apt-get purge nvidia*

sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
sudo apt-get install nvidia-396 
(at time of writing for gforce 1080)

#### reboot

### Basic shite
sudo apt install -y chromium-browser  (now we can close Firefox)
sudo apt install zsh

### Gotta write code - might as well use Sublime. Just run these 4 all at once
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

sudo apt update

sudo apt install sublime-text

Lauch Ubuntu Software and install Guake Terminal - then everything is an f12 away. 

### Machine Learning Setup

sudo apt-get update

sudo apt-get upgrade

### swag
sudo apt-get install -y build-essential cmake gfortran git pkg-config  

sudo apt-get install -y python-dev software-properties-common wget vim

sudo apt-get autoremove

## CUDA
https://developer.nvidia.com/cuda-downloads - download the file and patches

sudo dpkg -i cuda-repo-ubuntu1604-9-1-local_9.1.85-1_amd64.deb

sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
  
sudo apt-get update

sudo apt-get install cuda

## reboot since a new driver might be installed then test it

nvidia-smi 

## cuDNN
https://developer.nvidia.com/rdp/cudnn-download - have to join NVIDIA dev program. It's free and if you're actually reading this, you're registered. Or not. 

### unpack and install
tar xvf cudnn-8.0-linux-x64-v6.0.tgz
sudo cp -P cuda/lib64/* /usr/local/cuda/lib64/
sudo cp cuda/include/* /usr/local/cuda/include/

Update your paths
echo 'export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64"' >> ~/.bashrc
echo 'export CUDA_HOME=/usr/local/cuda' >> ~/.bashrc
echo 'export PATH="/usr/local/cuda/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc


## framework dependencies
sudo apt-get update

sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler libopencv-dev

### install python 2 and 3 along with other important packages like boost, lmdb, glog, blas, ass and gas.

sudo apt-get install -y --no-install-recommends libboost-all-dev doxygen
sudo apt-get install -y libgflags-dev libgoogle-glog-dev liblmdb-dev libblas-dev 
sudo apt-get install -y libatlas-base-dev libopenblas-dev libgphoto2-dev libeigen3-dev libhdf5-dev 

sudo apt-get install -y python-dev python-pip python-nose python-numpy python-scipy
sudo apt-get install -y python3-dev python3-pip python3-nose python3-numpy python3-scipy
