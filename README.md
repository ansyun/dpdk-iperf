# dpdk-iperf
Fork from official iperf-3.1.3, and run on the dpdk user space TCP/IP stack(ANS).

## porting iperf to ANS tcp/ip stack is ongoing, please waiting.......

####Build and Install
--------------
*  Download latest dpdk version from [dpdk website](http://dpdk.org/), and build dpdk
```
$ make config T=x86_64-native-linuxapp-gcc
$ make install T=x86_64-native-linuxapp-gcc
$ export RTE_SDK=/home/mytest/dpdk
$ export RTE_TARGET=x86_64-native-linuxapp-gcc
```
*  Download ANS following the [ANS wiki](https://github.com/opendp/dpdk-ans/wiki/Compile-APP-with-ans), buld ans and startup ans
```
$ git clone https://github.com/opendp/dpdk-ans.git
$ export RTE_ANS=/home/mytest/dpdk-ans
$ make
$ sudo ./build/ans -c 0x1 -n 1  -- -p 0x1 --config="(0,0,0)"
EAL: Detected lcore 0 as core 0 on socket 0
EAL: Detected lcore 1 as core 1 on socket 0
EAL: Support maximum 128 logical core(s) by configuration.
EAL: Detected 2 lcore(s)
EAL: VFIO modules not all loaded, skip VFIO support...
EAL: Setting up physically contiguous memory...
EAL: Ask a virtual area of 0x400000 bytes
EAL: Virtual area found at 0x7fdf90c00000 (size = 0x400000)
EAL: Ask a virtual area of 0x15400000 bytes
```
*  Download dpdk-iperf, build dpdk-iperf and startup dpdk-iperf
```
$ git clone https://github.com/opendp/dpdk-iperf.git
$ ./configure; make;


