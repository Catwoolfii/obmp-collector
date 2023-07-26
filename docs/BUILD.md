Building from Source 
====================
See the various requirements and suggested system configurations at [Requirements](REQUIREMENTS.md)

Openbmp is built and installed using 'cmake' to build the makefiles. 


Debian 11
------------
### Install Debian 11
Install standard Debian 11/bullseye server image [Debian Download](https://www.debian.org/download)

### Install the dependancies

``` 
sudo apt-get install cmake gcc g++ lib{boost-dev,lz4-dev,rdkafka-dev,sasl2-dev,ssl-dev,yaml-cpp-dev,zstd-dev} zlib1g-dev
```

RHEL7/CentOS7
-------------

### Install RHEL7 or CentOS 7.  
We use CentOS 7 minimal.  [CentOS 7 Download](http://www.centos.org/download/)

### Install basic dependancies
```
sudo yum install -y gcc gcc-c++ libstdc++-devel boost-devel cmake git wget openssl-libs openssl-devel cyrus-sasl-devel cyrus-sasl-lib
```


RHEL6/CentOS6 (6.5) - Legacy support
------------------------------------

### Install RHEL6 or CentOS 6.  
We use CentOS 6 minimal.  [CentOS 6 Download](http://wiki.centos.org/Download)

### Install basic dependancies
```
sudo yum install -y gcc gcc-c++ libstdc++-devel boost-devel boost-static cmake git wget  openssl-libs openssl-devel cyrus-sasl-devel cyrus-sasl-devel cyrus-sasl-lib
```


Compiling Source (All Platforms)
-------------------------------------
> #### IMPORTANT
> Make sure you have installed librdkafka development and runtime libs as mentioned under all platforms above.

Do the following: 

    wget clone https://github.com/Catwoolfii/obmp-collector/archive/refs/heads/main.tar.gz
    sudo tar zxvf main.tar.gz
    cd obmp-collector-main
    sudo mkdir -p build && cd build
    sudo cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr ../  
    sudo make -j 4

### Example output
```
localadmin@toolServer:/ws/ws-openbmp/openbmp/build$ sudo cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr ../
-- The C compiler identification is GNU 10.2.1
-- The CXX compiler identification is GNU 10.2.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Boost: /usr/lib/x86_64-linux-gnu/cmake/Boost-1.74.0/BoostConfig.cmake (found suitable version "1.74.0", minimum required is "1.41.0")
-- Found OpenSSL: /usr/lib/x86_64-linux-gnu/libcrypto.so (found suitable version "1.1.1n", minimum required is "1")
-- Performing Test SUPPORTS_STD_CXX11
-- Performing Test SUPPORTS_STD_CXX11 - Success
-- Performing Test SUPPORTS_STD_CXX01
-- Performing Test SUPPORTS_STD_CXX01 - Success
-- Configuring done
-- Generating done
-- Build files have been written to: /ws/ws-openbmp/openbmp/build

localadmin@toolServer:/ws/ws-openbmp/openbmp/build$ sudo make
Scanning dependencies of target openbmpd
[  8%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bmp/BMPReader.cpp.o
[  8%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bmp/BMPListener.cpp.o
[ 12%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/kafka/MsgBusImpl_kafka.cpp.o
[ 16%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/kafka/KafkaEventCallback.cpp.o
[ 20%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/kafka/KafkaDeliveryReportCallback.cpp.o
[ 24%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/kafka/KafkaTopicSelector.cpp.o
[ 28%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/kafka/KafkaPeerPartitionerCallback.cpp.o
[ 32%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/openbmp.cpp.o
[ 36%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bmp/parseBMP.cpp.o
[ 40%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/md5.cpp.o
[ 44%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/Logger.cpp.o
[ 48%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/Config.cpp.o
[ 52%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/client_thread.cpp.o
[ 56%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/parseBGP.cpp.o
[ 60%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/NotificationMsg.cpp.o
[ 64%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/OpenMsg.cpp.o
[ 68%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/UpdateMsg.cpp.o
[ 72%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/MPReachAttr.cpp.o
[ 76%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/MPUnReachAttr.cpp.o
[ 80%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/ExtCommunity.cpp.o
[ 84%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/AddPathDataContainer.cpp.o
[ 88%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/EVPN.cpp.o
[ 92%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/linkstate/MPLinkState.cpp.o
[ 96%] Building CXX object Server/CMakeFiles/openbmpd.dir/src/bgp/linkstate/MPLinkStateAttr.cpp.o
[100%] Linking CXX executable openbmpd
[100%] Built target openbmpd
```

Binary will be located under **Server/**

Install (All Platforms)
----------------------------------------------------

Run: **sudo** make install

> this will install openbmpd in /usr/bin/ by default.  You should be able to type **openbmpd** now to get the usage help. 
> 

```
ubuntu@bmp-dev:~/test/openbmp/build$ sudo make install
[100%] Built target openbmpd
Install the project...
-- Install configuration: ""
-- Installing: /usr/bin/openbmpd
-- Installing: /etc/openbmp/openbmpd.conf
-- Installing: /etc/default/openbmpd
-- Installing: /lib/systemd/system/openbmpd.service
-- Installing: /etc/logrotate.d/openbmpd
```
