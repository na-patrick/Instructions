# VISIONAWARE INSTALLATION

## 1. Ubuntu installation

Start by downloading Ubuntu 18.04.1.  
You can find the download [here](http://old-releases.ubuntu.com/releases/18.04.1/).  

Write the .iso to a bootable usb. You can do this using your software of choice (I used Ubuntu's "Startup Disk Creator").  

Run through the installation process. Pick "Normal Installation" and "Download updates while installing Ubuntu".  
In my case, I had to "Erase Ubuntu 18.04.1 LTS and reinstall".  


## 2. CUDA installation

Install dependencies for CUDA: `sudo apt-get update`, `sudo apt-get upgrade`, `sudo apt-get install linux-headers-$(uname -r)`, and `sudo apt-get build-essential`  
Disable Nouveau drivers by creating a file `/etc/modprobe.d/blacklist-nouveau.conf` with the following contents:  
`blacklist nouveau`  
`options nouveau modeset=0`

I didn't need to do this, but CUDA also asks to regenerate kernel initfamfs: `sudo update-initramfs -u`  

[Download CUDA](https://developer.nvidia.com/cuda-10.0-download-archive).  
Download the runfile associated with Ubuntu 18.04.  
Run the installation file: `sudo sh cuda-10.0.130_410.48_linux.run`  

Go through the installation process, I chose the following options:  
Install drivers: yes  
OpenGL libraries: default  
nvidia-xconfig: default  
CUDA 10.0: yes  
Toolkit location: default  
Symbolic link: yes  
Samples: yes  
Samples location: default  

Add the following to `~/.profile`:  
`export PATH=/usr/local/cuda/bin:/usr/local/cuda/NsightCompute-1.0${PATH:+:${PATH}}`  
`export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}`  

Restart the computer.  

## 3. QT installation

Install some prerequisites: `sudo apt-get install mesa-common-dev`, `sudo apt-get install libglu1-mesa-dev`  
Navigate through the Qt website and download "Qt Open Source".  
Give execution permissions to the runfile: `chmod +x`  
Run the installer.  
When installing components, choose "Archive" and refresh. Then pick Qt 5.12.0.  
Install the components.

## 4. Pylon installation

Visit the [Basler website](https://www.baslerweb.com/en/sales-support/downloads/software-downloads/pylon-5-1-0-linux-x86-64-bit/) and install the Pylon SDK.  
Extract the tarfile: `tar -xvzf`  
Change directory to the extracted folder.  
Extract the SDK into `/opt`: `sudo tar -C /opt -xzf pylonSDK*.tar.gz`  
Add `export LD_LIBRARY_PATH=.:/usr/local/lib:/opt/pylon5/lib64:LD_LIBRARY_PATH` to `~/.profile`  

## 5. Tensorflow C installation

Visit the [Tensorflow for C website](https://www.tensorflow.org/install/lang_c) and download the Linux GPU support library.  
Extract the tarfile: `sudo tar -C /usr/local -xzf libtensorflow-gpu-linux-x86_64-1.14.0.tar.gz`  
Configure the linker: `sudo ldconfig`  

## 6. glog installation

Install glog with: `sudo apt install libgoogle-glog-dev`  

## 7. VisionAware installation

Install git: `sudo apt-get install git`  
Clone the git repo: `git clone https://github.com/NeuronAware/VisionAware.git`  
Open in Qt Creator, turn off "shadow build" in build options, and run.  

## 8. CuDNN installation
```sh
sudo dpkg -i <downloaded cudnn file.deb>
```

## 9. Make sure `PATH` and `LD_LIBRARY_PATH` environment variables are correctly set
```sh
export PATH=.:/usr/local/cuda/bin:/usr/local/cuda/NsightCompute-1.0${PATH:+:${PATH}}
export LD_LIBRARY_PATH=.:/usr/local/lib:/opt/pylon5/lib64:/usr/local/cuda/lib64:/usr/local/cuda/lib64/stubs${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
