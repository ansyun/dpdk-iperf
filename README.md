#### dpdk-iperf
--------------
Fork from official iperf-3.1.3, and run on the dpdk user space TCP/IP stack(ANS).

#### Build and Install
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
$ git clone https://github.com/ansyun/dpdk-ans.git
$ export RTE_ANS=/home/mytest/dpdk-ans
$ ./install_deps.sh
$ cd ans
$ make
$ sudo ./build/ans -c 0x2 -n 1  -- -p 0x1 --config="(0,0,1)"
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
*  Download dpdk-iperf and build dpdk-iperf3/iperf3
```
$ git clone https://github.com/ansyun/dpdk-iperf.git
dpdk-iperf3 process run on ANS tcp/ip stack.
iperf3 process run on linux kernel tcp/ip stack.

You may one of below command to compile dpdk-iperf
$ make all // make dpdk-iperf3 and iperf3
$ make dpdk-iperf // make dpdk-iperf3 
$ make iperf // make iperf3

```

*  run dpdk-iperf3 on ans side
```
/dpdk-iperf# ./dpdk_iperf3 -s --bind 10.0.0.2
EAL: Detected 40 lcore(s)
EAL: Detected 2 NUMA nodes
EAL: Multi-process socket /var/run/dpdk/rte/mp_socket_39587_4958d65583aec4
EAL: Probing VFIO support...
USER8: LCORE[-1] anssock any lcore id 0xffffffff
USER8: LCORE[10] anssock app id: 39587
USER8: LCORE[10] anssock app name: dpdk_iperf3
USER8: LCORE[10] anssock app lcoreId: 10
USER8: LCORE[10] mp ops number 4, mp ops index: 0
USER8: LCORE[10] setsockopt: not support optname 2
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
fcntl(F_GETFL): Bad file descriptor
Accepted connection from ::2300:0:0:0, port 44544
An unknown state was sent by the client, ignoring it.
fcntl(F_GETFL): Bad file descriptor
[2036] local :: port 5201 connected to :: port 44546
[ ID] Interval           Transfer     Bandwidth
[2036]   0.00-1.00   sec  1.05 GBytes  9.03 Gbits/sec
[2036]   1.00-2.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   2.00-3.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   3.00-4.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   4.00-5.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   5.00-6.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   6.00-7.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   7.00-8.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   8.00-9.00   sec  1.10 GBytes  9.41 Gbits/sec
[2036]   9.00-10.00  sec  1.10 GBytes  9.41 Gbits/sec
[2036]  10.00-10.04  sec  40.9 MBytes  9.41 Gbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth
[2036]   0.00-10.04  sec  0.00 Bytes  0.00 bits/sec                  sender
[2036]   0.00-10.04  sec  11.0 GBytes  9.38 Gbits/sec                  receiver
An unknown state was sent by the client, ignoring it.
USER8: LCORE[10] setsockopt: not support optname 2
-----------------------------------------------------------
Server listening on 5201
-----------------------------------------------------------
```
*  run iperf3 on linux side
```
/dpdk-iperf# ./iperf3 -c 10.0.0.2
Connecting to host 10.0.0.2, port 5201
[  5] local 10.0.0.10 port 44546 connected to 10.0.0.2 port 5201
[ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
[  5]   0.00-1.00   sec  1.09 GBytes  9.39 Gbits/sec    0    694 KBytes
[  5]   1.00-2.00   sec  1.10 GBytes  9.41 Gbits/sec    0    694 KBytes
[  5]   2.00-3.00   sec  1.10 GBytes  9.41 Gbits/sec    0    694 KBytes
[  5]   3.00-4.00   sec  1.10 GBytes  9.41 Gbits/sec    0    694 KBytes
[  5]   4.00-5.00   sec  1.09 GBytes  9.41 Gbits/sec    0    694 KBytes
[  5]   5.00-6.00   sec  1.10 GBytes  9.42 Gbits/sec    0    694 KBytes
[  5]   6.00-7.00   sec  1.10 GBytes  9.41 Gbits/sec    0    694 KBytes
[  5]   7.00-8.00   sec  1.10 GBytes  9.41 Gbits/sec    0    694 KBytes
[  5]   8.00-9.00   sec  1.10 GBytes  9.41 Gbits/sec    0    694 KBytes
An unknown state was sent by the client, ignoring it.
[  5]   9.00-10.00  sec  1.10 GBytes  9.41 Gbits/sec    0    694 KBytes
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bandwidth       Retr
[  5]   0.00-10.00  sec  11.0 GBytes  9.41 Gbits/sec    0             sender
[  5]   0.00-10.00  sec  11.0 GBytes  9.41 Gbits/sec                  receiver

iperf Done.

```
#### Notes
-------
- If you want to use linux iperf3 connect to dpdk-iperf3, the linux iperf3 shall be complied from dpdk-iperf project, not the open source on other website.

#### Support
-------
For free support, please use ans team mail list at anssupport@163.com, or QQ Group:86883521, or https://dpdk-ans.slack.com.

