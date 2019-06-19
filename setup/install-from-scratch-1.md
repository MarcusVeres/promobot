# Install from Scratch 

> Detailed steps to set up promobot. Attempt 1. No prior knowledge of Qt, Docker, or Promobot SDK.  


## Part 1 :: Linux Setup 

#### Install XENIAL 

    docker run -it --name ubuntu ubuntu:xenial bash
    exit 


#### Run Ubuntu with promobot files in `/src` folder 

```
docker run \
  --name ubuntu \
  -e HOST_IP=$(ifconfig en0 | awk '/ *inet /{print $2}') \
  -v /Users/marcus/temp/promobot:/src \
  -t -i \
  ubuntu:xenial /bin/bash
```


#### Install dependencies 

```
apt-get update && apt-get -y install sudo
useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo
sudo apt-get -y install lsb-core
sudo apt-get -y install wget
sudo apt-get -y install apt-transport-https
sudo apt-get install -y software-properties-common 
```


#### Upgrade CMAKE 

> https://thoughtbot.com/blog/the-magic-behind-configure-make-make-install
> https://cmake.org/files/v3.7/

```
cd ~
mkdir dependencies && cd dependencies 
wget https://cmake.org/files/v3.7/cmake-3.7.2.tar.gz
cd cmake-3.7.2/
./configure
make 
make install
```


#### Refresh bash for Cmake 

> https://unix.stackexchange.com/questions/5609/how-do-i-clear-bashs-cache-of-paths-to-executables

```
type cmake
hash -r cmake 
which cmake 
cmake --version 
```

> Also seems to work with 3.8 :: https://cmake.org/files/v3.8/cmake-3.8.2.tar.gz

```
cd ~/dependencies 
wget https://cmake.org/files/v3.8/cmake-3.8.2.tar.gz
cd cmake-3.8.2/
./configure
make 
make install
```

> NOTE : I was not able to get this to work with some newer versions of cmake ( 3.13, 3.14 and 3.15 ).


#### Set default Qt5 

> Needs a `Qt5` compatible with version `5.6.2` and `CMAKE 3.7.2` stops at `5.5.1`.  

> **WARNING : Qt5 versio `5.11` is too avdanced! Will result in strange errors.** Keep versions between `5.6.2` and `5.9.5`!  

> https://askubuntu.com/questions/1062046/how-to-update-qt-from-5-5-1-to-5-9-5-on-ubuntu-16-04

Add a package manager, update links, and download QT. 
```
sudo add-apt-repository ppa:beineri/opt-qt591-xenial
sudo apt-get update 
sudo apt install qt59-meta-full
```

Create a `default.conf` file 
```
cd /etc/xdg/qtchooser
/opt/qt59/bin
/opt/qt59/lib
``` 

To avoid this error (caused by Linux caching an old reference):

    Could not find a configuration file for package "Qt5" that is compatible
    with requested version "5.6.2".
  
    The following configuration files were considered but not accepted:
  
      /usr/lib/x86_64-linux-gnu/cmake/Qt5/Qt5Config.cmake, version: 5.5.1

Type this:

    source /opt/qt59/bin/qt59-env.sh 

> Sauce : https://launchpad.net/~beineri/+archive/ubuntu/opt-qt-5.11.0-xenial



## Part 2 :: Linux GUI 

> I think this requires the `Qt` desktop version. I thought QtCreator was a command line tool, like cmake. Turns out it's a clusterfuck.  

> `Qt` can refer to an IDE, a programming framework, a command line tool, and the system itself. Also they cost $500 a month. This is like that Ext JS Sencha bullshit. Why use open-source tools when there are shittier, poorly-documented alternatives available for exhorbitant amounts of money?! inb4 `hurr, there's an open version of Qt on the side`.    


#### Exercise in futility 

    sudo apt-get install ubuntu-desktop

> Remember that Docker isn't suited for this type of use, and realize you wasted a bunch of time because the sdk_documentation doesn't say "install Ubuntu Desktop", and you thought server edition was enough.  


#### Maybe it's still on the command line

- `cmake build/` seems to have done something!
    - results in an error. but... it started 

```
root@6fb4f0cdbc4b:/src/sdk/examples# cmake build
-- Using CATKIN_DEVEL_PREFIX: /src/sdk/examples/devel
-- Using CMAKE_PREFIX_PATH:
-- Using PYTHON_EXECUTABLE: /usr/bin/python
-- Using Debian Python package layout
-- Using empy: /usr/bin/empy
-- Using CATKIN_ENABLE_TESTING: ON
-- Call enable_testing()
-- Using CATKIN_TEST_RESULTS_DIR: /src/sdk/examples/build/test_results
-- Found gtest sources under '/usr/src/gtest': gtests will be built
-- Using Python nosetests: /usr/bin/nosetests-2.7
-- catkin 0.7.8
Traceback (most recent call last):
  File "/src/sdk/examples/build/catkin_generated/generate_cached_setup.py", line 20, in <module>
    from catkin.environment_cache import generate_environment_script
ImportError: No module named catkin.environment_cache
CMake Error at /opt/ros/kinetic/share/catkin/cmake/safe_execute_process.cmake:11 (message):
  execute_process(/usr/bin/python
  "/src/sdk/examples/build/catkin_generated/generate_cached_setup.py")
  returned error code 1
Call Stack (most recent call first):
  /opt/ros/kinetic/share/catkin/cmake/all.cmake:186 (safe_execute_process)
  /opt/ros/kinetic/share/catkin/cmake/catkinConfig.cmake:20 (include)
  CMakeLists.txt:57 (find_package)


-- Configuring incomplete, errors occurred!
See also "/src/sdk/examples/build/CMakeFiles/CMakeOutput.log".
See also "/src/sdk/examples/build/CMakeFiles/CMakeError.log".
```

#### Try something else 

- [x] call `qtcreator` command from ubuntu cli
    - results in failure. calls for the same stuff that `startx` needs: a GUI 
    - this is underdocumented. no point in going further, alone 
    
- [x] seek external help



## Next Steps  

- [ ] order a couple flash drives ( boot drive, dual boot)
- [ ] install ubuntu, dual boot, on mac
- [ ] give ubuntu 64 gigs 

- [ ] dual boot laptop 
    - [ ] boot into Ubuntu 16.04 
    - [ ] run through the sdk setup from within ubuntu
    - [ ] run the `cmake` and `qmake` commands, on the `build/` folder, from ubuntu
    - [ ] see what happens 
