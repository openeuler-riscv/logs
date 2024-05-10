oec-hardware测试结果

````
-----------------  Summary -----------------
acpi                                    FAIL
clock                                   FAIL
cpufreq                                 FAIL
disk                                    PASS
dpdk-enP2p197s0                         FAIL
dpdk-enP2p201s0                         FAIL
dpdk-enP1p129s0f0                       FAIL
dpdk-enP1p129s0f1                       FAIL
ethernet-enP2p197s0                     FAIL
ethernet-enP2p201s0                     FAIL
ethernet-enP1p129s0f0                   FAIL
ethernet-enP1p129s0f1                   FAIL
kabi                                    PASS
kabiwhitelist                           PASS
kdump                                   FAIL
memory                                  PASS
nvme-nvme0n1                            FAIL
perf                                    PASS
spdk-nvme0n1                            FAIL
system                                  FAIL
usb                                     PASS
watchdog                                FAIL
````



acpi：FAIL

sg2042是否不支持acpi电源管理？

````
[2024-05-08 16:51:46,715][INFO] The command is: acpidump.
[2024-05-08 16:51:46,726][ERROR] Execute command acpidump failed.
 Cannot open directory - /sys/firmware/acpi/tablesCould not get ACPI tables, AE_NOT_FOUND
[2024-05-08 16:51:46,728][ERROR] Test acpi failed.
Cannot open directory - /sys/firmware/acpi/tablesCould not get ACPI tables, AE_NOT_FOUND
````



clock：FAIL

````
[2024-05-08 17:00:38,284][INFO] The command is: /usr/share/oech/lib/tests/compatible/clock/clock.
[2024-05-08 17:03:38,292][ERROR] Execute command /usr/share/oech/lib/tests/compatible/clock/clock failed.
 
[2024-05-08 17:03:38,293][ERROR] Test clock failed.
````



cpufreq：FAIL

是否 cpu 不支持？

````
[2024-05-08 17:10:04,348][INFO] The command is: cpupower -c 0 frequency-info -p | grep governor | cut -d '"' -f 2.
[2024-05-08 17:10:04,371][INFO] Execute command cpupower -c 0 frequency-info -p | grep governor | cut -d '"' -f 2 succeed.
 
[2024-05-08 17:10:04,373][INFO] Get cpu governor succeed.
[2024-05-08 17:10:04,374][INFO] The command is: lscpu | grep '^CPU(s):' | awk '{print $2}'.
[2024-05-08 17:10:04,405][INFO] Execute command lscpu | grep '^CPU(s):' | awk '{print $2}' succeed.
 64

[2024-05-08 17:10:04,407][INFO] Get the CPU(s) succeed.
[2024-05-08 17:10:04,408][INFO] The command is: cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq.
[2024-05-08 17:10:04,418][ERROR] Execute command cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq failed.
 cat: /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq: No such file or directory
[2024-05-08 17:10:04,419][ERROR] Get the scaling_max_freq of cpu failed.
[2024-05-08 17:10:04,420][ERROR] Fail to get CPU info.
 Please check if the CPU supports cpufreq.
````



disk：PASS

未插入U盘时测试FAIL，插入U盘后测试 PASS

````
There are 2 selected test suites: disk, system.
Start to run 1/2 test suite: disk.
sda raw IO test
Starting sequential raw IO test...
/dev/sda fio succeed.
Starting rand raw IO test...
/dev/sda fio succeed.
sda vfs test
Starting sequential vfs IO test...
/root/vfs_test fio succeed.
Starting rand vfs IO test...
/root/vfs_test fio succeed.
End to run 1/2 test suite: disk.
The disk doesn't have quadruple information, couldn't get hardware.
Start to run 2/2 test suite: system.
Checking installed cert package...
Checking kernel...
Failed to run system. 'openEuler 24.03 (LTS)'
End to run 2/2 test suite: system.
There is no cert device need to export.
-----------------  Summary -----------------
disk                                    PASS
system                                  FAIL
Log saved to file: /usr/share/oech/logs/oech-20240508184413-CSLjoyY8vw.tar succeed.
Do you want to submit last result? (y|n) y
Start to upload result to server 192.168.0.103, please wait.
Upload result to server 192.168.0.103 succeed.
````

下面是测试FAIL的日志

````
[2024-05-08 17:17:51,066][INFO] Disk Info:
[2024-05-08 17:17:51,068][INFO] The command is: fdisk -l.
[2024-05-08 17:17:51,106][INFO] Execute command fdisk -l succeed.
 Disk /dev/nvme0n1: 953.87 GiB, 1024209543168 bytes, 2000409264 sectors
Disk model: FORESEE XP1000F001T                     
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xd7335472

Device         Boot   Start      End  Sectors  Size Id Type
/dev/nvme0n1p1         2048   526335   524288  256M  c W95 FAT32 (LBA)
/dev/nvme0n1p2       526336  1574911  1048576  512M ef EFI (FAT-12/16/32)
/dev/nvme0n1p3      1574912 33554431 31979520 15.2G 83 Linux


Disk /dev/mmcblk1: 59.48 GiB, 63864569856 bytes, 124735488 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x031f9acf

Device         Boot Start    End Sectors  Size Id Type
/dev/mmcblk1p1       2048 524287  522240  255M  c W95 FAT32 (LBA)

[2024-05-08 17:17:51,107][INFO] Partition Info:
[2024-05-08 17:17:51,108][INFO] The command is: df -h.
[2024-05-08 17:17:51,134][INFO] Execute command df -h succeed.
 Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p3   15G  3.3G   11G  23% /
devtmpfs        4.0M     0  4.0M   0% /dev
tmpfs            61G     0   61G   0% /dev/shm
tmpfs           4.0M     0  4.0M   0% /sys/fs/cgroup
efivarfs         28K  2.3K   26K   8% /sys/firmware/efi/efivars
tmpfs            25G  8.8M   25G   1% /run
tmpfs            61G     0   61G   0% /tmp
/dev/nvme0n1p2  511M  369M  142M  73% /boot

[2024-05-08 17:17:51,135][INFO] Mount Info:
[2024-05-08 17:17:51,136][INFO] The command is: mount.
[2024-05-08 17:17:51,149][INFO] Execute command mount succeed.
 /dev/nvme0n1p3 on / type ext4 (rw,noatime)
rpc_pipefs on /var/lib/nfs/rpc_pipefs type rpc_pipefs (rw,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,size=4096k,nr_inodes=15830640,mode=755)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,size=4096k,nr_inodes=1024,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/usr/lib/systemd/systemd-cgroups-agent,name=systemd)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
efivarfs on /sys/firmware/efi/efivars type efivarfs (rw,nosuid,nodev,noexec,relatime)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
configfs on /sys/kernel/config type configfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
tmpfs on /run type tmpfs (rw,nosuid,nodev,size=25362384k,nr_inodes=819200,mode=755)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=30,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=15424)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,nosuid,nodev,relatime,pagesize=2M)
mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)
debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)
tracefs on /sys/kernel/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev,nr_inodes=1048576)
fusectl on /sys/fs/fuse/connections type fusectl (rw,nosuid,nodev,noexec,relatime)
/dev/nvme0n1p2 on /boot type vfat (rw,noatime,fmask=0022,dmask=0022,codepage=437,iocharset=ascii,shortname=mixed,errors=remount-ro,x-systemd.mount-timeout=300s)

[2024-05-08 17:17:51,151][INFO] Swap Info:
[2024-05-08 17:17:51,152][INFO] The command is: cat /proc/swaps.
[2024-05-08 17:17:51,160][INFO] Execute command cat /proc/swaps succeed.
 Filename				Type		Size		Used		Priority

[2024-05-08 17:17:51,162][INFO] LVM Info:
[2024-05-08 17:17:51,162][INFO] The command is: pvdisplay.
[2024-05-08 17:17:51,223][INFO] Execute command pvdisplay succeed.
 
[2024-05-08 17:17:51,224][INFO] The command is: vgdisplay.
[2024-05-08 17:17:51,274][INFO] Execute command vgdisplay succeed.
 
[2024-05-08 17:17:51,275][INFO] The command is: lvdisplay.
[2024-05-08 17:17:51,323][INFO] Execute command lvdisplay succeed.
 
[2024-05-08 17:17:51,324][INFO] Md Info:
[2024-05-08 17:17:51,325][INFO] The command is: cat /proc/mdstat.
[2024-05-08 17:17:51,334][INFO] Execute command cat /proc/mdstat succeed.
 
[2024-05-08 17:17:52,173][INFO] The command is: /usr/sbin/swapon -a.
[2024-05-08 17:17:52,186][INFO] Execute command /usr/sbin/swapon -a succeed.
 
[2024-05-08 17:17:52,190][ERROR] No suite disk found to test.
````



dpdk-enP2p197s0：FAIL

````
[2024-05-08 18:55:30,468][INFO] Driver Name: 
[2024-05-08 18:55:30,470][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 18:55:30,492][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-08 18:55:30,694][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-08 18:55:30,695][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-08 18:55:30,954][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-08 18:55:30,955][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-08 18:55:31,244][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-08 18:55:31,246][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:31,256][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:31,257][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-08 18:55:31,282][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-08 18:55:31,284][INFO] Hugepage successfully configured.
[2024-05-08 18:55:31,286][INFO] Node Pages Size Total
[2024-05-08 18:55:31,287][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:31,297][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:31,298][INFO] 2    1024  2Mb    2Gb
[2024-05-08 18:55:31,299][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:31,309][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:31,310][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:31,319][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:31,321][INFO] 0    1024  2Mb    2Gb
[2024-05-08 18:55:31,322][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:31,331][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:31,333][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:31,342][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:31,343][INFO] 3    1024  2Mb    2Gb
[2024-05-08 18:55:31,345][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:31,354][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:31,355][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:31,364][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:31,366][INFO] 1    1024  2Mb    2Gb
[2024-05-08 18:55:31,367][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:31,376][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:31,378][INFO] The command is: ethtool enP2p197s0 | grep Speed | awk '{print $2}'.
[2024-05-08 18:55:31,404][INFO] Execute command ethtool enP2p197s0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-08 18:55:31,406][INFO] The speed of enP2p197s0 is 100Mb/s.
[2024-05-08 18:55:31,407][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 18:55:31,433][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 18:55:31,435][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 18:55:31,461][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 18:55:31,462][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 18:55:31,489][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 18:55:31,491][ERROR] Test icmp failed.
[2024-05-08 18:55:31,492][INFO] Unbinding server card...
[2024-05-08 18:55:31,596][ERROR] Call remote server url http://192.168.0.103/api/unbind/server failed.
[2024-05-08 18:55:31,598][INFO] Unbinding client card...
[2024-05-08 18:55:31,599][INFO] The command is: dpdk-devbind.py -u 4c00000000.pcie.
[2024-05-08 18:55:32,488][ERROR] Execute command dpdk-devbind.py -u 4c00000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 4c00000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-08 18:55:32,490][INFO] The command is: dpdk-devbind.py -b  4c00000000.pcie.
[2024-05-08 18:55:32,735][ERROR] Execute command dpdk-devbind.py -b  4c00000000.pcie failed.
 Error: No devices specified.
[2024-05-08 18:55:32,737][INFO] Setting client interface enP2p197s0 up...
[2024-05-08 18:55:32,738][INFO] The command is: ip link set up enP2p197s0.
[2024-05-08 18:55:32,750][INFO] Execute command ip link set up enP2p197s0 succeed.
 
[2024-05-08 18:55:32,752][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-08 18:55:32,768][INFO] Execute command ip link show enP2p197s0 | grep 'state UP' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-08 18:55:32,770][INFO] Set interface enP2p197s0 up succeed.
[2024-05-08 18:55:33,158][INFO] Status: 200 OK
[2024-05-08 18:55:33,159][INFO] Stop all test servers.
````



dpdk-enP2p201s0：FAIL

````
[2024-05-08 18:55:33,176][INFO] Driver Name: 
[2024-05-08 18:55:33,177][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 18:55:33,201][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-08 18:55:33,401][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-08 18:55:33,402][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-08 18:55:33,661][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-08 18:55:33,662][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-08 18:55:33,935][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-08 18:55:33,937][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:33,947][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:33,948][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-08 18:55:33,974][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-08 18:55:33,976][INFO] Hugepage successfully configured.
[2024-05-08 18:55:33,977][INFO] Node Pages Size Total
[2024-05-08 18:55:33,979][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:33,989][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:33,990][INFO] 2    1024  2Mb    2Gb
[2024-05-08 18:55:33,991][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:34,000][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:34,002][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:34,011][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:34,012][INFO] 0    1024  2Mb    2Gb
[2024-05-08 18:55:34,013][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:34,022][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:34,024][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:34,033][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:34,034][INFO] 3    1024  2Mb    2Gb
[2024-05-08 18:55:34,035][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:34,045][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:34,047][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:34,056][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:34,057][INFO] 1    1024  2Mb    2Gb
[2024-05-08 18:55:34,058][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:34,067][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:34,068][INFO] The command is: ethtool enP2p201s0 | grep Speed | awk '{print $2}'.
[2024-05-08 18:55:34,093][INFO] Execute command ethtool enP2p201s0 | grep Speed | awk '{print $2}' succeed.
 Unknown!

[2024-05-08 18:55:34,095][ERROR] Failed to run dpdk-enP2p201s0. invalid literal for int() with base 10: 'Unkn'
[2024-05-08 18:55:34,096][INFO] Unbinding server card...
[2024-05-08 18:55:34,204][ERROR] Call remote server url http://192.168.0.103/api/unbind/server failed.
[2024-05-08 18:55:34,205][INFO] Unbinding client card...
[2024-05-08 18:55:34,206][INFO] The command is: dpdk-devbind.py -u 4c00000000.pcie.
[2024-05-08 18:55:35,093][ERROR] Execute command dpdk-devbind.py -u 4c00000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 4c00000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-08 18:55:35,094][INFO] The command is: dpdk-devbind.py -b  4c00000000.pcie.
[2024-05-08 18:55:35,344][ERROR] Execute command dpdk-devbind.py -b  4c00000000.pcie failed.
 Error: No devices specified.
[2024-05-08 18:55:35,345][INFO] Setting client interface enP2p201s0 up...
[2024-05-08 18:55:35,346][INFO] The command is: ip link set up enP2p201s0.
[2024-05-08 18:55:35,358][INFO] Execute command ip link set up enP2p201s0 succeed.
 
[2024-05-08 18:55:35,359][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:35,376][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:36,377][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:36,393][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:37,395][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:37,410][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:38,412][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:38,428][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:39,430][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:39,445][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:40,447][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:40,463][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:41,464][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:41,481][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:42,483][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:42,501][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:43,502][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:43,518][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:44,520][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 18:55:44,537][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:45,539][ERROR] Set interface enP2p201s0 up failed.
[2024-05-08 18:55:45,924][INFO] Status: 200 OK
[2024-05-08 18:55:45,926][INFO] Stop all test servers.
````



dpdk-enP1p129s0f0：FAIL

````
[2024-05-08 18:55:45,942][INFO] Driver Name: 
[2024-05-08 18:55:45,943][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 18:55:45,967][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-08 18:55:46,168][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-08 18:55:46,169][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-08 18:55:46,431][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-08 18:55:46,433][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-08 18:55:46,707][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-08 18:55:46,709][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:46,719][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:46,720][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-08 18:55:46,747][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-08 18:55:46,749][INFO] Hugepage successfully configured.
[2024-05-08 18:55:46,750][INFO] Node Pages Size Total
[2024-05-08 18:55:46,752][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:46,762][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:46,763][INFO] 2    1024  2Mb    2Gb
[2024-05-08 18:55:46,764][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:46,774][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:46,776][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:46,785][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:46,787][INFO] 0    1024  2Mb    2Gb
[2024-05-08 18:55:46,787][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:46,798][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:46,799][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:46,809][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:46,810][INFO] 3    1024  2Mb    2Gb
[2024-05-08 18:55:46,811][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:46,822][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:46,823][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:46,833][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:46,834][INFO] 1    1024  2Mb    2Gb
[2024-05-08 18:55:46,835][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:46,845][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:46,846][INFO] The command is: ethtool enP1p129s0f0 | grep Speed | awk '{print $2}'.
[2024-05-08 18:55:46,872][INFO] Execute command ethtool enP1p129s0f0 | grep Speed | awk '{print $2}' succeed.
 Unknown!

[2024-05-08 18:55:46,874][ERROR] Failed to run dpdk-enP1p129s0f0. invalid literal for int() with base 10: 'Unkn'
[2024-05-08 18:55:46,875][INFO] Unbinding server card...
[2024-05-08 18:55:46,969][ERROR] Call remote server url http://192.168.0.103/api/unbind/server failed.
[2024-05-08 18:55:46,971][INFO] Unbinding client card...
[2024-05-08 18:55:46,972][INFO] The command is: dpdk-devbind.py -u 7062000000.pcie.
[2024-05-08 18:55:47,857][ERROR] Execute command dpdk-devbind.py -u 7062000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 7062000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-08 18:55:47,858][INFO] The command is: dpdk-devbind.py -b  7062000000.pcie.
[2024-05-08 18:55:48,108][ERROR] Execute command dpdk-devbind.py -b  7062000000.pcie failed.
 Error: No devices specified.
[2024-05-08 18:55:48,109][INFO] Setting client interface enP1p129s0f0 up...
[2024-05-08 18:55:48,110][INFO] The command is: ip link set up enP1p129s0f0.
[2024-05-08 18:55:48,123][INFO] Execute command ip link set up enP1p129s0f0 succeed.
 
[2024-05-08 18:55:48,124][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:48,140][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:49,142][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:49,157][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:50,159][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:50,175][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:51,177][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:51,193][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:52,194][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:52,210][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:53,212][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:53,227][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:54,229][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:54,245][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:55,247][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:55,262][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:56,264][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:56,280][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:57,281][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 18:55:57,297][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 
[2024-05-08 18:55:58,299][ERROR] Set interface enP1p129s0f0 up failed.
[2024-05-08 18:55:58,653][INFO] Status: 200 OK
[2024-05-08 18:55:58,655][INFO] Stop all test servers.
````



dpdk-enP1p129s0f1：FAIL

````
[2024-05-08 18:55:58,671][INFO] Driver Name: 
[2024-05-08 18:55:58,673][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 18:55:58,696][INFO] The command is: dpdk-hugepages.py -u.
[2024-05-08 18:55:58,893][INFO] Execute command dpdk-hugepages.py -u succeed.
 
[2024-05-08 18:55:58,894][INFO] The command is: dpdk-hugepages.py -c.
[2024-05-08 18:55:59,151][INFO] Execute command dpdk-hugepages.py -c succeed.
 
[2024-05-08 18:55:59,153][INFO] The command is: dpdk-hugepages.py --setup 2G.
[2024-05-08 18:55:59,425][INFO] Execute command dpdk-hugepages.py --setup 2G succeed.
 
[2024-05-08 18:55:59,427][INFO] The command is: cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:59,438][INFO] Execute command cat /sys/devices/system/node/node0/hugepages//hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:59,439][INFO] The command is: mount | grep hugetlbfs | awk '{print $2}'.
[2024-05-08 18:55:59,465][INFO] Execute command mount | grep hugetlbfs | awk '{print $2}' succeed.
 on

[2024-05-08 18:55:59,466][INFO] Hugepage successfully configured.
[2024-05-08 18:55:59,468][INFO] Node Pages Size Total
[2024-05-08 18:55:59,469][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:59,480][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:59,481][INFO] 2    1024  2Mb    2Gb
[2024-05-08 18:55:59,482][INFO] The command is: cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:59,492][INFO] Execute command cat /sys/devices/system/node/node2/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:59,493][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:59,502][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:59,504][INFO] 0    1024  2Mb    2Gb
[2024-05-08 18:55:59,505][INFO] The command is: cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:59,514][INFO] Execute command cat /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:59,516][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:59,525][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:59,527][INFO] 3    1024  2Mb    2Gb
[2024-05-08 18:55:59,528][INFO] The command is: cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:59,537][INFO] Execute command cat /sys/devices/system/node/node3/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:59,539][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages.
[2024-05-08 18:55:59,548][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-2048kB/nr_hugepages succeed.
 1024

[2024-05-08 18:55:59,550][INFO] 1    1024  2Mb    2Gb
[2024-05-08 18:55:59,551][INFO] The command is: cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages.
[2024-05-08 18:55:59,561][INFO] Execute command cat /sys/devices/system/node/node1/hugepages/hugepages-1048576kB/nr_hugepages succeed.
 0

[2024-05-08 18:55:59,563][INFO] The command is: ethtool enP1p129s0f1 | grep Speed | awk '{print $2}'.
[2024-05-08 18:55:59,587][INFO] Execute command ethtool enP1p129s0f1 | grep Speed | awk '{print $2}' succeed.
 Unknown!

[2024-05-08 18:55:59,589][ERROR] Failed to run dpdk-enP1p129s0f1. invalid literal for int() with base 10: 'Unkn'
[2024-05-08 18:55:59,590][INFO] Unbinding server card...
[2024-05-08 18:55:59,704][ERROR] Call remote server url http://192.168.0.103/api/unbind/server failed.
[2024-05-08 18:55:59,706][INFO] Unbinding client card...
[2024-05-08 18:55:59,707][INFO] The command is: dpdk-devbind.py -u 7062000000.pcie.
[2024-05-08 18:56:00,594][ERROR] Execute command dpdk-devbind.py -u 7062000000.pcie failed.
 Warning: no supported DPDK kernel modules are loadedTraceback (most recent call last):  File "/usr/bin/dpdk-devbind.py", line 798, in <module>    main()  File "/usr/bin/dpdk-devbind.py", line 794, in main    do_arg_actions()  File "/usr/bin/dpdk-devbind.py", line 753, in do_arg_actions    unbind_all(args, force_flag)  File "/usr/bin/dpdk-devbind.py", line 473, in unbind_all    for d in dev_list:  File "/usr/bin/dpdk-devbind.py", line 321, in dev_id_from_dev_name    raise ValueError("Unknown device: %s. "ValueError: Unknown device: 7062000000.pcie. Please specify device in "bus:slot.func" format
[2024-05-08 18:56:00,596][INFO] The command is: dpdk-devbind.py -b  7062000000.pcie.
[2024-05-08 18:56:00,842][ERROR] Execute command dpdk-devbind.py -b  7062000000.pcie failed.
 Error: No devices specified.
[2024-05-08 18:56:00,843][INFO] Setting client interface enP1p129s0f1 up...
[2024-05-08 18:56:00,844][INFO] The command is: ip link set up enP1p129s0f1.
[2024-05-08 18:56:00,856][INFO] Execute command ip link set up enP1p129s0f1 succeed.
 
[2024-05-08 18:56:00,858][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:00,874][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:01,876][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:01,892][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:02,893][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:02,910][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:03,911][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:03,928][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:04,930][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:04,945][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:05,947][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:05,962][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:06,964][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:06,980][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:07,982][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:07,998][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:08,999][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:09,016][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:10,017][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 18:56:10,033][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 
[2024-05-08 18:56:11,035][ERROR] Set interface enP1p129s0f1 up failed.
[2024-05-08 18:56:11,408][INFO] Status: 200 OK
[2024-05-08 18:56:11,410][INFO] Stop all test servers.
````



ethernet-enP2p197s0：FAIL

sg2042是否不支持infiniband？

````
[2024-05-08 16:47:34,394][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-08 16:47:34,410][INFO] Execute command ip link show enP2p197s0 | grep 'state UP' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-08 16:47:34,412][INFO] The command is: ifconfig enP2p197s0 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 16:47:34,437][INFO] Execute command ifconfig enP2p197s0 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.107
fe80::bfb1:ad8e:4440:f624

[2024-05-08 16:47:34,438][INFO] The command is: ifconfig enP2p197s0 | grep '.*ether' | awk '{print $2}'.
[2024-05-08 16:47:34,463][INFO] Execute command ifconfig enP2p197s0 | grep '.*ether' | awk '{print $2}' succeed.
 00:e0:4c:68:00:7b

[2024-05-08 16:47:34,465][INFO] The client IP address already configured.
[2024-05-08 16:47:34,466][INFO] The command is: ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:47:34,577][INFO] Execute command ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-08 16:47:34,590][INFO] Driver Name: 
[2024-05-08 16:47:34,591][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 16:47:34,592][INFO] The command is: ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:06.0/0002:c5:00.0/ | grep -q infiniband.
[2024-05-08 16:47:34,610][ERROR] Execute command ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:06.0/0002:c5:00.0/ | grep -q infiniband failed.
 
[2024-05-08 16:47:34,612][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-08 16:47:34,613][INFO] It will test normal ethernet enP2p197s0.
[2024-05-08 16:47:34,614][INFO] The command is: ethtool enP2p197s0 | grep 'Port' | awk '{print $2}'.
[2024-05-08 16:47:34,638][INFO] Execute command ethtool enP2p197s0 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-08 16:47:34,640][INFO] The enP2p197s0 port type is Twisted, skip checking.
[2024-05-08 16:47:34,641][INFO] The test interface is enP2p197s0.
[2024-05-08 16:47:34,643][INFO] The server ip is 192.168.0.103.
[2024-05-08 16:47:34,643][INFO] The client ip is 192.168.0.107
fe80::bfb1:ad8e:4440:f624
 on enP2p197s0.
[2024-05-08 16:47:34,644][INFO] Setting interface enP2p197s0 down.
[2024-05-08 16:47:34,645][INFO] The command is: ip link set down enP2p197s0.
[2024-05-08 16:47:34,676][INFO] Execute command ip link set down enP2p197s0 succeed.
 
[2024-05-08 16:47:34,677][INFO] The command is: ip link show enP2p197s0 | grep 'state DOWN'.
[2024-05-08 16:47:34,693][INFO] Execute command ip link show enP2p197s0 | grep 'state DOWN' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN mode DEFAULT group default qlen 1000

[2024-05-08 16:47:34,695][INFO] Set interface enP2p197s0 down succeed.
[2024-05-08 16:47:34,696][INFO] Setting interface enP2p197s0 up.
[2024-05-08 16:47:34,697][INFO] The command is: ip link set up enP2p197s0.
[2024-05-08 16:47:34,947][INFO] Execute command ip link set up enP2p197s0 succeed.
 
[2024-05-08 16:47:34,948][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-08 16:47:34,968][ERROR] Execute command ip link show enP2p197s0 | grep 'state UP' failed.
 
[2024-05-08 16:47:35,970][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-08 16:47:35,985][ERROR] Execute command ip link show enP2p197s0 | grep 'state UP' failed.
 
[2024-05-08 16:47:36,987][INFO] The command is: ip link show enP2p197s0 | grep 'state UP'.
[2024-05-08 16:47:37,004][INFO] Execute command ip link show enP2p197s0 | grep 'state UP' succeed.
 2: enP2p197s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-08 16:47:37,006][INFO] Set interface enP2p197s0 up succeed.
[2024-05-08 16:47:37,007][INFO] The command is: ethtool enP2p197s0 | grep Speed | awk '{print $2}'.
[2024-05-08 16:47:37,032][INFO] Execute command ethtool enP2p197s0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-08 16:47:37,034][INFO] The speed of enP2p197s0 is 100Mb/s.
[2024-05-08 16:47:37,035][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:47:37,061][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 16:47:37,063][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:47:37,088][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 16:47:37,090][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:47:37,114][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 16:47:37,116][ERROR] Test icmp failed.
[2024-05-08 16:47:37,117][INFO] Stop all test servers.
[2024-05-08 16:47:37,730][INFO] Status: 200 OK
[2024-05-08 16:47:37,731][INFO] The command is: ifconfig enP2p197s0:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 16:47:37,756][INFO] Execute command ifconfig enP2p197s0:0 | grep '.*inet' | awk '{print $2}' succeed.
````



ethernet-enP2p201s0：FAIL

sg2042是否不支持infiniband？

````
[2024-05-08 16:37:42,397][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 16:37:42,414][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 3: enP2p201s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-08 16:37:42,415][INFO] The command is: ifconfig enP2p201s0 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 16:37:42,442][INFO] Execute command ifconfig enP2p201s0 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.106
fe80::4f77:e42d:1011:65ac

[2024-05-08 16:37:42,444][INFO] The command is: ifconfig enP2p201s0 | grep '.*ether' | awk '{print $2}'.
[2024-05-08 16:37:42,470][INFO] Execute command ifconfig enP2p201s0 | grep '.*ether' | awk '{print $2}' succeed.
 00:e0:4c:68:00:7c

[2024-05-08 16:37:42,472][INFO] The client IP address already configured.
[2024-05-08 16:37:42,474][INFO] The command is: ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:37:42,583][INFO] Execute command ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-08 16:37:42,595][INFO] Driver Name: 
[2024-05-08 16:37:42,597][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 16:37:42,598][INFO] The command is: ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:0e.0/0002:c9:00.0/ | grep -q infiniband.
[2024-05-08 16:37:42,614][ERROR] Execute command ls /sys/devices/platform/4c00000000.pcie/pci0002:c0/0002:c0:00.0/0002:c1:00.0/0002:c2:0e.0/0002:c9:00.0/ | grep -q infiniband failed.
 
[2024-05-08 16:37:42,615][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-08 16:37:42,617][INFO] It will test normal ethernet enP2p201s0.
[2024-05-08 16:37:42,618][INFO] The command is: ethtool enP2p201s0 | grep 'Port' | awk '{print $2}'.
[2024-05-08 16:37:42,646][INFO] Execute command ethtool enP2p201s0 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-08 16:37:42,647][INFO] The enP2p201s0 port type is Twisted, skip checking.
[2024-05-08 16:37:42,648][INFO] The test interface is enP2p201s0.
[2024-05-08 16:37:42,649][INFO] The server ip is 192.168.0.103.
[2024-05-08 16:37:42,650][INFO] The client ip is 192.168.0.106
fe80::4f77:e42d:1011:65ac
 on enP2p201s0.
[2024-05-08 16:37:42,651][INFO] Setting interface enP2p201s0 down.
[2024-05-08 16:37:42,652][INFO] The command is: ip link set down enP2p201s0.
[2024-05-08 16:37:42,684][INFO] Execute command ip link set down enP2p201s0 succeed.
 
[2024-05-08 16:37:42,685][INFO] The command is: ip link show enP2p201s0 | grep 'state DOWN'.
[2024-05-08 16:37:42,704][INFO] Execute command ip link show enP2p201s0 | grep 'state DOWN' succeed.
 3: enP2p201s0: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN mode DEFAULT group default qlen 1000

[2024-05-08 16:37:42,706][INFO] Set interface enP2p201s0 down succeed.
[2024-05-08 16:37:42,707][INFO] Setting interface enP2p201s0 up.
[2024-05-08 16:37:42,708][INFO] The command is: ip link set up enP2p201s0.
[2024-05-08 16:37:42,963][INFO] Execute command ip link set up enP2p201s0 succeed.
 
[2024-05-08 16:37:42,964][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 16:37:42,983][ERROR] Execute command ip link show enP2p201s0 | grep 'state UP' failed.
 
[2024-05-08 16:37:43,985][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 16:37:44,000][ERROR] Execute command ip link show enP2p201s0 | grep 'state UP' failed.
 
[2024-05-08 16:37:45,002][INFO] The command is: ip link show enP2p201s0 | grep 'state UP'.
[2024-05-08 16:37:45,017][INFO] Execute command ip link show enP2p201s0 | grep 'state UP' succeed.
 3: enP2p201s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000

[2024-05-08 16:37:45,018][INFO] Set interface enP2p201s0 up succeed.
[2024-05-08 16:37:45,019][INFO] The command is: ethtool enP2p201s0 | grep Speed | awk '{print $2}'.
[2024-05-08 16:37:45,045][INFO] Execute command ethtool enP2p201s0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-08 16:37:45,047][INFO] The speed of enP2p201s0 is 100Mb/s.
[2024-05-08 16:37:45,048][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:37:45,073][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 16:37:45,075][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:37:45,100][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 16:37:45,102][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 16:37:45,127][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 16:37:45,128][ERROR] Test icmp failed.
[2024-05-08 16:37:45,130][INFO] Stop all test servers.
[2024-05-08 16:37:45,626][INFO] Status: 200 OK
[2024-05-08 16:37:45,628][INFO] The command is: ifconfig enP2p201s0:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 16:37:45,652][INFO] Execute command ifconfig enP2p201s0:0 | grep '.*inet' | awk '{print $2}' succeed.
````



ethernet-enP1p129s0f0：FAIL

sg2042是否不支持infiniband？

````
[2024-05-08 15:13:58,246][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 15:13:58,262][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 4: enP1p129s0f0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-08 15:13:58,263][INFO] The command is: ifconfig enP1p129s0f0 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 15:13:58,288][INFO] Execute command ifconfig enP1p129s0f0 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.105
fe80::ba88:9bc4:3770:e63b

[2024-05-08 15:13:58,290][INFO] The command is: ifconfig enP1p129s0f0 | grep '.*ether' | awk '{print $2}'.
[2024-05-08 15:13:58,315][INFO] Execute command ifconfig enP1p129s0f0 | grep '.*ether' | awk '{print $2}' succeed.
 a0:36:9f:54:0c:c8

[2024-05-08 15:13:58,316][INFO] The client IP address already configured.
[2024-05-08 15:13:58,318][INFO] The command is: ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 15:13:58,428][INFO] Execute command ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-08 15:13:58,441][INFO] Driver Name: 
[2024-05-08 15:13:58,442][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 15:13:58,443][INFO] The command is: ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.0/ | grep -q infiniband.
[2024-05-08 15:13:58,459][ERROR] Execute command ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.0/ | grep -q infiniband failed.
 
[2024-05-08 15:13:58,461][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-08 15:13:58,462][INFO] It will test normal ethernet enP1p129s0f0.
[2024-05-08 15:13:58,463][INFO] The command is: ethtool enP1p129s0f0 | grep 'Port' | awk '{print $2}'.
[2024-05-08 15:13:58,488][INFO] Execute command ethtool enP1p129s0f0 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-08 15:13:58,490][INFO] The enP1p129s0f0 port type is Twisted, skip checking.
[2024-05-08 15:13:58,491][INFO] The test interface is enP1p129s0f0.
[2024-05-08 15:13:58,492][INFO] The server ip is 192.168.0.103.
[2024-05-08 15:13:58,493][INFO] The client ip is 192.168.0.105
fe80::ba88:9bc4:3770:e63b
 on enP1p129s0f0.
[2024-05-08 15:13:58,494][INFO] Setting interface enP1p129s0f0 down.
[2024-05-08 15:13:58,495][INFO] The command is: ip link set down enP1p129s0f0.
[2024-05-08 15:13:58,855][INFO] Execute command ip link set down enP1p129s0f0 succeed.
 
[2024-05-08 15:13:58,857][INFO] The command is: ip link show enP1p129s0f0 | grep 'state DOWN'.
[2024-05-08 15:13:58,874][INFO] Execute command ip link show enP1p129s0f0 | grep 'state DOWN' succeed.
 4: enP1p129s0f0: <BROADCAST,MULTICAST> mtu 1500 qdisc mq state DOWN mode DEFAULT group default qlen 1000

[2024-05-08 15:13:58,875][INFO] Set interface enP1p129s0f0 down succeed.
[2024-05-08 15:13:58,876][INFO] Setting interface enP1p129s0f0 up.
[2024-05-08 15:13:58,877][INFO] The command is: ip link set up enP1p129s0f0.
[2024-05-08 15:13:59,043][INFO] Execute command ip link set up enP1p129s0f0 succeed.
 
[2024-05-08 15:13:59,045][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 15:13:59,060][ERROR] Execute command ip link show enP1p129s0f0 | grep 'state UP' failed.
 
[2024-05-08 15:14:00,062][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 15:14:00,077][ERROR] Execute command ip link show enP1p129s0f0 | grep 'state UP' failed.
 
[2024-05-08 15:14:01,079][INFO] The command is: ip link show enP1p129s0f0 | grep 'state UP'.
[2024-05-08 15:14:01,094][INFO] Execute command ip link show enP1p129s0f0 | grep 'state UP' succeed.
 4: enP1p129s0f0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-08 15:14:01,096][INFO] Set interface enP1p129s0f0 up succeed.
[2024-05-08 15:14:01,097][INFO] The command is: ethtool enP1p129s0f0 | grep Speed | awk '{print $2}'.
[2024-05-08 15:14:01,122][INFO] Execute command ethtool enP1p129s0f0 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-08 15:14:01,124][INFO] The speed of enP1p129s0f0 is 100Mb/s.
[2024-05-08 15:14:01,125][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 15:14:01,150][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 15:14:01,152][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 15:14:01,178][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 15:14:01,180][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 15:14:01,206][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 15:14:01,208][ERROR] Test icmp failed.
[2024-05-08 15:14:01,209][INFO] Stop all test servers.
[2024-05-08 15:14:02,907][INFO] Status: 200 OK
[2024-05-08 15:14:02,909][INFO] The command is: ifconfig enP1p129s0f0:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 15:14:02,933][INFO] Execute command ifconfig enP1p129s0f0:0 | grep '.*inet' | awk '{print $2}' succeed.
````



ethernet-enP1p129s0f1：FAIL

sg2042是否不支持infiniband？

````
[2024-05-08 13:39:55,113][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 13:39:55,128][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 5: enP1p129s0f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-08 13:39:55,129][INFO] The command is: ifconfig enP1p129s0f1 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 13:39:55,154][INFO] Execute command ifconfig enP1p129s0f1 | grep '.*inet' | awk '{print $2}' succeed.
 192.168.0.107
fe80::160:ccaf:37d1:4b11

[2024-05-08 13:39:55,156][INFO] The command is: ifconfig enP1p129s0f1 | grep '.*ether' | awk '{print $2}'.
[2024-05-08 13:39:55,180][INFO] Execute command ifconfig enP1p129s0f1 | grep '.*ether' | awk '{print $2}' succeed.
 a0:36:9f:54:0c:ca

[2024-05-08 13:39:55,182][INFO] The client IP address already configured.
[2024-05-08 13:39:55,183][INFO] The command is: ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 13:39:55,207][INFO] Execute command ping -q -c 1 -W 1 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 0%

[2024-05-08 13:39:55,221][INFO] Driver Name: 
[2024-05-08 13:39:55,222][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 13:39:55,223][INFO] The command is: ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.1/ | grep -q infiniband.
[2024-05-08 13:39:55,240][ERROR] Execute command ls /sys/devices/platform/7062000000.pcie/pci0001:80/0001:80:00.0/0001:81:00.1/ | grep -q infiniband failed.
 
[2024-05-08 13:39:55,241][INFO] Current ethernet doesn't support RoCE, no need test Roce.
[2024-05-08 13:39:55,242][INFO] It will test normal ethernet enP1p129s0f1.
[2024-05-08 13:39:55,243][INFO] The command is: ethtool enP1p129s0f1 | grep 'Port' | awk '{print $2}'.
[2024-05-08 13:39:55,267][INFO] Execute command ethtool enP1p129s0f1 | grep 'Port' | awk '{print $2}' succeed.
 Twisted

[2024-05-08 13:39:55,269][INFO] The enP1p129s0f1 port type is Twisted, skip checking.
[2024-05-08 13:39:55,270][INFO] The test interface is enP1p129s0f1.
[2024-05-08 13:39:55,271][INFO] The server ip is 192.168.0.103.
[2024-05-08 13:39:55,272][INFO] The client ip is 192.168.0.107
fe80::160:ccaf:37d1:4b11
 on enP1p129s0f1.
[2024-05-08 13:39:55,273][INFO] Setting interface enP1p129s0f1 down.
[2024-05-08 13:39:55,274][INFO] The command is: ip link set down enP1p129s0f1.
[2024-05-08 13:39:55,636][INFO] Execute command ip link set down enP1p129s0f1 succeed.
 
[2024-05-08 13:39:55,637][INFO] The command is: ip link show enP1p129s0f1 | grep 'state DOWN'.
[2024-05-08 13:39:55,652][INFO] Execute command ip link show enP1p129s0f1 | grep 'state DOWN' succeed.
 5: enP1p129s0f1: <BROADCAST,MULTICAST> mtu 1500 qdisc mq state DOWN mode DEFAULT group default qlen 1000

[2024-05-08 13:39:55,653][INFO] Set interface enP1p129s0f1 down succeed.
[2024-05-08 13:39:55,654][INFO] Setting interface enP1p129s0f1 up.
[2024-05-08 13:39:55,655][INFO] The command is: ip link set up enP1p129s0f1.
[2024-05-08 13:39:55,820][INFO] Execute command ip link set up enP1p129s0f1 succeed.
 
[2024-05-08 13:39:55,821][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 13:39:55,836][ERROR] Execute command ip link show enP1p129s0f1 | grep 'state UP' failed.
 
[2024-05-08 13:39:56,838][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 13:39:56,853][ERROR] Execute command ip link show enP1p129s0f1 | grep 'state UP' failed.
 
[2024-05-08 13:39:57,855][INFO] The command is: ip link show enP1p129s0f1 | grep 'state UP'.
[2024-05-08 13:39:57,871][INFO] Execute command ip link show enP1p129s0f1 | grep 'state UP' succeed.
 5: enP1p129s0f1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000

[2024-05-08 13:39:57,872][INFO] Set interface enP1p129s0f1 up succeed.
[2024-05-08 13:39:57,873][INFO] The command is: ethtool enP1p129s0f1 | grep Speed | awk '{print $2}'.
[2024-05-08 13:39:57,897][INFO] Execute command ethtool enP1p129s0f1 | grep Speed | awk '{print $2}' succeed.
 100Mb/s

[2024-05-08 13:39:57,899][INFO] The speed of enP1p129s0f1 is 100Mb/s.
[2024-05-08 13:39:57,900][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 13:39:57,925][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 13:39:57,927][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 13:39:57,952][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 13:39:57,954][INFO] The command is: ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}'.
[2024-05-08 13:39:57,979][INFO] Execute command ping -q -c 500 -i 0 192.168.0.103 | grep 'packet loss' | awk '{print $6}' succeed.
 
[2024-05-08 13:39:57,980][ERROR] Test icmp failed.
[2024-05-08 13:39:57,981][INFO] Stop all test servers.
[2024-05-08 13:39:58,543][INFO] Status: 200 OK
[2024-05-08 13:39:58,544][INFO] The command is: ifconfig enP1p129s0f1:0 | grep '.*inet' | awk '{print $2}'.
[2024-05-08 13:39:58,568][INFO] Execute command ifconfig enP1p129s0f1:0 | grep '.*inet' | awk '{print $2}' succeed.
````



kabi：PASS

````
There are 2 selected test suites: kabi, system.
Start to install required packages: rpm-build
Start to run 1/2 test suite: kabi.
 riscv64 architecture does not support kabi testing.
End to run 1/2 test suite: kabi.
Start to run 2/2 test suite: system.
Checking installed cert package...
Checking kernel...
Failed to run system. 'openEuler 24.03 (LTS)'
End to run 2/2 test suite: system.
There is no cert device need to export.
-----------------  Summary -----------------
kabi                                    PASS
system                                  FAIL
Log saved to file: /usr/share/oech/logs/oech-20240508190650-aiTd4loBXz.tar succeed.
Do you want to submit last result? (y|n) y
Start to upload result to server 192.168.0.103, please wait.
Upload result to server 192.168.0.103 succeed.
````



kabiwhitelist：PASS

````
There are 2 selected test suites: kabiwhitelist, system.
Start to run 1/2 test suite: kabiwhitelist.
Ko or rpm check complete
Clearing temporary files is complete
End to run 1/2 test suite: kabiwhitelist.
Start to run 2/2 test suite: system.
Checking installed cert package...
Checking kernel...
Failed to run system. 'openEuler 24.03 (LTS)'
End to run 2/2 test suite: system.
There is no cert device need to export.
-----------------  Summary -----------------
kabiwhitelist                           PASS
system                                  FAIL
Log saved to file: /usr/share/oech/logs/oech-20240508190847-lUkdONohCm.tar succeed.
Do you want to submit last result? (y|n) y
Start to upload result to server 192.168.0.103, please wait.
Upload result to server 192.168.0.103 succeed.
````



kdump：FAIL

缺少 kexec-tools

````
[2024-05-07 21:49:23,208][INFO] Start to install required packages: crash, kexec-tools
[2024-05-07 21:49:23,210][INFO] The command is: yum install -y crash kexec-tools.
[2024-05-07 21:49:27,044][ERROR] Execute command yum install -y crash kexec-tools failed.
Error: Unable to find a match: kexec-tools
[2024-05-07 21:49:27,046][ERROR] Fail to install required packages.
Error: Unable to find a match: kexec-tools
[2024-05-07 21:49:27,047][ERROR] Required rpm package not installed, test stopped.
````



memory：PASS

````
There are 2 selected test suites: memory, system.
Start to install required packages: memtester, libhugetlbfs-utils
Start to run 1/2 test suite: memory.
Get memory information succeed.
Start to memtester, please wait seconds.
The command is: memtester 4096M 1.
Execute command memtester 4096M 1 succeed.
 memtester version 4.6.0 (64-bit)
Copyright (C) 2001-2020 Charles Cazabon.
Licensed under the GNU General Public License version 2 (only).

pagesize is 4096
pagesizemask is 0xfffffffffffff000
want 4096MB (4294967296 bytes)
got  4096MB (4294967296 bytes), trying mlock ...locked.
Loop 1/1:
  Stuck Address       : ok         
  Random Value        : ok
  Compare XOR         : ok
  Compare SUB         : ok
  Compare MUL         : ok
  Compare DIV         : ok
  Compare OR          : ok
  Compare AND         : ok
  Sequential Increment: ok
  Solid Bits          : ok         
  Block Sequential    : ok         
  Checkerboard        : ok         
  Bit Spread          : ok         
  Bit Flip            : ok         
  Walking Ones        : ok         
  Walking Zeroes      : ok         
  8-bit Writes        : ok
  16-bit Writes       : ok

Done.

Memtester test succeed.
Start to test eat memory.
System Memory: 123839 MB
Free Memory: 113884 MB
Swap Memory: 8191 MB

set the system not to restart.
Eat memory test succeed.
Start to test hugetlb.
Get memory information succeed.
HugePages Total: 4096
HugePages Free: 4096
HugePages Size: 2MB
Get memory information succeed.
Hugepages test succeed.
End to run 1/2 test suite: memory.
Start to run 2/2 test suite: system.
Checking installed cert package...
Checking kernel...
Failed to run system. 'openEuler 24.03 (LTS)'
End to run 2/2 test suite: system.
There is no cert device need to export.
-----------------  Summary -----------------
memory                                  PASS
system                                  FAIL
Log saved to file: /usr/share/oech/logs/oech-20240508214121-FvuNdJZylU.tar succeed.
Do you want to submit last result? (y|n) y
Start to upload result to server 192.168.0.103, please wait.
Upload result to server 192.168.0.103 succeed.
````



nvme-nvme0n1：FAIL

测试的是nvme0n1，因为nvme0n1正在使用，该测试skip

````
[2024-05-08 19:11:25,038][INFO] Driver Name: 
[2024-05-08 19:11:25,040][INFO] The driver version information cannot be obtained. Please view it manually.
[2024-05-08 19:11:25,041][INFO] The command is: nvme list.
[2024-05-08 19:11:25,087][INFO] Execute command nvme list succeed.
 Node                  Generic               SN                   Model                                    Namespace  Usage                      Format           FW Rev  
--------------------- --------------------- -------------------- ---------------------------------------- ---------- -------------------------- ---------------- --------
/dev/nvme0n1          /dev/ng0n1            NEV4642004130        FORESEE XP1000F001T                      0x1          1.02  TB /   1.02  TB    512   B +  0 B   V1.28   

[2024-05-08 19:11:25,089][INFO] The command is: /usr/sbin/swapon -a.
[2024-05-08 19:11:25,099][INFO] Execute command /usr/sbin/swapon -a succeed.
 
[2024-05-08 19:11:25,101][ERROR] nvme0n1 is in use now, skip this test.
````



perf：PASS

````
There are 2 selected test suites: perf, system.
Start to install required packages: perf
Start to run 1/2 test suite: perf.
Collecting the perf record.
Record events succeed.
Hardware event found.
Samples found for the hardware event.
End to run 1/2 test suite: perf.
Start to run 2/2 test suite: system.
Checking installed cert package...
Checking kernel...
Failed to run system. 'openEuler 24.03 (LTS)'
End to run 2/2 test suite: system.
There is no cert device need to export.
-----------------  Summary -----------------
perf                                    PASS
system                                  FAIL
Log saved to file: /usr/share/oech/logs/oech-20240508191556-5ZqyiQSc2u.tar succeed.
Do you want to submit last result? (y|n) y
Start to upload result to server 192.168.0.103, please wait.
Upload result to server 192.168.0.103 succeed.
````



spdk-nvme0n1：FAIL

spdk工具问题？

````
[2024-05-08 19:18:05,339][ERROR] The spdk version is too low and needs to be upgraded to 21.01.1-5.
[2024-05-08 19:18:05,341][ERROR] Unload uio_pci_generic driver failed.
````



system：FAIL

````
[2024-05-08 19:22:02,262][INFO] The command is: uname -a.
[2024-05-08 19:22:02,271][INFO] Execute command uname -a succeed.
 Linux openeuler-riscv64 6.6.0-19.0.0.21.oe2403.riscv64 #1 SMP Sat Apr 20 04:42:31 UTC 2024 riscv64 riscv64 riscv64 GNU/Linux

[2024-05-08 19:22:02,272][INFO] The command is: lsmod.
[2024-05-08 19:22:02,293][INFO] Execute command lsmod succeed.
 Module                  Size  Used by
sg                    344064  0
nft_fib_inet           16384  1
nft_fib_ipv4           32768  1 nft_fib_inet
nft_fib_ipv6           32768  1 nft_fib_inet
nft_fib                24576  3 nft_fib_ipv6,nft_fib_ipv4,nft_fib_inet
nft_reject_inet        16384  6
nf_reject_ipv4         49152  1 nft_reject_inet
nf_reject_ipv6         65536  1 nft_reject_inet
nft_reject             20480  1 nft_reject_inet
nft_ct                122880  11
nft_chain_nat          16384  3
nf_tables            2822144  206 nft_ct,nft_reject_inet,nft_fib_ipv6,nft_fib_ipv4,nft_chain_nat,nft_reject,nft_fib,nft_fib_inet
ebtable_nat            16384  0
ebtable_broute         16384  0
ip6table_nat           24576  0
ip6table_mangle        20480  0
ip6table_raw           16384  0
ip6table_security      16384  0
iptable_nat            24576  0
nf_nat                282624  3 ip6table_nat,nft_chain_nat,iptable_nat
nf_conntrack         1351680  2 nf_nat,nft_ct
nf_defrag_ipv6        122880  1 nf_conntrack
nf_defrag_ipv4         24576  1 nf_conntrack
libcrc32c              16384  3 nf_conntrack,nf_nat,nf_tables
iptable_mangle         16384  0
iptable_raw            16384  0
iptable_security       16384  0
rfkill                196608  0
ip_set                364544  0
ebtable_filter         16384  0
ebtables              299008  3 ebtable_nat,ebtable_filter,ebtable_broute
ip6table_filter        16384  0
ip6_tables            172032  5 ip6table_filter,ip6table_raw,ip6table_nat,ip6table_mangle,ip6table_security
iptable_filter         16384  0
ip_tables             167936  5 iptable_filter,iptable_security,iptable_raw,iptable_nat,iptable_mangle
snd_hda_intel         233472  0
snd_intel_dspcfg       16384  1 snd_hda_intel
snd_hda_codec         811008  1 snd_hda_intel
snd_hda_core          634880  2 snd_hda_intel,snd_hda_codec
snd_pcm               962560  3 snd_hda_intel,snd_hda_codec,snd_hda_core
snd_timer             364544  1 snd_pcm
snd                   712704  4 snd_hda_intel,snd_hda_codec,snd_timer,snd_pcm
soundcore              12288  1 snd
uio_pdrv_genirq        36864  0
uio                    98304  1 uio_pdrv_genirq
sch_fq_codel          143360  5
fuse                 1593344  1
nfnetlink             122880  4 nf_tables,ip_set
amdgpu              36560896  0
amdxcp                 16384  1 amdgpu
drm_exec               40960  1 amdgpu
gpu_sched             376832  1 amdgpu
drm_buddy             126976  1 amdgpu
radeon              15900672  2
ixgbe                3452928  0
drm_suballoc_helper    77824  2 amdgpu,radeon
drm_display_helper    909312  2 amdgpu,radeon
drm_ttm_helper         20480  2 amdgpu,radeon
xfrm_algo              36864  1 ixgbe
ttm                   610304  3 amdgpu,radeon,drm_ttm_helper
mdio                   45056  1 ixgbe
dm_mirror             167936  0
dm_region_hash        143360  1 dm_mirror
dm_log                 94208  2 dm_region_hash,dm_mirror
dm_mod               1310720  2 dm_log,dm_mirror

[2024-05-08 19:22:02,295][INFO] The command is: dmidecode.
[2024-05-08 19:22:02,304][INFO] Execute command dmidecode succeed.
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
	Release Date: Mar 28 2024
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


[2024-05-08 19:22:02,305][INFO] Checking installed cert package...
[2024-05-08 19:22:02,306][INFO] The command is: rpm -V --nomtime --nomode --nocontexts oec-hardware.
[2024-05-08 19:22:02,540][INFO] Execute command rpm -V --nomtime --nomode --nocontexts oec-hardware succeed.
 S.5......    /usr/share/oech/lib/config/test_config.yaml

[2024-05-08 19:22:02,541][INFO] Checking kernel...
[2024-05-08 19:22:02,542][INFO] Kernel RPM: kernel-6.6.0-19.0.0.21.oe2403.riscv64
[2024-05-08 19:22:02,543][INFO] OS Version: openEuler 24.03 (LTS)
[2024-05-08 19:22:02,544][INFO] The command is: cat /proc/cmdline.
[2024-05-08 19:22:02,553][INFO] Execute command cat /proc/cmdline succeed.
 BOOT_IMAGE=/vmlinuz-6.6.0-19.0.0.21.oe2403.riscv64 rootwait root=/dev/nvme0n1p3 console=ttyS0,115200 selinux=0 earlycon nvme.use_threaded_interrupts=1 nvme_core.io_timeout=3000

[2024-05-08 19:22:02,555][ERROR] Failed to run system. 'openEuler 24.03 (LTS)'
````



usb：PASS

````
There are 2 selected test suites: system, usb.
Start to run 1/2 test suite: usb.
USB device:
USB device plug/unplug test begin...
Please plug in a USB device.
Done well? (y|n) y
Found new USB device.
USB device:
Please unplug the USB device you plugged in just now.
Done well? (y|n) y
USB device unplugged.
USB device:
All usb sockets have been tested? (y|n) y
End to run 1/2 test suite: usb.
The usb doesn't have quadruple information, couldn't get hardware.
Start to run 2/2 test suite: system.
Checking installed cert package...
Checking kernel...
Failed to run system. 'openEuler 24.03 (LTS)'
End to run 2/2 test suite: system.
There is no cert device need to export.
-----------------  Summary -----------------
system                                  FAIL
usb                                     PASS
Log saved to file: /usr/share/oech/logs/oech-20240508192707-D0LWvFMeZw.tar succeed.
Do you want to submit last result? (y|n) y
Start to upload result to server 192.168.0.103, please wait.
Upload result to server 192.168.0.103 succeed.
````



watchdog：FAIL

设备自动重启后，oech没有后续输出,也没有上传日志

客户端显示

````
There are 2 selected test suites: system, watchdog.
Start to run 1/2 test suite: system.
Checking installed cert package...
Checking kernel...
Failed to run system. 'openEuler 24.03 (LTS)'
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
[2024-05-07 22:04:13,250][INFO] The command is: systemctl daemon-reload.
[2024-05-07 22:04:14,266][INFO] Execute command systemctl daemon-reload succeed.
 
[2024-05-07 22:04:14,267][INFO] The command is: systemctl enable oech.
[2024-05-07 22:04:15,277][INFO] Execute command systemctl enable oech succeed.
 
[2024-05-07 22:04:15,278][INFO] Load softdog driver.
[2024-05-07 22:04:15,280][INFO] The command is: modprobe softdog.
[2024-05-07 22:04:15,323][INFO] Execute command modprobe softdog succeed.
 
[2024-05-07 22:04:15,324][INFO] Set/Get the watchdog timeout time.
[2024-05-07 22:04:15,325][INFO] The command is: ./watchdog -g | grep '^Watchdog timeout is *'.
[2024-05-07 22:04:15,340][INFO] Execute command ./watchdog -g | grep '^Watchdog timeout is *' succeed.
 Watchdog timeout is 60 seconds.

[2024-05-07 22:04:15,342][INFO] The command is: ./watchdog -s 20.
[2024-05-07 22:04:15,349][INFO] Execute command ./watchdog -s 20 succeed.
 Watchdog timeout set to 20 seconds.

[2024-05-07 22:04:15,350][INFO] Set/Get watchdog timeout succeed.
[2024-05-07 22:05:22,989][INFO] Please wait seconds.
````



