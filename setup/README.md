## Promobot Setup 

> How to set up the Promobot SDK. Most of this is intuited. Near the end, things get dicey. **I want clear, step-by-step instructions and links to the PPAs/libraries used.**  


## Requirements 

> What, exactly, do I need to run? 

- [ ] You **must** run Ubuntu **Desktop** edition (16.04 / Xenial ONLY)
- [ ] 8 GiB RAM
- [ ] ?? Processor
- [ ] ?? Hard drive space 
- [ ] **Apparently, I need QtCreator desktop. Which version? Which dependencies? Where are the links?!**  

### List of Required Scripts 

- [ ] sudo
- [ ] lsb-core
- [ ] wget
- [ ] apt-transport-https
- [ ] software-properties-common

- [ ] qmake `3.7.2` to `3.8.2`
- [ ] Qt5 version `5.6.2` to `5.9.5`


## Detailed Instructions 

### System Setup 

```
apt-get update && apt-get -y install sudo
useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo
sudo apt-get -y install lsb-core
sudo apt-get -y install wget
sudo apt-get -y install apt-transport-https
sudo apt-get install -y software-properties-common 
```

### Qt Configure

Create a `default.conf`
```
cd /etc/xdg/qtchooser
vi default.conf 
```

Write the following lines 
```
/opt/qt59/bin
/opt/qt59/lib
```

Run a script to update references 
```
source /opt/qt59/bin/qt59-env.sh 
```
> Note: effects of this script don't seem to be permanent. Qt reverted to `5.5.1` after reboot. 


### Build and Compile 

Extract the contents of the `Promobot-SDK-1.8.0.tar.gz` (or whatever version) and navigate to the folder. 
```
mkdir sdk 
tar xzvf Promobot_SDK_1.8.0.tar.gz --strip-components=1 -C sdk
cd sdk
```

Make the install shell script executable
```
chmod +x install-sdk.sh
sudo ./install-sdk.sh
``` 

Download and install `QtCreator` 
- from where? 
- what version? *clearly* this shit matters. everything else throws an error if it's not the **exact** version this POS software needs
- the desktop tool, or the cli, or the library?
- do I need to create an account? they're asking me to confirm my email and sign in to their system. **is this necessary?**

Build the `examples/` folder (created when the sdk was extracted. on the same level as `sdk/` and `install-sdk.sh`
```
cd examples
chmod +x build.sh
./build.sh
``` 

Install the examples 
```
./build.sh install -DCMAKE_INSTALL_PREFIX=/opt/promobot
```
- does this install on the robot? locally? 
- the script runs, but no executable is produced. 


## What now?! 

> *"After the installation is completed, you can create a new application project."*

- spell this out for me, motherfucker
    - install QtCreator version **0.0.0.10** on Ubuntu Desktop
    - use *these* settings
    - create, or don't create, an account
    - select X license
    - open QtCreator desktop
    - **create a new QtCreator project (application template)**

> *"You can use `templateobject.cpp`"* 

- **where** do I find this file? 

> *"You must have the skills to develop in C++ and Qt"* 

- and read minds, apparently. Even Gentoo comes with fucking instructions. 
- `</rant>` 


## Appendix I :: Attempts 

> Documenting steps taken, until I succeed. 

- [First Attempt](./install-from-scratch-1.md)
