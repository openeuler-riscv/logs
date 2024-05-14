openEuler RISC-V LLVM oec-hardware 测试结果



| 测试项目      | 测试结果 | 失败原因                                                     |
| ------------- | -------- | ------------------------------------------------------------ |
| acpi          | FAIL     | 设备不支持                                                   |
| clock         | FAIL     | 设备 rtc 未自带电池，时间不可靠                              |
| cpufreq       | FAIL     | 设备不支持调频                                               |
| disk          | PASS     |                                                              |
| dpdk          | FAIL     | 测试使用板载螃蟹网卡，不支持 DPDK                            |
| ethernet      | FAIL     | 1. 测试使用板载螃蟹网卡，不支持 Inifiniband<br>2. ip link down 后再 up 网卡反应时间较长(2~3s)<br>3. 通过 WiFi 连接到 Server，网络环境原因带宽低于测试预期值（50MB/s） |
| kabi          | PASS     |                                                              |
| kabiwhitelist | FAIL     | 没有提供预定义配置（Please configure the board information in the configuration file） |
| kdump         | FAIL     | kernel-debuginfo 软件包安装问题                              |
| memory        | PASS     |                                                              |
| nvme-nvme0n1  | FAIL     | 作为系统盘使用中，跳过此硬盘的测试                           |
| perf          | PASS     |                                                              |
| spdk-nvme0n1  | FAIL     | 版本过低不支持                                               |
| system        | FAIL     | 设备运行 kernel 版本较旧，软件仓里未包含该版本 kernel        |
| usb           | PASS     |                                                              |
| watchdog      | PASS     |                                                              |



acpi：FAIL

设备不支持

````
[2024-05-11 17:22:21,053][INFO] The command is: acpidump.
[2024-05-11 17:22:21,064][ERROR] Execute command acpidump failed.
 Cannot open directory - /sys/firmware/acpi/tablesCould not get ACPI tables, AE_NOT_FOUND
[2024-05-11 17:22:21,065][ERROR] Test acpi failed.
Cannot open directory - /sys/firmware/acpi/tablesCould not get ACPI tables, AE_NOT_FOUND
````

clock：FAIL

设备 rtc 未自带电池，时间不可靠

````
[2024-05-11 17:22:21,069][INFO] The command is: /usr/share/oech/lib/tests/compatible/clock/clock.
[2024-05-11 17:25:21,077][ERROR] Execute command /usr/share/oech/lib/tests/compatible/clock/clock failed.
 
[2024-05-11 17:25:21,078][ERROR] Test clock failed.
````

cpufreq：FAIL

设备不支持调频

````
[2024-05-11 17:25:21,083][INFO] The command is: cpupower -c 0 frequency-info -p | grep governor | cut -d '"' -f 2.
[2024-05-11 17:25:21,105][INFO] Execute command cpupower -c 0 frequency-info -p | grep governor | cut -d '"' -f 2 succeed.
 
[2024-05-11 17:25:21,106][INFO] Get cpu governor succeed.
[2024-05-11 17:25:21,108][INFO] The command is: lscpu | grep '^CPU(s):' | awk '{print $2}'.
[2024-05-11 17:25:21,135][INFO] Execute command lscpu | grep '^CPU(s):' | awk '{print $2}' succeed.
 64

[2024-05-11 17:25:21,137][INFO] Get the CPU(s) succeed.
[2024-05-11 17:25:21,138][INFO] The command is: cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq.
[2024-05-11 17:25:21,147][ERROR] Execute command cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq failed.
 cat: /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq: No such file or directory
[2024-05-11 17:25:21,148][ERROR] Get the scaling_max_freq of cpu failed.
[2024-05-11 17:25:21,149][ERROR] Fail to get CPU info.
 Please check if the CPU supports cpufreq.
````

disk：PASS

dpdk-enP2p197s0：FAIL

测试使用板载螃蟹网卡，不支持 DPDK

````
[2024-05-11 19:29:38,235][INFO] Driver Name: 
[2024-05-11 19:29:38,237][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-11 19:29:38,260][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-11 19:29:38,466][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-11 19:29:38,468][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-11 19:29:38,663][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-11 19:29:38,664][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-11 19:29:38,952][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-11 19:29:38,954][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:38,964][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:38,965][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-11 19:29:38,996][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-11 19:29:38,998][INFO] Hugepage successfully configured.
[2024-05-11 19:29:39,000][INFO] Node Pages Size Total
[2024-05-11 19:29:39,002][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:39,011][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:39,012][INFO] 2    1024  2Mb    2Gb
[2024-05-11 19:29:39,013][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:39,024][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:39,025][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:39,033][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:39,035][INFO] 0    1024  2Mb    2Gb
[2024-05-11 19:29:39,036][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:39,044][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:39,046][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:39,055][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:39,056][INFO] 3    1024  2Mb    2Gb
[2024-05-11 19:29:39,057][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:39,066][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:39,067][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:39,076][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:39,078][INFO] 1    1024  2Mb    2Gb
[2024-05-11 19:29:39,079][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:39,088][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:39,089][INFO] The command is: ethtool enP2p197s0 | grep Speed | awk '{print $2}'.
[2024-05-11 19:29:39,115][INFO] Execute command ethtool enP2p197s0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-11 19:29:39,117][INFO] The speed of enP2p197s0 is 100Mb/s.
[2024-05-11 19:29:39,118][INFO] The command is: ping -q -c 500 -i 0.001 192.168.0.102 | grep 'packet loss' | awk '{print $6}'.
[2024-05-11 19:29:41,539][INFO] Execute command ping -q -c 500 -i 0.001 192.168.0.102 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-11 19:29:41,540][INFO] Test icmp succeed.
[2024-05-11 19:29:41,541][ERROR] The card driver  doesn't support dpdk test, Supported drivers are ['mlx4_core', 'mlx5_core', 'ixgbe', 'ice', 'hinic', 'igc'].
[2024-05-11 19:29:41,543][INFO] Unbinding server card...
[2024-05-11 19:29:41,780][ERROR] Call remote server url http://192.168.0.102/api/unbind/server failed.
[2024-05-11 19:29:41,782][INFO] Unbinding client card...
[2024-05-11 19:29:41,783][INFO] The command is: dpdk-devbind.py -u 4c00000000.pcie.
[2024-05-11 19:29:42,663][ERROR] Execute command dpdk-devbind.py -u 4c00000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 4c00000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-11 19:29:42,665][INFO] The command is: dpdk-devbind.py -b  4c00000000.pcie.
[2024-05-11 19:29:42,911][ERROR] Execute command dpdk-devbind.py -b  4c00000000.pcie failed.
 Error: No devices specified.
[2024-05-11 19:29:42,912][INFO] Setting client interface enP2p197s0 up...
[2024-05-11 19:29:42,913][INFO] The command is: ip link set up enP2p197s0.
[2024-05-11 19:29:42,926][INFO] Execute command ip link set up enP2p197s0 succeed.
 
[2024-05-11 19:29:42,927][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-11 19:29:42,942][INFO] Execute command ip link show enP2p197s0 | grep 'state UP' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-11 19:29:42,944][INFO] Set interface enP2p197s0 up succeed.
[2024-05-11 19:29:43,507][INFO] Status: 200 OK
[2024-05-11 19:29:43,508][INFO] Stop all test servers.
````

dpdk-enP2p201s0：FAIL

测试使用板载螃蟹网卡，不支持 DPDK

````
2024-05-11 19:29:43,524][INFO] Driver Name: 
[2024-05-11 19:29:43,525][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-11 19:29:43,548][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-11 19:29:43,750][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-11 19:29:43,752][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-11 19:29:44,011][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-11 19:29:44,013][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-11 19:29:44,302][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-11 19:29:44,304][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:44,315][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:44,316][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-11 19:29:44,342][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-11 19:29:44,344][INFO] Hugepage successfully configured.
[2024-05-11 19:29:44,345][INFO] Node Pages Size Total
[2024-05-11 19:29:44,346][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:44,356][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:44,357][INFO] 2    1024  2Mb    2Gb
[2024-05-11 19:29:44,358][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:44,367][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:44,368][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:44,379][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:44,381][INFO] 0    1024  2Mb    2Gb
[2024-05-11 19:29:44,382][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:44,390][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:44,392][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:44,401][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:44,402][INFO] 3    1024  2Mb    2Gb
[2024-05-11 19:29:44,403][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:44,413][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:44,414][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:44,423][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:44,424][INFO] 1    1024  2Mb    2Gb
[2024-05-11 19:29:44,425][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:44,435][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:44,436][INFO] The command is: ethtool enP2p201s0 | grep Speed | awk '{print $2}'.
[2024-05-11 19:29:44,461][INFO] Execute command ethtool enP2p201s0 | grep Speed | awk '{print $2}' succeed.
 Unknown!

[2024-05-11 19:29:44,463][ERROR] Failed to run dpdk-enP2p201s0. invalid literal for int() with base 10: 'Unkn'
[2024-05-11 19:29:44,464][INFO] Unbinding server card...
[2024-05-11 19:29:44,601][ERROR] Call remote server url http://192.168.0.102/api/unbind/server failed.
[2024-05-11 19:29:44,603][INFO] Unbinding client card...
[2024-05-11 19:29:44,604][INFO] The command is: dpdk-devbind.py -u 4c00000000.pcie.
[2024-05-11 19:29:45,484][ERROR] Execute command dpdk-devbind.py -u 4c00000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 4c00000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-11 19:29:45,485][INFO] The command is: dpdk-devbind.py -b  4c00000000.pcie.
[2024-05-11 19:29:45,732][ERROR] Execute command dpdk-devbind.py -b  4c00000000.pcie failed.
 Error: No devices specified.
[2024-05-11 19:29:45,734][INFO] Setting client interface enP2p201s0 up...
[2024-05-11 19:29:45,735][INFO] The command is: ip link set up enP2p201s0.
[2024-05-11 19:29:45,746][INFO] Execute command ip link set up enP2p201s0 succeed.
 
[2024-05-11 19:29:45,747][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:45,764][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:46,765][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:46,781][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:47,783][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:47,799][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:48,800][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:48,816][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:49,818][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:49,835][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:50,837][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:50,856][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:51,858][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:51,873][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:52,874][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:52,892][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:53,894][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:53,912][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:54,914][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-11 19:29:54,929][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:55,931][ERROR] Set interface enP2p201s0 up failed.
[2024-05-11 19:29:56,353][INFO] Status: 200 OK
[2024-05-11 19:29:56,355][INFO] Stop all test servers.
````

dpdk-enP1p129s0f0：FAIL

测试使用板载螃蟹网卡，不支持 DPDK

````
[2024-05-11 19:29:56,370][INFO] Driver Name: 
[2024-05-11 19:29:56,372][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-11 19:29:56,395][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-11 19:29:56,598][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-11 19:29:56,599][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-11 19:29:56,867][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-11 19:29:56,868][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-11 19:29:57,149][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-11 19:29:57,152][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:57,162][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:57,163][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-11 19:29:57,189][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-11 19:29:57,190][INFO] Hugepage successfully configured.
[2024-05-11 19:29:57,192][INFO] Node Pages Size Total
[2024-05-11 19:29:57,193][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:57,202][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:57,204][INFO] 2    1024  2Mb    2Gb
[2024-05-11 19:29:57,204][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:57,214][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:57,216][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:57,225][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:57,226][INFO] 0    1024  2Mb    2Gb
[2024-05-11 19:29:57,228][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:57,237][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:57,239][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:57,248][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:57,249][INFO] 3    1024  2Mb    2Gb
[2024-05-11 19:29:57,250][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:57,260][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:57,261][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:29:57,271][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:29:57,272][INFO] 1    1024  2Mb    2Gb
[2024-05-11 19:29:57,273][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:29:57,282][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:29:57,284][INFO] The command is: ethtool enP1p129s0f0 | grep Speed | awk '{print $2}'.
[2024-05-11 19:29:57,309][INFO] Execute command ethtool enP1p129s0f0 | grep Speed | awk '{print $2}' succeed.
 Unknown!

[2024-05-11 19:29:57,311][ERROR] Failed to run dpdk-enP1p129s0f0. invalid literal for int() with base 10: 'Unkn'
[2024-05-11 19:29:57,312][INFO] Unbinding server card...
[2024-05-11 19:29:57,427][ERROR] Call remote server url http://192.168.0.102/api/unbind/server failed.
[2024-05-11 19:29:57,429][INFO] Unbinding client card...
[2024-05-11 19:29:57,430][INFO] The command is: dpdk-devbind.py -u 7062000000.pcie.
[2024-05-11 19:29:58,326][ERROR] Execute command dpdk-devbind.py -u 7062000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 7062000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-11 19:29:58,328][INFO] The command is: dpdk-devbind.py -b  7062000000.pcie.
[2024-05-11 19:29:58,575][ERROR] Execute command dpdk-devbind.py -b  7062000000.pcie failed.
 Error: No devices specified.
[2024-05-11 19:29:58,576][INFO] Setting client interface enP1p129s0f0 up...
[2024-05-11 19:29:58,577][INFO] The command is: ip link set up enP1p129s0f0.
[2024-05-11 19:29:58,589][INFO] Execute command ip link set up enP1p129s0f0 succeed.
 
[2024-05-11 19:29:58,591][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:29:58,606][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:29:59,607][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:29:59,622][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:00,624][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:00,639][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:01,641][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:01,657][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:02,658][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:02,674][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:03,675][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:03,691][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:04,693][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:04,708][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:05,710][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:05,725][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:06,727][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:06,743][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:07,744][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-11 19:30:07,759][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-11 19:30:08,761][ERROR] Set interface enP1p129s0f0 up failed.
[2024-05-11 19:30:09,162][INFO] Status: 200 OK
[2024-05-11 19:30:09,164][INFO] Stop all test servers.
````

dpdk-enP1p129s0f1：FAIL

测试使用板载螃蟹网卡，不支持 DPDK

````
[2024-05-11 19:30:09,179][INFO] Driver Name: 
[2024-05-11 19:30:09,181][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-11 19:30:09,205][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-11 19:30:09,408][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-11 19:30:09,409][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-11 19:30:09,672][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-11 19:30:09,673][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-11 19:30:09,952][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-11 19:30:09,955][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-11 19:30:09,964][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:30:09,965][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-11 19:30:09,992][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-11 19:30:09,993][INFO] Hugepage successfully configured.
[2024-05-11 19:30:09,995][INFO] Node Pages Size Total
[2024-05-11 19:30:09,997][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:30:10,006][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:30:10,007][INFO] 2    1024  2Mb    2Gb
[2024-05-11 19:30:10,008][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:30:10,018][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:30:10,019][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:30:10,028][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:30:10,029][INFO] 0    1024  2Mb    2Gb
[2024-05-11 19:30:10,030][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:30:10,040][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:30:10,041][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:30:10,051][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:30:10,052][INFO] 3    1024  2Mb    2Gb
[2024-05-11 19:30:10,053][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:30:10,063][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:30:10,064][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-11 19:30:10,074][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-11 19:30:10,075][INFO] 1    1024  2Mb    2Gb
[2024-05-11 19:30:10,076][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-11 19:30:10,086][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-11 19:30:10,087][INFO] The command is: ethtool enP1p129s0f1 | grep Speed | awk '{print $2}'.
[2024-05-11 19:30:10,111][INFO] Execute command ethtool enP1p129s0f1 | grep Speed | awk '{print $2}' succeed.
 Unknown!

[2024-05-11 19:30:10,113][ERROR] Failed to run dpdk-enP1p129s0f1. invalid literal for int() with base 10: 'Unkn'
[2024-05-11 19:30:10,114][INFO] Unbinding server card...
[2024-05-11 19:30:10,236][ERROR] Call remote server url http://192.168.0.102/api/unbind/server failed.
[2024-05-11 19:30:10,237][INFO] Unbinding client card...
[2024-05-11 19:30:10,239][INFO] The command is: dpdk-devbind.py -u 7062000000.pcie.
[2024-05-11 19:30:11,127][ERROR] Execute command dpdk-devbind.py -u 7062000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 7062000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-11 19:30:11,128][INFO] The command is: dpdk-devbind.py -b  7062000000.pcie.
[2024-05-11 19:30:11,378][ERROR] Execute command dpdk-devbind.py -b  7062000000.pcie failed.
 Error: No devices specified.
[2024-05-11 19:30:11,379][INFO] Setting client interface enP1p129s0f1 up...
[2024-05-11 19:30:11,380][INFO] The command is: ip link set up enP1p129s0f1.
[2024-05-11 19:30:11,392][INFO] Execute command ip link set up enP1p129s0f1 succeed.
 
[2024-05-11 19:30:11,393][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:11,412][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:12,413][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:12,432][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:13,433][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:13,449][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:14,450][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:14,468][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:15,470][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:15,486][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:16,487][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:16,503][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:17,505][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:17,521][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:18,523][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:18,538][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:19,540][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:19,555][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:20,557][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-11 19:30:20,572][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-11 19:30:21,574][ERROR] Set interface enP1p129s0f1 up failed.
[2024-05-11 19:30:21,988][INFO] Status: 200 OK
[2024-05-11 19:30:21,989][INFO] Stop all test servers.
````

ethernet-enP2p197s0：FAIL

- 测试使用板载螃蟹网卡，不支持 Inifiniband
- ip link down 后再 up 网卡反应时间较长（2~3s）
- 通过 WiFi 连接到 Server，网络环境原因带宽低于测试预期值（50MB/s）

````
[2024-05-11 19:30:21,994][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-11 19:30:22,011][INFO] Execute command ip link show enP2p197s0 | grep 'state UP' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-11 19:30:22,012][INFO] The command is: ifconfig enP2p197s0 | grep '.*inet' | awk '{print $2}'.
[2024-05-11 19:30:22,038][INFO] Execute command ifconfig enP2p197s0 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.105
fe80::3093:b23e:ace5:e73e

[2024-05-11 19:30:22,040][INFO] The command is: ifconfig enP2p197s0 | grep '.*ether' | awk '{print $2}'.
[2024-05-11 19:30:22,064][INFO] Execute command ifconfig enP2p197s0 | grep '.*ether' | awk '{print $2}' succeed.
 00:e0:4c:68:00:7b

[2024-05-11 19:30:22,066][INFO] The client IP address already configured.
[2024-05-11 19:30:22,067][INFO] The command is: ping -q -c 1 -W 1 192.168.0.102 | grep 'packet loss' | awk '{print $6}'.
[2024-05-11 19:30:22,103][INFO] Execute command ping -q -c 1 -W 1 192.168.0.102 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-11 19:30:22,117][INFO] Driver Name: 
[2024-05-11 19:30:22,118][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-11 19:30:22,120][INFO] The command is: ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:06.0/0002:c5:00.0/ | grep -q infiniband.
[2024-05-11 19:30:22,136][ERROR] Execute command ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:06.0/0002:c5:00.0/ | grep -q infiniband failed.
 
[2024-05-11 19:30:22,138][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-11 19:30:22,139][INFO] It will test normal ethernet enP2p197s0.
[2024-05-11 19:30:22,140][INFO] The command is: ethtool enP2p197s0 | grep 'Port' | awk '{print $2}'.
[2024-05-11 19:30:22,164][INFO] Execute command ethtool enP2p197s0 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-11 19:30:22,166][INFO] The enP2p197s0 port type is Twisted, skip checking.
[2024-05-11 19:30:22,167][INFO] The test interface is enP2p197s0.
[2024-05-11 19:30:22,168][INFO] The server ip is 192.168.0.102.
[2024-05-11 19:30:22,169][INFO] The client ip is 192.168.0.105
fe80::3093:b23e:ace5:e73e
 on enP2p197s0.
[2024-05-11 19:30:22,170][INFO] Setting interface enP2p197s0 down.
[2024-05-11 19:30:22,171][INFO] The command is: ip link set down enP2p197s0.
[2024-05-11 19:30:22,201][INFO] Execute command ip link set down enP2p197s0 succeed.
 
[2024-05-11 19:30:22,203][INFO] The command is: ip link show enP2p197s0 | grep 'state DOWN'.
[2024-05-11 19:30:22,218][INFO] Execute command ip link show enP2p197s0 | grep 'state DOWN' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN mode DEFAULT group default qlen 1000

[2024-05-11 19:30:22,220][INFO] Set interface enP2p197s0 down succeed.
[2024-05-11 19:30:22,221][INFO] Setting interface enP2p197s0 up.
[2024-05-11 19:30:22,221][INFO] The command is: ip link set up enP2p197s0.
[2024-05-11 19:30:22,433][INFO] Execute command ip link set up enP2p197s0 succeed.
 
[2024-05-11 19:30:22,434][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-11 19:30:22,454][ERROR] Execute command ip link show enP2p197s0 | grep 'state UP' failed.
 
[2024-05-11 19:30:23,456][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-11 19:30:23,471][ERROR] Execute command ip link show enP2p197s0 | grep 'state UP' failed.
 
[2024-05-11 19:30:24,472][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-11 19:30:24,488][INFO] Execute command ip link show enP2p197s0 | grep 'state UP' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-11 19:30:24,489][INFO] Set interface enP2p197s0 up succeed.
[2024-05-11 19:30:24,490][INFO] The command is: ethtool enP2p197s0 | grep Speed | awk '{print $2}'.
[2024-05-11 19:30:24,515][INFO] Execute command ethtool enP2p197s0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-11 19:30:24,517][INFO] The speed of enP2p197s0 is 100Mb/s.
[2024-05-11 19:30:24,518][INFO] The command is: ping -q -c 500 -i 0.001 192.168.0.102 | grep 'packet loss' | awk '{print $6}'.
[2024-05-11 19:30:27,699][INFO] Execute command ping -q -c 500 -i 0.001 192.168.0.102 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-11 19:30:27,700][INFO] Test icmp succeed.
[2024-05-11 19:30:30,773][INFO] Status: 200 OK
[2024-05-11 19:30:30,775][INFO] Testing udp latency...
[2024-05-11 19:30:30,776][INFO] The command is: qperf 192.168.0.102 udp_lat.
[2024-05-11 19:30:32,914][INFO] Execute command qperf 192.168.0.102 udp_lat succeed.
 udp_lat:
    latency  =  4.82 ms

[2024-05-11 19:30:32,915][INFO] The command is: qperf 192.168.0.102 udp_lat.
[2024-05-11 19:30:34,960][INFO] Execute command qperf 192.168.0.102 udp_lat succeed.
 udp_lat:
    latency  =  5.39 ms

[2024-05-11 19:30:34,961][INFO] The command is: qperf 192.168.0.102 udp_lat.
[2024-05-11 19:30:37,088][INFO] Execute command qperf 192.168.0.102 udp_lat succeed.
 udp_lat:
    latency  =  5.63 ms

[2024-05-11 19:30:37,089][INFO] Testing tcp latency...
[2024-05-11 19:30:37,090][INFO] The command is: qperf 192.168.0.102 tcp_lat.
[2024-05-11 19:30:39,384][INFO] Execute command qperf 192.168.0.102 tcp_lat succeed.
 tcp_lat:
    latency  =  7.66 ms

[2024-05-11 19:30:39,385][INFO] The command is: qperf 192.168.0.102 tcp_lat.
[2024-05-11 19:30:41,460][INFO] Execute command qperf 192.168.0.102 tcp_lat succeed.
 tcp_lat:
    latency  =  5.38 ms

[2024-05-11 19:30:41,461][INFO] The command is: qperf 192.168.0.102 tcp_lat.
[2024-05-11 19:30:43,516][INFO] Execute command qperf 192.168.0.102 tcp_lat succeed.
 tcp_lat:
    latency  =  3.5 ms

[2024-05-11 19:30:43,518][INFO] Testing tcp bandwidth...
[2024-05-11 19:30:43,519][INFO] The command is: qperf 192.168.0.102 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-11 19:30:45,630][INFO] Execute command qperf 192.168.0.102 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 3.87 MB/sec

[2024-05-11 19:30:45,632][INFO] Current bandwidth is 30.96Mb/s, target is 50.00Mb/s
[2024-05-11 19:30:45,633][INFO] The command is: qperf 192.168.0.102 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-11 19:30:47,702][INFO] Execute command qperf 192.168.0.102 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 5.05 MB/sec

[2024-05-11 19:30:47,704][INFO] Current bandwidth is 40.40Mb/s, target is 50.00Mb/s
[2024-05-11 19:30:47,705][INFO] The command is: qperf 192.168.0.102 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-11 19:30:49,932][INFO] Execute command qperf 192.168.0.102 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 4.39 MB/sec

[2024-05-11 19:30:49,934][INFO] Current bandwidth is 35.12Mb/s, target is 50.00Mb/s
[2024-05-11 19:30:49,936][ERROR] Test tcp bandwidth failed.
[2024-05-11 19:30:49,937][INFO] Stop all test servers.
[2024-05-11 19:30:53,368][INFO] Status: 200 OK
[2024-05-11 19:30:53,370][INFO] The command is: ifconfig enP2p197s0:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-11 19:30:53,394][INFO] Execute command ifconfig enP2p197s0:0 | grep '.*inet' | awk '{print $2}' succeed.
````

ethernet-enP2p201s0：FAIL

- 测试使用板载螃蟹网卡，不支持 Inifiniband
- ip link down 后再 up 网卡反应时间较长（2~3s）
- 通过 WiFi 连接到 Server，网络环境原因带宽低于测试预期值（50MB/s）

````
[2024-05-13 10:20:07,285][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-13 10:20:07,302][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 3: enP2p201s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-13 10:20:07,304][INFO] The command is: ifconfig enP2p201s0 | grep '.*inet' | awk '{print $2}'.
[2024-05-13 10:20:07,329][INFO] Execute command ifconfig enP2p201s0 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.106
fe80::112a:575d:6d84:a424

[2024-05-13 10:20:07,331][INFO] The command is: ifconfig enP2p201s0 | grep '.*ether' | awk '{print $2}'.
[2024-05-13 10:20:07,358][INFO] Execute command ifconfig enP2p201s0 | grep '.*ether' | awk '{print $2}' succeed.
 00:e0:4c:68:00:7c

[2024-05-13 10:20:07,360][INFO] The client IP address already configured.
[2024-05-13 10:20:07,361][INFO] The command is: ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-13 10:20:07,410][INFO] Execute command ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-13 10:20:07,422][INFO] Driver Name: 
[2024-05-13 10:20:07,423][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-13 10:20:07,424][INFO] The command is: ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:0e.0/0002:c9:00.0/ | grep -q infiniband.
[2024-05-13 10:20:07,439][ERROR] Execute command ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:0e.0/0002:c9:00.0/ | grep -q infiniband failed.
 
[2024-05-13 10:20:07,441][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-13 10:20:07,442][INFO] It will test normal ethernet enP2p201s0.
[2024-05-13 10:20:07,443][INFO] The command is: ethtool enP2p201s0 | grep 'Port' | awk '{print $2}'.
[2024-05-13 10:20:07,468][INFO] Execute command ethtool enP2p201s0 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-13 10:20:07,470][INFO] The enP2p201s0 port type is Twisted, skip checking.
[2024-05-13 10:20:07,471][INFO] The test interface is enP2p201s0.
[2024-05-13 10:20:07,471][INFO] The server ip is 192.168.0.103.
[2024-05-13 10:20:07,472][INFO] The client ip is 192.168.0.106
fe80::112a:575d:6d84:a424
 on enP2p201s0.
[2024-05-13 10:20:07,473][INFO] Setting interface enP2p201s0 down.
[2024-05-13 10:20:07,474][INFO] The command is: ip link set down enP2p201s0.
[2024-05-13 10:20:07,503][INFO] Execute command ip link set down enP2p201s0 succeed.
 
[2024-05-13 10:20:07,505][INFO] The command is: ip link show enP2p201s0 | grep 'state DOWN'.
[2024-05-13 10:20:07,520][INFO] Execute command ip link show enP2p201s0 | grep 'state DOWN' succeed.
 3: enP2p201s0: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN mode DEFAULT group default qlen 1000

[2024-05-13 10:20:07,521][INFO] Set interface enP2p201s0 down succeed.
[2024-05-13 10:20:07,522][INFO] Setting interface enP2p201s0 up.
[2024-05-13 10:20:07,523][INFO] The command is: ip link set up enP2p201s0.
[2024-05-13 10:20:07,775][INFO] Execute command ip link set up enP2p201s0 succeed.
 
[2024-05-13 10:20:07,776][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-13 10:20:07,795][ERROR] Execute command ip link show enP2p201s0 | grep 'state UP' failed.
 
[2024-05-13 10:20:08,797][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-13 10:20:08,811][ERROR] Execute command ip link show enP2p201s0 | grep 'state UP' failed.
 
[2024-05-13 10:20:09,813][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-13 10:20:09,828][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 3: enP2p201s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-13 10:20:09,829][INFO] Set interface enP2p201s0 up succeed.
[2024-05-13 10:20:09,830][INFO] The command is: ethtool enP2p201s0 | grep Speed | awk '{print $2}'.
[2024-05-13 10:20:09,853][INFO] Execute command ethtool enP2p201s0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-13 10:20:09,855][INFO] The speed of enP2p201s0 is 100Mb/s.
[2024-05-13 10:20:09,856][INFO] The command is: ping -q -c 500 -i 0.001 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-13 10:20:11,971][INFO] Execute command ping -q -c 500 -i 0.001 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-13 10:20:11,973][INFO] Test icmp succeed.
[2024-05-13 10:20:14,789][INFO] Status: 200 OK
[2024-05-13 10:20:14,791][INFO] Testing udp latency...
[2024-05-13 10:20:14,792][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:20:16,852][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  2.16 ms

[2024-05-13 10:20:16,853][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:20:18,872][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  2.13 ms

[2024-05-13 10:20:18,873][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:20:20,913][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  3.09 ms

[2024-05-13 10:20:20,914][INFO] Testing tcp latency...
[2024-05-13 10:20:20,915][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:20:22,950][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  2.33 ms

[2024-05-13 10:20:22,951][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:20:24,994][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  2.27 ms

[2024-05-13 10:20:24,996][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:20:27,023][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  2.7 ms

[2024-05-13 10:20:27,025][INFO] Testing tcp bandwidth...
[2024-05-13 10:20:27,026][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:20:29,072][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 5.41 MB/sec

[2024-05-13 10:20:29,074][INFO] Current bandwidth is 43.28Mb/s, target is 50.00Mb/s
[2024-05-13 10:20:29,075][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:20:31,162][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 6.06 MB/sec

[2024-05-13 10:20:31,165][INFO] Current bandwidth is 48.48Mb/s, target is 50.00Mb/s
[2024-05-13 10:20:31,166][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:20:33,238][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 6.16 MB/sec

[2024-05-13 10:20:33,239][INFO] Current bandwidth is 49.28Mb/s, target is 50.00Mb/s
[2024-05-13 10:20:33,241][ERROR] Test tcp bandwidth failed.
[2024-05-13 10:20:33,242][INFO] Stop all test servers.
[2024-05-13 10:20:36,401][INFO] Status: 200 OK
[2024-05-13 10:20:36,403][INFO] The command is: ifconfig enP2p201s0:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-13 10:20:36,426][INFO] Execute command ifconfig enP2p201s0:0 | grep '.*inet' | awk '{print $2}' succeed.
````

ethernet-enP1p129s0f0：FAIL

- 测试使用板载螃蟹网卡，不支持 Inifiniband
- ip link down 后再 up 网卡反应时间较长（2~3s）
- 通过 WiFi 连接到 Server，网络环境原因带宽低于测试预期值（50MB/s）

````
[2024-05-13 10:31:57,174][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-13 10:31:57,191][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 4: enP1p129s0f0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-13 10:31:57,192][INFO] The command is: ifconfig enP1p129s0f0 | grep '.*inet' | awk '{print $2}'.
[2024-05-13 10:31:57,217][INFO] Execute command ifconfig enP1p129s0f0 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.107
fe80::3ad9:8d4c:2c19:becd

[2024-05-13 10:31:57,219][INFO] The command is: ifconfig enP1p129s0f0 | grep '.*ether' | awk '{print $2}'.
[2024-05-13 10:31:57,243][INFO] Execute command ifconfig enP1p129s0f0 | grep '.*ether' | awk '{print $2}' succeed.
 a0:36:9f:54:0c:c8

[2024-05-13 10:31:57,244][INFO] The client IP address already configured.
[2024-05-13 10:31:57,246][INFO] The command is: ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-13 10:31:57,296][INFO] Execute command ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-13 10:31:57,309][INFO] Driver Name: 
[2024-05-13 10:31:57,311][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-13 10:31:57,311][INFO] The command is: ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.0/ | grep -q infiniband.
[2024-05-13 10:31:57,328][ERROR] Execute command ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.0/ | grep -q infiniband failed.
 
[2024-05-13 10:31:57,329][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-13 10:31:57,330][INFO] It will test normal ethernet enP1p129s0f0.
[2024-05-13 10:31:57,331][INFO] The command is: ethtool enP1p129s0f0 | grep 'Port' | awk '{print $2}'.
[2024-05-13 10:31:57,357][INFO] Execute command ethtool enP1p129s0f0 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-13 10:31:57,358][INFO] The enP1p129s0f0 port type is Twisted, skip checking.
[2024-05-13 10:31:57,359][INFO] The test interface is enP1p129s0f0.
[2024-05-13 10:31:57,361][INFO] The server ip is 192.168.0.103.
[2024-05-13 10:31:57,362][INFO] The client ip is 192.168.0.107
fe80::3ad9:8d4c:2c19:becd
 on enP1p129s0f0.
[2024-05-13 10:31:57,363][INFO] Setting interface enP1p129s0f0 down.
[2024-05-13 10:31:57,364][INFO] The command is: ip link set down enP1p129s0f0.
[2024-05-13 10:31:57,724][INFO] Execute command ip link set down enP1p129s0f0 succeed.
 
[2024-05-13 10:31:57,725][INFO] The command is: ip link show enP1p129s0f0 | grep 'state DOWN'.
[2024-05-13 10:31:57,741][INFO] Execute command ip link show enP1p129s0f0 | grep 'state DOWN' succeed.
 4: enP1p129s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc mq state DOWN mode DEFAULT group default qlen 1000

[2024-05-13 10:31:57,742][INFO] Set interface enP1p129s0f0 down succeed.
[2024-05-13 10:31:57,743][INFO] Setting interface enP1p129s0f0 up.
[2024-05-13 10:31:57,744][INFO] The command is: ip link set up enP1p129s0f0.
[2024-05-13 10:31:57,909][INFO] Execute command ip link set up enP1p129s0f0 succeed.
 
[2024-05-13 10:31:57,910][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-13 10:31:57,926][ERROR] Execute command ip link show enP1p129s0f0 | grep 'state UP' failed.
 
[2024-05-13 10:31:58,927][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-13 10:31:58,942][ERROR] Execute command ip link show enP1p129s0f0 | grep 'state UP' failed.
 
[2024-05-13 10:31:59,944][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-13 10:31:59,959][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 4: enP1p129s0f0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-13 10:31:59,960][INFO] Set interface enP1p129s0f0 up succeed.
[2024-05-13 10:31:59,961][INFO] The command is: ethtool enP1p129s0f0 | grep Speed | awk '{print $2}'.
[2024-05-13 10:31:59,985][INFO] Execute command ethtool enP1p129s0f0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-13 10:31:59,987][INFO] The speed of enP1p129s0f0 is 100Mb/s.
[2024-05-13 10:31:59,988][INFO] The command is: ping -q -c 500 -i 0.001 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-13 10:32:02,694][INFO] Execute command ping -q -c 500 -i 0.001 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-13 10:32:02,696][INFO] Test icmp succeed.
[2024-05-13 10:32:05,496][INFO] Status: 200 OK
[2024-05-13 10:32:05,498][INFO] Testing udp latency...
[2024-05-13 10:32:05,499][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:32:07,585][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  4.13 ms

[2024-05-13 10:32:07,586][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:32:09,619][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  3.68 ms

[2024-05-13 10:32:09,621][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:32:11,664][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  6.71 ms

[2024-05-13 10:32:11,666][INFO] Testing tcp latency...
[2024-05-13 10:32:11,666][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:32:13,714][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  3.48 ms

[2024-05-13 10:32:13,730][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:32:15,780][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  3.13 ms

[2024-05-13 10:32:15,782][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:32:17,815][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  3.22 ms

[2024-05-13 10:32:17,817][INFO] Testing tcp bandwidth...
[2024-05-13 10:32:17,819][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:32:19,864][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 4.06 MB/sec

[2024-05-13 10:32:19,867][INFO] Current bandwidth is 32.48Mb/s, target is 50.00Mb/s
[2024-05-13 10:32:19,868][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:32:21,937][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 3.8 MB/sec

[2024-05-13 10:32:21,939][INFO] Current bandwidth is 30.40Mb/s, target is 50.00Mb/s
[2024-05-13 10:32:21,940][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:32:23,970][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 4.29 MB/sec

[2024-05-13 10:32:23,972][INFO] Current bandwidth is 34.32Mb/s, target is 50.00Mb/s
[2024-05-13 10:32:23,973][ERROR] Test tcp bandwidth failed.
[2024-05-13 10:32:23,975][INFO] Stop all test servers.
[2024-05-13 10:32:27,159][INFO] Status: 200 OK
[2024-05-13 10:32:27,162][INFO] The command is: ifconfig enP1p129s0f0:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-13 10:32:27,186][INFO] Execute command ifconfig enP1p129s0f0:0 | grep '.*inet' | awk '{print $2}' succeed.
````

ethernet-enP1p129s0f1：FAIL

- 测试使用板载螃蟹网卡，不支持 Inifiniband
- ip link down 后再 up 网卡反应时间较长（2~3s）
- 通过 WiFi 连接到 Server，网络环境原因带宽低于测试预期值（50MB/s）

````
[2024-05-13 10:26:20,458][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-13 10:26:20,473][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 5: enP1p129s0f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-13 10:26:20,475][INFO] The command is: ifconfig enP1p129s0f1 | grep '.*inet' | awk '{print $2}'.
[2024-05-13 10:26:20,499][INFO] Execute command ifconfig enP1p129s0f1 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.105
fe80::3433:122d:ab8f:5a39

[2024-05-13 10:26:20,500][INFO] The command is: ifconfig enP1p129s0f1 | grep '.*ether' | awk '{print $2}'.
[2024-05-13 10:26:20,525][INFO] Execute command ifconfig enP1p129s0f1 | grep '.*ether' | awk '{print $2}' succeed.
 a0:36:9f:54:0c:ca

[2024-05-13 10:26:20,527][INFO] The client IP address already configured.
[2024-05-13 10:26:20,528][INFO] The command is: ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-13 10:26:20,627][INFO] Execute command ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-13 10:26:20,640][INFO] Driver Name: 
[2024-05-13 10:26:20,641][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-13 10:26:20,642][INFO] The command is: ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.1/ | grep -q infiniband.
[2024-05-13 10:26:20,659][ERROR] Execute command ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.1/ | grep -q infiniband failed.
 
[2024-05-13 10:26:20,660][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-13 10:26:20,661][INFO] It will test normal ethernet enP1p129s0f1.
[2024-05-13 10:26:20,662][INFO] The command is: ethtool enP1p129s0f1 | grep 'Port' | awk '{print $2}'.
[2024-05-13 10:26:20,685][INFO] Execute command ethtool enP1p129s0f1 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-13 10:26:20,687][INFO] The enP1p129s0f1 port type is Twisted, skip checking.
[2024-05-13 10:26:20,688][INFO] The test interface is enP1p129s0f1.
[2024-05-13 10:26:20,689][INFO] The server ip is 192.168.0.103.
[2024-05-13 10:26:20,690][INFO] The client ip is 192.168.0.105
fe80::3433:122d:ab8f:5a39
 on enP1p129s0f1.
[2024-05-13 10:26:20,691][INFO] Setting interface enP1p129s0f1 down.
[2024-05-13 10:26:20,692][INFO] The command is: ip link set down enP1p129s0f1.
[2024-05-13 10:26:21,056][INFO] Execute command ip link set down enP1p129s0f1 succeed.
 
[2024-05-13 10:26:21,057][INFO] The command is: ip link show enP1p129s0f1 | grep 'state DOWN'.
[2024-05-13 10:26:21,072][INFO] Execute command ip link show enP1p129s0f1 | grep 'state DOWN' succeed.
 5: enP1p129s0f1: <BROADCAST,MULTICAST> mtu 1500 qdisc mq state DOWN mode DEFAULT group default qlen 1000

[2024-05-13 10:26:21,073][INFO] Set interface enP1p129s0f1 down succeed.
[2024-05-13 10:26:21,074][INFO] Setting interface enP1p129s0f1 up.
[2024-05-13 10:26:21,075][INFO] The command is: ip link set up enP1p129s0f1.
[2024-05-13 10:26:21,241][INFO] Execute command ip link set up enP1p129s0f1 succeed.
 
[2024-05-13 10:26:21,242][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-13 10:26:21,257][ERROR] Execute command ip link show enP1p129s0f1 | grep 'state UP' failed.
 
[2024-05-13 10:26:22,259][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-13 10:26:22,274][ERROR] Execute command ip link show enP1p129s0f1 | grep 'state UP' failed.
 
[2024-05-13 10:26:23,275][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-13 10:26:23,291][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 5: enP1p129s0f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-13 10:26:23,292][INFO] Set interface enP1p129s0f1 up succeed.
[2024-05-13 10:26:23,293][INFO] The command is: ethtool enP1p129s0f1 | grep Speed | awk '{print $2}'.
[2024-05-13 10:26:23,317][INFO] Execute command ethtool enP1p129s0f1 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-13 10:26:23,318][INFO] The speed of enP1p129s0f1 is 100Mb/s.
[2024-05-13 10:26:23,319][INFO] The command is: ping -q -c 500 -i 0.001 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-13 10:26:25,754][INFO] Execute command ping -q -c 500 -i 0.001 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-13 10:26:25,755][INFO] Test icmp succeed.
[2024-05-13 10:26:28,571][INFO] Status: 200 OK
[2024-05-13 10:26:28,573][INFO] Testing udp latency...
[2024-05-13 10:26:28,574][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:26:30,601][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  3.1 ms

[2024-05-13 10:26:30,602][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:26:32,624][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  2.94 ms

[2024-05-13 10:26:32,625][INFO] The command is: qperf 192.168.0.103 udp_lat.
[2024-05-13 10:26:34,652][INFO] Execute command qperf 192.168.0.103 udp_lat succeed.
 udp_lat:
    latency  =  3.03 ms

[2024-05-13 10:26:34,653][INFO] Testing tcp latency...
[2024-05-13 10:26:34,654][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:26:36,711][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  3.5 ms

[2024-05-13 10:26:36,713][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:26:38,757][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  3.13 ms

[2024-05-13 10:26:38,758][INFO] The command is: qperf 192.168.0.103 tcp_lat.
[2024-05-13 10:26:40,809][INFO] Execute command qperf 192.168.0.103 tcp_lat succeed.
 tcp_lat:
    latency  =  3.05 ms

[2024-05-13 10:26:40,810][INFO] Testing tcp bandwidth...
[2024-05-13 10:26:40,811][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:26:42,855][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 3.93 MB/sec

[2024-05-13 10:26:42,857][INFO] Current bandwidth is 31.44Mb/s, target is 50.00Mb/s
[2024-05-13 10:26:42,858][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:26:44,904][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 3.77 MB/sec

[2024-05-13 10:26:44,906][INFO] Current bandwidth is 30.16Mb/s, target is 50.00Mb/s
[2024-05-13 10:26:44,907][INFO] The command is: qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}'.
[2024-05-13 10:26:46,952][INFO] Execute command qperf 192.168.0.103 tcp_bw | grep 'bw' | grep -v 'tcp_bw' | awk '{print $3,$4}' succeed.
 4.55 MB/sec

[2024-05-13 10:26:46,954][INFO] Current bandwidth is 36.40Mb/s, target is 50.00Mb/s
[2024-05-13 10:26:46,955][ERROR] Test tcp bandwidth failed.
[2024-05-13 10:26:46,956][INFO] Stop all test servers.
[2024-05-13 10:26:50,145][INFO] Status: 200 OK
[2024-05-13 10:26:50,147][INFO] The command is: ifconfig enP1p129s0f1:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-13 10:26:50,170][INFO] Execute command ifconfig enP1p129s0f1:0 | grep '.*inet' | awk '{print $2}' succeed.
````

kabi：PASS

kabiwhitelist：FAIL

没有提供预定义配置（Please configure the board information in the configuration file） 

````
[2024-05-11 19:30:53,425][INFO] The command is: bash /usr/share/oech/lib/tests/compatible/kabiwhitelist/kabi_check.sh.
[2024-05-11 19:30:54,258][INFO] Execute command bash /usr/share/oech/lib/tests/compatible/kabiwhitelist/kabi_check.sh succeed.
 ####################KABI TEST START####################
Please configure the board information in the configuration file
Test results are as follows

[2024-05-11 19:30:54,259][INFO] The command is: ls /usr/share/oech/lib/tests/compatible/kabiwhitelist/test_log/ | grep noko.
[2024-05-11 19:30:54,276][INFO] Execute command ls /usr/share/oech/lib/tests/compatible/kabiwhitelist/test_log/ | grep noko succeed.
 nokorpm.txt

[2024-05-11 19:30:54,278][ERROR] Please configure the board information in the configuration file
[2024-05-11 19:30:54,282][INFO] Clearing temporary files is complete
````

kdump：FAIL

kernel-debuginfo 软件包安装问题

````
[2024-05-11 22:15:07,736][INFO] The command is: systemctl daemon-reload.
[2024-05-11 22:15:08,637][INFO] Execute command systemctl daemon-reload succeed.
 
[2024-05-11 22:15:08,638][INFO] The command is: systemctl enable oech.
[2024-05-11 22:15:09,528][INFO] Execute command systemctl enable oech succeed.
 
[2024-05-11 22:15:09,530][INFO] The command is: yum install -y kernel-debuginfo-6.6.0-19.0.0.21.mg2403.riscv64.
[2024-05-11 22:15:12,769][ERROR] Execute command yum install -y kernel-debuginfo-6.6.0-19.0.0.21.mg2403.riscv64 failed.
 Error: Unable to find a match: kernel-debuginfo-6.6.0-19.0.0.21.mg2403.riscv64
[2024-05-11 22:15:12,770][ERROR] Fail to install required packages.
 Error: Unable to find a match: kernel-debuginfo-6.6.0-19.0.0.21.mg2403.riscv64
````

nvme-nvme0n1：FAIL

作为系统盘使用中，跳过此硬盘的测试

````
[2024-05-11 21:48:12,958][INFO] Driver Name: 
[2024-05-11 21:48:12,960][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-11 21:48:12,962][INFO] The command is: nvme list.
[2024-05-11 21:48:13,033][INFO] Execute command nvme list succeed.
 Node                  Generic               SN                   Model                                    Namespace  Usage                      Format           FW Rev  
--------------------- --------------------- -------------------- ---------------------------------------- ---------- -------------------------- ---------------- --------
/dev/nvme0n1          /dev/ng0n1            NEV4642004130        FORESEE XP1000F001T                      0x1          1.02  TB /   1.02  TB    512   B +  0 B   V1.28   

[2024-05-11 21:48:13,034][INFO] The command is: /usr/sbin/swapon -a.
[2024-05-11 21:48:13,065][INFO] Execute command /usr/sbin/swapon -a succeed.
 
[2024-05-11 21:48:13,067][ERROR] nvme0n1 is in use now, skip this test.
````

perf：PASS

spdk-nvme0n1：FAIL

版本过低不支持

````
[2024-05-11 21:48:31,343][ERROR] The spdk version is too low and needs to be upgraded to 21.01.1-5.
[2024-05-11 21:48:31,345][ERROR] Unload uio_pci_generic driver failed.
````

system：FAIL

设备运行 kernel 版本较旧，软件仓里未包含该版本 kernel

````
[2024-05-11 22:02:35,281][INFO] The command is: uname -a.
[2024-05-11 22:02:35,291][INFO] Execute command uname -a succeed.
 Linux openeuler-riscv64 6.6.0-19.0.0.21.mg2403.riscv64 #1 SMP Mon May  6 09:52:52 UTC 2024 riscv64 riscv64 riscv64 GNU/Linux

[2024-05-11 22:02:35,292][INFO] The command is: lsmod.
[2024-05-11 22:02:35,321][INFO] Execute command lsmod succeed.
 Module                  Size  Used by
binfmt_misc            28672  1
sg                     65536  0
dm_mod                204800  0
nft_fib_inet           12288  1
nft_fib_ipv4           12288  1 nft_fib_inet
nft_fib_ipv6           12288  1 nft_fib_inet
nft_fib                12288  3 nft_fib_ipv6,nft_fib_ipv4,nft_fib_inet
nft_reject_inet        12288  6
nf_reject_ipv4         12288  1 nft_reject_inet
nf_reject_ipv6         20480  1 nft_reject_inet
nft_reject             12288  1 nft_reject_inet
nft_ct                 20480  11
nft_chain_nat          12288  3
amdgpu               6922240  0
nf_tables             299008  206 nft_ct,nft_reject_inet,nft_fib_ipv6,nft_fib_ipv4,nft_chain_nat,nft_reject,nft_fib,nft_fib_inet
ebtable_nat            12288  0
ebtable_broute         12288  0
ip6table_nat           12288  0
ip6table_mangle        12288  0
ip6table_raw           12288  0
ip6table_security      12288  0
iptable_nat            12288  0
nf_nat                 61440  3 ip6table_nat,nft_chain_nat,iptable_nat
nf_conntrack          221184  2 nf_nat,nft_ct
nf_defrag_ipv6         28672  1 nf_conntrack
nf_defrag_ipv4         12288  1 nf_conntrack
libcrc32c              12288  3 nf_conntrack,nf_nat,nf_tables
iptable_mangle         12288  0
iptable_raw            12288  0
iptable_security       12288  0
rfkill                 45056  0
ip_set                 69632  0
ebtable_filter         12288  0
ebtables               49152  3 ebtable_nat,ebtable_filter,ebtable_broute
ip6table_filter        12288  0
ip6_tables             28672  5 ip6table_filter,ip6table_raw,ip6table_nat,ip6table_mangle,ip6table_security
iptable_filter         12288  0
ip_tables              28672  5 iptable_filter,iptable_security,iptable_raw,iptable_nat,iptable_mangle
amdxcp                 12288  1 amdgpu
drm_exec               12288  1 amdgpu
gpu_sched              53248  1 amdgpu
drm_buddy              20480  1 amdgpu
radeon               2023424  2
snd_hda_intel          57344  0
snd_intel_dspcfg       12288  1 snd_hda_intel
snd_hda_codec         188416  1 snd_hda_intel
snd_hda_core          143360  2 snd_hda_intel,snd_hda_codec
drm_suballoc_helper    16384  2 amdgpu,radeon
snd_pcm               184320  3 snd_hda_intel,snd_hda_codec,snd_hda_core
drm_display_helper    212992  2 amdgpu,radeon
ixgbe                 491520  0
snd_timer              49152  1 snd_pcm
drm_ttm_helper         12288  2 amdgpu,radeon
snd                   131072  4 snd_hda_intel,snd_hda_codec,snd_timer,snd_pcm
ttm                   102400  3 amdgpu,radeon,drm_ttm_helper
xfrm_algo              20480  1 ixgbe
soundcore              12288  1 snd
mdio                   12288  1 ixgbe
uio_pdrv_genirq        20480  0
uio                    28672  1 uio_pdrv_genirq
sch_fq_codel           20480  5
fuse                  172032  1
nfnetlink              20480  4 nf_tables,ip_set

[2024-05-11 22:02:35,323][INFO] The command is: dmidecode.
[2024-05-11 22:02:35,337][INFO] Execute command dmidecode succeed.
 # dmidecode 3.5
# SMBIOS entry point at 0xbffdc000
Found SMBIOS entry point in EFI, reading table from /dev/mem.
SMBIOS 2.8 present.
18 structures occupying 944 bytes.
Table at 0xBFFDB000.

Handle 0x0000, DMI type 19, 31 bytes
Memory Array Mapped Address
	Starting Address: 0x0000001800000000k
	Ending Address: 0x0000002000000000k
	Range Size: 32 GB
	Physical Array Handle: 0x1008
	Partition Width: 1

Handle 0x0001, DMI type 19, 31 bytes
Memory Array Mapped Address
	Starting Address: 0x0000001000000000k
	Ending Address: 0x0000001800000000k
	Range Size: 32 GB
	Physical Array Handle: 0x1008
	Partition Width: 1

Handle 0x0002, DMI type 19, 31 bytes
Memory Array Mapped Address
	Starting Address: 0x0000000800000000k
	Ending Address: 0x0000001000000000k
	Range Size: 32 GB
	Physical Array Handle: 0x1008
	Partition Width: 1

Handle 0x0003, DMI type 19, 31 bytes
Memory Array Mapped Address
	Starting Address: 0x0000000100000000k
	Ending Address: 0x0000000800000000k
	Range Size: 28 GB
	Physical Array Handle: 0x1008
	Partition Width: 1

Handle 0x0004, DMI type 19, 31 bytes
Memory Array Mapped Address
	Starting Address: 0x0000000002800000k
	Ending Address: 0x00000000C0000000k
	Range Size: 3032 MB
	Physical Array Handle: 0x1008
	Partition Width: 1

Handle 0x0005, DMI type 0, 26 bytes
BIOS Information
	Vendor: EFI Development Kit II / Sophgo
	Version: V1.0
	Release Date: Mar 27 2024
	Address: 0xE8000
	Runtime Size: 96 kB
	ROM Size: 64 kB
	Characteristics:
		PCI is supported
		BIOS is upgradeable
		Boot from CD is supported
		Selectable boot is supported
		ACPI is supported
		USB legacy is supported
		Targeted content distribution is supported
		UEFI is supported

Handle 0x0006, DMI type 1, 27 bytes
System Information
	Manufacturer: SOPHGO
	Product Name: Sophgo SG2042 EVB Board
	Version: None
	Serial Number: Not Set
	UUID: 9987fd42-907e-5446-1d7d-7da0109f60a1
	Wake-up Type: Power Switch
	SKU Number: Not Specified
	Family: Not Specified

Handle 0x1004, DMI type 2, 17 bytes
Base Board Information
	Manufacturer: SOPHGO
	Product Name: Sophgo SG2042 EVB Board
	Version: None
	Serial Number: Not Set
	Asset Tag: Not Specified
	Features:
		Board is a hosting board
	Location In Chassis: Not Set
	Chassis Handle: 0x1005
	Type: Motherboard
	Contained Object Handles: 1
		0x1006

Handle 0x1005, DMI type 3, 24 bytes
Chassis Information
	Manufacturer: SOPHGO
	Type: Unknown
	Lock: Not Present
	Version: None
	Serial Number: Not Set
	Asset Tag: Not Specified
	Boot-up State: Unknown
	Power Supply State: Safe
	Thermal State: Safe
	Security Status: None
	OEM Information: 0x00000000
	Height: 1 U
	Number Of Power Cords: 1
	Contained Elements: 0
	SKU Number: Not Specified

Handle 0x1006, DMI type 4, 50 bytes
Processor Information
	Socket Designation: Socket type unknown
	Type: Central Processor
	Family: RV64
	Manufacturer: SOPHGO
	ID: 00 00 00 00 00 00 00 00
	Version: SG2042
	Voltage: 0.0 V
	External Clock: Unknown
	Max Speed: 2200 MHz
	Current Speed: Unknown
	Status: Populated, Enabled
	Upgrade: Other
	L1 Cache Handle: 0x1000
	L2 Cache Handle: 0x1002
	L3 Cache Handle: 0x1003
	Serial Number: Not Specified
	Asset Tag: Not Specified
	Part Number: Not Set
	Core Count: 64
	Core Enabled: 64
	Thread Count: 64
	Characteristics:
		64-bit capable
		Multi-Core
		Execute Protection
		Enhanced Virtualization
		Power/Performance Control

Handle 0x1000, DMI type 7, 27 bytes
Cache Information
	Socket Designation: L1 Instruction
	Configuration: Enabled, Not Socketed, Level 1
	Operational Mode: Unknown
	Location: Internal
	Installed Size: 48 kB
	Maximum Size: 48 kB
	Supported SRAM Types:
		Unknown
	Installed SRAM Type: Unknown
	Speed: Unknown
	Error Correction Type: Parity
	System Type: Instruction
	Associativity: Other

Handle 0x1001, DMI type 7, 27 bytes
Cache Information
	Socket Designation: L1 Data
	Configuration: Enabled, Not Socketed, Level 1
	Operational Mode: Unknown
	Location: Internal
	Installed Size: 32 kB
	Maximum Size: 32 kB
	Supported SRAM Types:
		Unknown
	Installed SRAM Type: Unknown
	Speed: Unknown
	Error Correction Type: Single-bit ECC
	System Type: Data
	Associativity: 2-way Set-associative

Handle 0x1002, DMI type 7, 27 bytes
Cache Information
	Socket Designation: L2
	Configuration: Enabled, Not Socketed, Level 2
	Operational Mode: Write Back
	Location: Internal
	Installed Size: 512 kB
	Maximum Size: 512 kB
	Supported SRAM Types:
		Unknown
	Installed SRAM Type: Unknown
	Speed: Unknown
	Error Correction Type: Single-bit ECC
	System Type: Unified
	Associativity: 16-way Set-associative

Handle 0x1003, DMI type 7, 27 bytes
Cache Information
	Socket Designation: L3
	Configuration: Enabled, Not Socketed, Level 3
	Operational Mode: Write Back
	Location: Internal
	Installed Size: 1 MB
	Maximum Size: 1 MB
	Supported SRAM Types:
		Unknown
	Installed SRAM Type: Unknown
	Speed: Unknown
	Error Correction Type: Single-bit ECC
	System Type: Unified
	Associativity: 8-way Set-associative

Handle 0x1007, DMI type 16, 23 bytes
Physical Memory Array
	Location: System Board Or Motherboard
	Use: System Memory
	Error Correction Type: None
	Maximum Capacity: 16 GB
	Error Information Handle: Not Provided
	Number Of Devices: 1

Handle 0x1008, DMI type 17, 92 bytes
Memory Device
	Array Handle: 0x1007
	Error Information Handle: Not Provided
	Total Width: 64 bits
	Data Width: 32 bits
	Size: 31704 kB
	Form Factor: Row Of Chips
	Set: None
	Locator: DIMM SLOT
	Bank Locator: BANK 0
	Type: DDR4
	Type Detail: Unbuffered (Unregistered)
	Speed: Unknown
	Manufacturer: Not Specified
	Serial Number: Not Specified
	Asset Tag: Not Specified
	Part Number: Not Specified
	Rank: Unknown
	Configured Memory Speed: Unknown
	Minimum Voltage: Unknown
	Maximum Voltage: Unknown
	Configured Voltage: Unknown
	Memory Technology: DRAM
	Memory Operating Mode Capability: Volatile memory
	Firmware Version: Not Specified
	Module Manufacturer ID: Unknown
	Module Product ID: Unknown
	Memory Subsystem Controller Manufacturer ID: Unknown
	Memory Subsystem Controller Product ID: Unknown
	Non-Volatile Size: None
	Volatile Size: 130008 MB
	Cache Size: None
	Logical Size: None

Handle 0x0007, DMI type 32, 11 bytes
System Boot Information
	Status: No errors detected

Handle 0xFEFF, DMI type 127, 4 bytes
End Of Table


[2024-05-11 22:02:35,338][INFO] Checking installed cert package...
[2024-05-11 22:02:35,339][INFO] The command is: rpm -V --nomtime --nomode --nocontexts oec-hardware.
[2024-05-11 22:02:35,676][INFO] Execute command rpm -V --nomtime --nomode --nocontexts oec-hardware succeed.
 S.5......    /usr/share/oech/lib/config/test_config.yaml

[2024-05-11 22:02:35,677][INFO] Checking kernel...
[2024-05-11 22:02:35,679][INFO] Kernel RPM: kernel-6.6.0-19.0.0.21.mg2403.riscv64
[2024-05-11 22:02:35,680][INFO] OS Version: openEuler 24.03 (LTS)
[2024-05-11 22:02:35,681][INFO] The command is: cat /proc/cmdline.
[2024-05-11 22:02:35,690][INFO] Execute command cat /proc/cmdline succeed.
 BOOT_IMAGE=/vmlinuz-6.6.0-19.0.0.21.mg2403.riscv64 root=UUID=c6a516cc-a7e7-42f2-9110-c668496ab628 selinux=0 console=ttyS0,115200 earlycon

[2024-05-11 22:02:35,699][INFO] The command is: rpm -V --nomtime --nomode --nocontexts kernel-6.6.0-19.0.0.21.mg2403.riscv64.
[2024-05-11 22:02:37,894][ERROR] Execute command rpm -V --nomtime --nomode --nocontexts kernel-6.6.0-19.0.0.21.mg2403.riscv64 failed.
 
[2024-05-11 22:02:37,895][INFO] Checking selinux...
[2024-05-11 22:02:37,896][INFO] The command is: /usr/sbin/sestatus | grep 'SELinux status' | grep -qw 'enabled'.
[2024-05-11 22:02:37,918][ERROR] Execute command /usr/sbin/sestatus | grep 'SELinux status' | grep -qw 'enabled' failed.
 
[2024-05-11 22:02:37,920][INFO] The command is: /usr/sbin/sestatus | grep 'Current mode' | grep -qw 'enforcing'.
[2024-05-11 22:02:37,940][ERROR] Execute command /usr/sbin/sestatus | grep 'Current mode' | grep -qw 'enforcing' failed.
 
[2024-05-11 22:02:37,942][ERROR] SElinux is not enforcing, expect is enforcing.
[2024-05-11 22:02:37,943][INFO] The command is: /usr/sbin/sestatus.
[2024-05-11 22:02:37,951][INFO] Execute command /usr/sbin/sestatus succeed.
 SELinux status:                 disabled
````

usb：PASS

````
[2024-05-11 22:05:44,665][INFO] USB device:
[2024-05-11 22:05:44,667][INFO] The command is: lsusb -t.
[2024-05-11 22:05:44,700][INFO] Execute command lsusb -t succeed.
 /:  Bus 001.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 480M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 002: Dev 004, If 0, Class=Human Interface Device, Driver=usbhid, 12M
        |__ Port 002: Dev 004, If 1, Class=Human Interface Device, Driver=usbhid, 12M
        |__ Port 003: Dev 005, If 0, Class=Human Interface Device, Driver=usbhid, 1.5M
        |__ Port 003: Dev 005, If 1, Class=Human Interface Device, Driver=usbhid, 1.5M
    |__ Port 002: Dev 003, If 0, Class=Hub, Driver=hub/4p, 480M
/:  Bus 002.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 10000M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 5000M
    |__ Port 002: Dev 003, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 003.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/1p, 480M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 480M
/:  Bus 004.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/4p, 5000M

[2024-05-11 22:05:45,529][INFO] USB device plug/unplug test begin...
[2024-05-11 22:05:45,531][INFO] Please plug in a USB device.
[2024-05-11 22:06:10,858][INFO] Found new USB device.
[2024-05-11 22:06:10,859][INFO] USB device:
[2024-05-11 22:06:10,860][INFO] The command is: lsusb -t.
[2024-05-11 22:06:10,895][INFO] Execute command lsusb -t succeed.
 /:  Bus 001.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 480M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 002: Dev 004, If 0, Class=Human Interface Device, Driver=usbhid, 12M
        |__ Port 002: Dev 004, If 1, Class=Human Interface Device, Driver=usbhid, 12M
        |__ Port 003: Dev 005, If 0, Class=Human Interface Device, Driver=usbhid, 1.5M
        |__ Port 003: Dev 005, If 1, Class=Human Interface Device, Driver=usbhid, 1.5M
    |__ Port 002: Dev 003, If 0, Class=Hub, Driver=hub/4p, 480M
/:  Bus 002.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 10000M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 5000M
    |__ Port 002: Dev 003, If 0, Class=Hub, Driver=hub/4p, 5000M
        |__ Port 001: Dev 006, If 0, Class=Mass Storage, Driver=usb-storage, 5000M
/:  Bus 003.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/1p, 480M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 480M
/:  Bus 004.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/4p, 5000M

[2024-05-11 22:06:10,897][INFO] Please unplug the USB device you plugged in just now.
[2024-05-11 22:06:35,064][INFO] USB device unplugged.
[2024-05-11 22:06:35,065][INFO] USB device:
[2024-05-11 22:06:35,066][INFO] The command is: lsusb -t.
[2024-05-11 22:06:35,099][INFO] Execute command lsusb -t succeed.
 /:  Bus 001.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 480M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 480M
        |__ Port 002: Dev 004, If 0, Class=Human Interface Device, Driver=usbhid, 12M
        |__ Port 002: Dev 004, If 1, Class=Human Interface Device, Driver=usbhid, 12M
        |__ Port 003: Dev 005, If 0, Class=Human Interface Device, Driver=usbhid, 1.5M
        |__ Port 003: Dev 005, If 1, Class=Human Interface Device, Driver=usbhid, 1.5M
    |__ Port 002: Dev 003, If 0, Class=Hub, Driver=hub/4p, 480M
/:  Bus 002.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/2p, 10000M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 5000M
    |__ Port 002: Dev 003, If 0, Class=Hub, Driver=hub/4p, 5000M
/:  Bus 003.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/1p, 480M
    |__ Port 001: Dev 002, If 0, Class=Hub, Driver=hub/4p, 480M
/:  Bus 004.Port 001: Dev 001, Class=root_hub, Driver=xhci_hcd/4p, 5000M
````

watchdog：PASS

设备自动重启后，再次执行oech上传日志，在 server 端显示 PASS

客户端显示

````
There are 2 selected test suites: system, watchdog.
Start to run 1/2 test suite: system.
Checking installed cert package...
Checking kernel...
Checking selinux...
SElinux is not enforcing, expect is enforcing.
End to run 1/2 test suite: system.
Start to run 2/2 test suite: watchdog.
Load softdog driver.
Set/Get the watchdog timeout time.
Set/Get watchdog timeout succeed.
System will reboot, are you ready? (y|n) y
Please wait seconds.
````

日志

````
[2024-05-11 23:29:42,784][INFO] The command is: systemctl daemon-reload.
[2024-05-11 23:29:43,682][INFO] Execute command systemctl daemon-reload succeed.

[2024-05-11 23:29:43,683][INFO] The command is: systemctl enable oech.
[2024-05-11 23:29:44,586][INFO] Execute command systemctl enable oech succeed.

[2024-05-11 23:29:44,587][INFO] Load softdog driver.
[2024-05-11 23:29:44,588][INFO] The command is: modprobe softdog.
[2024-05-11 23:29:44,627][INFO] Execute command modprobe softdog succeed.

[2024-05-11 23:29:44,629][INFO] Set/Get the watchdog timeout time.
[2024-05-11 23:29:44,629][INFO] The command is: ./watchdog -g | grep '^Watchdog timeout is *'.
[2024-05-11 23:29:44,645][INFO] Execute command ./watchdog -g | grep '^Watchdog timeout is *' succeed.
Watchdog timeout is 60 seconds.

[2024-05-11 23:29:44,646][INFO] The command is: ./watchdog -s 20.
[2024-05-11 23:29:44,654][INFO] Execute command ./watchdog -s 20 succeed.
Watchdog timeout set to 20 seconds.

[2024-05-11 23:29:44,655][INFO] Set/Get watchdog timeout succeed.
[2024-05-11 23:29:48,742][INFO] Please wait seconds.
[2024-03-27 10:18:16,316][INFO] Recover from watchdog.
````



