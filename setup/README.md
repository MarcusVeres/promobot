# Promobot Setup 


## Requirements 

- Computer running `Ubuntu 16.04 Xenial` DESKTOP edition
  - Desktop version is required for using `Qt`


## Instructions 

- Download the `Promobot-SDK.gzip` file from wherever 
- Save the following script as `install.sh` to the same folder as `Promobot-SDK`
- `chmod +x install.sh`
- `./install.sh` 

```bash
#!/bin/bash

# Donwload the ZIP file from wherever

unzip Promobot_SDK_1.8.0_En.zip
cd Promobot_SDK_1.8.0_En

# Extract the SDK
tar zxf Promobot_SDK_1.8.0.tar.gz
cd sdk/Promobot_SDK_1.8.0/

# Install dependencies
sudo apt update && sudo apt -y install \
    lsb-release \
    gnupg2 \
    wget \
    apt-transport-https \
    ca-certificates \
    iputils-ping

# Install Promobot
sudo /bin/bash install-sdk.sh

# Install Examples (printer etc)
cd /build/examples
/bin/bash build.sh
```

## Using the SDK 

> Pending training session results. 

