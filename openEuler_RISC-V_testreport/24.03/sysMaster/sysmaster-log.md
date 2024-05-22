## sysmaster 测试 log

### service功能测试（测试当前支持的服务）

1. 检查列表中的服务状态，有预期结果1（服务列表：NetworkManager.service dbus.service dbus.socket fstab.service getty@.service hostname-setup.service lvm-activate-openeuler.service sshd-keygen.target sshd-keygen@ecdsa.service sshd-keygen@ed25519.service sshd-keygen@rsa.service sshd.service udev-trigger.service udevd-control.socket udevd-kernel.socket udevd.service）

```bash
[root@openeuler-riscv64 ~]# sctl status NetworkManager.service dbus.service dbus.socket fstab.service getty@.service hostname-setup.service lvm-activate-openeuler.service sshd-keygen.target sshd-keygen@ecdsa.service sshd-keygen@ed25519.service sshd-keygen@rsa.service sshd.service udev-trigger.service udevd-control.socket udevd-kernel.socket udevd.service
● NetworkManager.service - Network Manager Service
 Loaded: true                                     
 Active: active (running)                         
 CGroup: NetworkManager.service                   
    PID: 772 /usr/sbin/NetworkManager --no-daemon
● dbus.service - D-Bus Service
 Loaded: true                                                                                      
 Active: active (running)                                                                          
 CGroup: dbus.service                                                                              
    PID: 769 /usr/bin/dbus-daemon --system --nofork --nopidfile --systemd-activation --syslog-only
● dbus.socket - D-Bus Socket
 Loaded: true               
 Active: active (listening) 
 CGroup: Empty cgroup path  
    PID: No process
● fstab.service - automount fstab device
 Loaded: true            
 Active: inactive (dead) 
 CGroup: fstab.service   
    PID: No process
Failed to show the status of getty@.service: NotExisted
● hostname-setup.service - hostname setup
 Loaded: true                   
 Active: active (exited)        
 CGroup: hostname-setup.service 
    PID: No process
Failed to show the status of lvm-activate-openeuler.service: NotExisted
● sshd-keygen.target
 Loaded: true              
 Active: active (active)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd-keygen@ecdsa.service - OpenSSH ecdsa Server Key Generation
 Loaded: true              
 Active: inactive (dead)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd-keygen@ed25519.service - OpenSSH ed25519 Server Key Generation
 Loaded: true              
 Active: inactive (dead)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd-keygen@rsa.service - OpenSSH rsa Server Key Generation
 Loaded: true              
 Active: inactive (dead)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd.service - OpenSSH server daemon
 Loaded: true                                             
 Active: active (running)                                 
 CGroup: sshd.service                                     
   Docs: man:sshd(8) man:sshd_config(5)                   
    PID: 744 sshd: /usr/sbin/sshd -D [listener] 0 of 10-1
● udev-trigger.service
 Loaded: true                 
 Active: active (exited)      
 CGroup: udev-trigger.service 
    PID: No process
● udevd-control.socket
 Loaded: true               
 Active: active (listening) 
 CGroup: Empty cgroup path  
    PID: No process
● udevd-kernel.socket
 Loaded: true              
 Active: active (running)  
 CGroup: Empty cgroup path 
    PID: No process
● udevd.service
 Loaded: true                               
 Active: active (running)                   
 CGroup: udevd.service                      
    PID: 708 /usr/lib/systemd/systemd-udevd
```

2. 检查以下服务功能，有预期结果2
- 1）执行命令hostname，执行命令cat /etc/hostname

```bash
[root@openeuler-riscv64 ~]# hostname
openeuler-riscv64
[root@openeuler-riscv64 ~]# cat /etc/hostname
openeuler-riscv64
```

- 2）执行busctl命令

```bash
[root@openeuler-riscv64 ~]# busctl
NAME                           PID PROCESS USER CONNECTION    UNIT SESSION DESCRIPTION
:1.0                             - -       -    -             -    -       -          
:1.1                             - -       -    -             -    -       -          
:1.2                             - -       -    -             -    -       -          
com.redhat.ifcfgrh1              - -       -    -             -    -       -          
fi.w1.wpa_supplicant1            - -       -    (activatable) -    -       -          
org.freedesktop.DBus             - -       -    -             -    -       -          
org.freedesktop.NetworkManager   - -       -    -             -    -       -          
org.freedesktop.PolicyKit1       - -       -    (activatable) -    -       -          
org.freedesktop.hostname1        - -       -    (activatable) -    -       -          
org.freedesktop.locale1          - -       -    (activatable) -    -       -          
org.freedesktop.login1           - -       -    (activatable) -    -       -          
org.freedesktop.nm_dispatcher    - -       -    (activatable) -    -       -          
org.freedesktop.nm_priv_helper   - -       -    (activatable) -    -       -          
org.freedesktop.realmd           - -       -    (activatable) -    -       -          
org.freedesktop.timedate1        - -       -    (activatable) -    -       -          
[root@openeuler-riscv64 ~]#
```

- 3）执行命令cat /etc/fstab；执行命令lsblk

```bash
[root@openeuler-riscv64 ~]# cat /etc/fstab
# <device>                                <dir> <type> <options> <dump> <fsck>
UUID=4504cf4d-8d64-448b-b3cd-acf0299d3cd1   /   ext4    rw,noatime  0   1
UUID=d4ef4ee6-b7f0-48b3-a60f-b97734d70a56   /boot   ext2    rw,noatime  0   2
[root@openeuler-riscv64 ~]# lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
vda    253:0    0   20G  0 disk 
├─vda1 253:1    0  512M  0 part /boot
└─vda2 253:2    0 19.5G  0 part /
[root@openeuler-riscv64 ~]# 
```

- 4）串口登录环境
- 5）执行命令udevadm trigger

```bash
[root@openeuler-riscv64 ~]# udevadm trigger
[root@openeuler-riscv64 ~]# 
```

3. sctl restart 重启列表中服务，有预期结果1

```bash
[root@openeuler-riscv64 ~]# sctl restart NetworkManager.service dbus.service dbus.socket fstab.service getty@.service hostname-setup.service lvm-activate-openeuler.service sshd-keygen.target sshd-keygen@ecdsa.service sshd-keygen@ed25519.service sshd-keygen@rsa.service sshd.service udev-trigger.service udevd-control.socket udevd-kernel.socket udevd.service
Failed to restart getty@.service: ENoent(UnitActionError)
Failed to restart lvm-activate-openeuler.service: Job errno
[root@openeuler-riscv64 ~]# sctl status NetworkManager.service dbus.service dbus.socket fstab.service getty@.service hostname-setup.service lvm-activate-openeuler.service sshd-keygen.target sshd-keygen@ecdsa.service sshd-keygen@ed25519.service sshd-keygen@rsa.service sshd.service udev-trigger.service udevd-control.socket udevd-kernel.socket udevd.service
● NetworkManager.service - Network Manager Service
 Loaded: true                                     
 Active: active (running)                         
 CGroup: NetworkManager.service                   
    PID: 971 /usr/sbin/NetworkManager --no-daemon
● dbus.service - D-Bus Service
 Loaded: true                                                                                      
 Active: active (running)                                                                          
 CGroup: dbus.service                                                                              
    PID: 970 /usr/bin/dbus-daemon --system --nofork --nopidfile --systemd-activation --syslog-only
● dbus.socket - D-Bus Socket
 Loaded: true               
 Active: active (listening) 
 CGroup: Empty cgroup path  
    PID: No process
● fstab.service - automount fstab device
 Loaded: true            
 Active: inactive (dead) 
 CGroup: fstab.service   
    PID: No process
Failed to show the status of getty@.service: NotExisted
● hostname-setup.service - hostname setup
 Loaded: true                   
 Active: active (exited)        
 CGroup: hostname-setup.service 
    PID: No process
Failed to show the status of lvm-activate-openeuler.service: NotExisted
● sshd-keygen.target
 Loaded: true              
 Active: active (active)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd-keygen@ecdsa.service - OpenSSH ecdsa Server Key Generation
 Loaded: true              
 Active: inactive (dead)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd-keygen@ed25519.service - OpenSSH ed25519 Server Key Generation
 Loaded: true              
 Active: inactive (dead)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd-keygen@rsa.service - OpenSSH rsa Server Key Generation
 Loaded: true              
 Active: inactive (dead)   
 CGroup: Empty cgroup path 
    PID: No process
● sshd.service - OpenSSH server daemon
 Loaded: true                                             
 Active: active (running)                                 
 CGroup: sshd.service                                     
   Docs: man:sshd(8) man:sshd_config(5)                   
    PID: 965 sshd: /usr/sbin/sshd -D [listener] 0 of 10-1
● udev-trigger.service
 Loaded: true                 
 Active: active (exited)      
 CGroup: udev-trigger.service 
    PID: No process
● udevd-control.socket
 Loaded: true               
 Active: active (listening) 
 CGroup: Empty cgroup path  
    PID: No process
● udevd-kernel.socket
 Loaded: true              
 Active: active (running)  
 CGroup: Empty cgroup path 
    PID: No process
● udevd.service
 Loaded: true                               
 Active: active (running)                   
 CGroup: udevd.service                      
    PID: 913 /usr/lib/systemd/systemd-udevd
[root@openeuler-riscv64 ~]# 
```

4. reboot重启环境后检查列表中的服务状态，重复步骤1、2

与之前结果相同

### 配置项测试：Description/Documentation/RemainAfterExit


1. 配置服务/usr/lib/sysmaster/system/base.service：

```bash
[Unit]
Description=this is a test
Documentation=this is doc

[Service]
ExecStart=/bin/sleep 2
RemainAfterExit=false
```

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=this is a test
Documentation=this is doc

[Service]
ExecStart=/bin/sleep 2
RemainAfterExit=false
[root@openeuler-riscv64 system]# 
```

2. sctl daemon-reload重新加载配置文件，重启服务检查服务sctl restart base; 检查服务sctl status base;有预期结果1

```bash
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - this is a test
 Loaded: true             
 Active: active (running) 
 CGroup: base.service     
   Docs: this is doc      
    PID: 892 /bin/sleep 2
[root@openeuler-riscv64 system]# 
```

3. 等待2s后再次检查服务，有预期结果2
```bash
[root@openeuler-riscv64 system]# sctl status base
● base.service - this is a test
 Loaded: true            
 Active: inactive (dead) 
 CGroup: base.service    
   Docs: this is doc     
    PID: No process
[root@openeuler-riscv64 system]# 

```

4. 将服务文件中的RemainAfterExit=false修改为RemainAfterExit=true；sctl daemon-reload重新加载配置文件后并重启服务后检查服务，有预期结果3

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=this is a test
Documentation=this is doc

[Service]
ExecStart=/bin/sleep 2
RemainAfterExit=true
[root@openeuler-riscv64 system]# sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - this is a test
 Loaded: true             
 Active: active (running) 
 CGroup: base.service     
   Docs: this is doc      
    PID: 912 /bin/sleep 2
[root@openeuler-riscv64 system]# 
```

5、等待2s后再次检查服务，有预期结果4

```bash
[root@openeuler-riscv64 system]# sctl status base
● base.service - this is a test
 Loaded: true            
 Active: active (exited) 
 CGroup: base.service    
   Docs: this is doc     
    PID: No process
```

6、停止服务：sctl stop base，在[Service]下增配置Type=oneshot，sctl daemon-reload重新加载配置，后台重启服务（sctl restart base &）后查看服务状态，有预期结果5

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=this is a test
Documentation=this is doc

[Service]
ExecStart=/bin/sleep 2
RemainAfterExit=true
Type=oneshot
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - this is a test
 Loaded: true               
 Active: activating (start) 
 CGroup: base.service       
   Docs: this is doc        
    PID: 955 /bin/sleep 2
[root@openeuler-riscv64 system]#
```

7、等待2s后再次检查服务，有预期结果6

```bash
[root@openeuler-riscv64 system]# sctl status base
● base.service - this is a test
 Loaded: true            
 Active: active (exited) 
 CGroup: base.service    
   Docs: this is doc     
    PID: No process
```

### 配置项测试：DefaultDependencies


1. 配置服务/usr/lib/sysmaster/system/base.service：
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 100

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 100
```

2. 备份/usr/lib/sysmaster/system/下的target文件，删除/usr/lib/sysmaster/system/下的target文件

```bash
[root@openeuler-riscv64 system]# ls
base.service      halt.target.bak         serial-getty@.service   sysinit.target.bak          udevd-kernel.socket
basic.target.bak  hostname-setup.service  shutdown.target.bak     syslog.socket               udevd.service
dbus.service      multi-user.target.bak   sockets.target.bak      syslog.target.bak           udev-trigger.service
dbus.socket       NetworkManager.service  sshd-keygen@.service    sysmaster-halt.service
fstab.service     paths.target.bak        sshd-keygen.target.bak  sysmaster-poweroff.service
getty@.service    poweroff.target.bak     sshd.service            sysmaster-reboot.service
getty.target.bak  reboot.target.bak       sysctl.service          udevd-control.socket

```

3. sctl daemon-reload重新加载配置文件，重启服务检查服务sctl restart base; 检查服务sctl status base;有预期结果1

```bash
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
Failed to restart base.service: Job errno
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true              
 Active: inactive (dead)   
 CGroup: Empty cgroup path 
    PID: No process
```

1. 在Description下增加DefaultDependencies=false；sctl daemon-reload重新加载配置文件后并重启服务后检查服务，有预期结果2

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service
DefaultDependencies=false

[Service]
ExecStart=/bin/sleep 100
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true               
 Active: active (running)   
 CGroup: base.service       
    PID: 917 /bin/sleep 100
[root@openeuler-riscv64 system]# 
```

5、停止base服务，有预期结果1

```bash
[root@openeuler-riscv64 system]# sctl stop base
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true            
 Active: inactive (dead) 
 CGroup: base.service    
    PID: No process
[root@openeuler-riscv64 system]# 
```

6、将DefaultDependencies=false修改为DefaultDependencies=true；sctl daemon-reload重新加载配置文件后并重启服务后检查服务，有预期结果1

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service
DefaultDependencies=true

[Service]
ExecStart=/bin/sleep 100
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
Failed to restart base.service: Job errno
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true            
 Active: inactive (dead) 
 CGroup: base.service    
    PID: No process
```

### 配置项测试：WantedBy

1. 配置服务/usr/lib/sysmaster/system/base.service及/usr/lib/sysmaster/system/wantedby.service：
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 100

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 100
[root@openeuler-riscv64 system]# cat wantedby.service 
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 100
[root@openeuler-riscv64 system]# 
```

2. sctl daemon-reload重新加载配置文件；sctl enable base后检查/etc/sysmaster/system/base.service.d，有预期结果1

```bash
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl enable base
[root@openeuler-riscv64 system]# ls /etc/sysmaster/system/base.service.d
ls: cannot access '/etc/sysmaster/system/base.service.d': No such file or directory
```

3. 给base.service增加[Install]配置如下：
[Install]
WantedBy=wantedby.service

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 100

[Install]
WantedBy=wantedby.service
[root@openeuler-riscv64 system]# 
```

4. sctl daemon-reload重新加载配置文件；sctl enable base后检查/etc/sysmaster/system/wantedby.service.wants/base.service，有预期结果2

```bash
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl enable base
[root@openeuler-riscv64 system]# ls /etc/sysmaster/system/wantedby.service.wants/base.service
/etc/sysmaster/system/wantedby.service.wants/base.service
[root@openeuler-riscv64 system]# 
```

5. sctl start wantedby启动wantedby.service后检查wantedby.service和base.service服务状态，有预期结果3

```bash
[root@openeuler-riscv64 system]# sctl start wantedby
[root@openeuler-riscv64 system]# sctl status wantedby.service
● wantedby.service - base service
 Loaded: true               
 Active: active (running)   
 CGroup: wantedby.service   
    PID: 932 /bin/sleep 100
[root@openeuler-riscv64 system]# sctl status base.service
● base.service - base service
 Loaded: true               
 Active: active (running)   
 CGroup: base.service       
    PID: 931 /bin/sleep 100
[root@openeuler-riscv64 system]# 
```

6、sctl stop base启动wantedby.service后检查wantedby.service和base.service服务状态，有预期结果4

```bash
[root@openeuler-riscv64 system]# sctl stop base
[root@openeuler-riscv64 system]# sctl start wantedby
[root@openeuler-riscv64 system]# sctl status wantedby.service
● wantedby.service - base service
 Loaded: true             
 Active: inactive (dead)  
 CGroup: wantedby.service 
    PID: No process
[root@openeuler-riscv64 system]# sctl status base.service
● base.service - base service
 Loaded: true               
 Active: active (running)   
 CGroup: base.service       
    PID: 939 /bin/sleep 100
[root@openeuler-riscv64 system]# 
```

7、sctl disable base后检查/etc/sysmaster/system/wantedby.service.wants/base.service，有预期结果5

```bash
[root@openeuler-riscv64 system]# sctl disable base
[root@openeuler-riscv64 system]# ls /etc/sysmaster/system/wantedby.service.wants/base.service
ls: cannot access '/etc/sysmaster/system/wantedby.service.wants/base.service': No such file or directory
[root@openeuler-riscv64 system]# 
```

8、sctl restart wantedby后检查wantedby.service和base.service服务状态，有预期结果6

```bash
[root@openeuler-riscv64 system]# sctl restart wantedby
[root@openeuler-riscv64 system]# sctl status wantedby.service
● wantedby.service - base service
 Loaded: true               
 Active: active (running)   
 CGroup: wantedby.service   
    PID: 948 /bin/sleep 100
[root@openeuler-riscv64 system]# sctl status base.service
● base.service - base service
 Loaded: true            
 Active: inactive (dead) 
 CGroup: base.service    
    PID: No process
[root@openeuler-riscv64 system]# 
```

### 配置项测试：ExecStart

```bash
[root@openeuler-riscv64 ~]# cat /etc/sysmaster/system.conf
LogLevel="info"
LogTarget="file"
LogFileSize=10240
LogFileNumber=10
[root@openeuler-riscv64 ~]# sctl daemon-reexec
[root@openeuler-riscv64 ~]# 
```

1. 配置服务/usr/lib/sysmaster/system/base.service：

```bash
[Unit]
Description=base service

[Service]
```

2. sctl daemon-reload重新加载配置文件；sctl restart base启动服务，有预期结果1

```bash
root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
Failed to restart base.service: Job errno
[root@openeuler-riscv64 system]# cat /var/log/sysmaster/sysmaster.log | grep "No ExecStart command is configured"
2024-05-21 19:53:07 sysmaster::unit::runtime Failed to load unit [base.service]: unit configuration error: 'No ExecStart command is configured and RemainAfterExit if false'.
```

3. 在[Service]下增加配置ExecStart=；sctl daemon-reload重新加载配置文件；sctl restart base启动服务，有预期结果1

```bash
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
Failed to restart base.service: Job errno
[root@openeuler-riscv64 system]# cat /var/log/sysmaster/sysmaster.log | grep "No ExecStart command is configured"
2024-05-21 19:53:07 sysmaster::unit::runtime Failed to load unit [base.service]: unit configuration error: 'No ExecStart command is configured and RemainAfterExit if false'.
2024-05-21 19:56:07 sysmaster::unit::runtime Failed to load unit [base.service]: unit configuration error: 'No ExecStart command is configured and RemainAfterExit if false'.
[root@openeuler-riscv64 system]# 
```


4、修改ExecStart=为ExecStart=/bin/sleep 2 ; /bin/sleep 222；sctl daemon-reload重新加载配置文件；sctl restart base启动服务，有预期结果2

[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 2 ; /bin/sleep 222
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
Failed to restart base.service: Job errno
[root@openeuler-riscv64 system]# cat /var/log/sysmaster/sysmaster.log | grep "More than Oneshot ExecStart command is configured"
2024-05-21 20:01:26 sysmaster::unit::runtime Failed to load unit [base.service]: unit configuration error: 'More than Oneshot ExecStart command is configured, service type is not oneshot'.
[root@openeuler-riscv64 system]# 


5、在[Service]下增加配置Type=oneshot；后台启动服务（sctl restart base&）；检查服务状态及sleep2、sleep222进程，有预期结果3

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 2 ; /bin/sleep 222
Type=oneshot
[root@openeuler-riscv64 ~]# sctl daemon-reload
[root@openeuler-riscv64 ~]# sctl restart base&
[3] 1070
[2]   Done                    sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true                
 Active: activating (start)  
 CGroup: base.service        
    PID: 1059 /bin/sleep 222
[root@openeuler-riscv64 system]# ps -elf | grep "sleep"
0 S root      1072   701  2  80   0 -   444 hrtime 20:06 ?        00:00:00 /bin/sleep 2
0 S root      1074   798 25  80   0 -  5295 pipe_r 20:06 pts/0    00:00:00 grep --color=auto sleep
[root@openeuler-riscv64 system]# ps -elf | grep "sleep"
0 S root      1075   701  0  80   0 -   444 hrtime 20:06 ?        00:00:00 /bin/sleep 222
0 S root      1077   798  0  80   0 -  5295 pipe_r 20:06 pts/0    00:00:00 grep --color=auto sleep
[root@openeuler-riscv64 system]# 
```

6、停止base服务，有预期结果4

```bash
[root@openeuler-riscv64 system]# sctl stop base
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true            
 Active: inactive (dead) 
 CGroup: base.service    
    PID: No process
```

7、修改服务配置文件如下，sctl daemon-reload重新加载配置文件；sctl restart base启动服务，等待3s后检查服务状态，有预期结果4：
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 1
Type=oneshot
ExecStart=/bin/sleep 2

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=/bin/sleep 1
Type=oneshot
ExecStart=/bin/sleep 2
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true            
 Active: inactive (dead) 
 CGroup: base.service    
    PID: No process
[root@openeuler-riscv64 system]# 
```

8、修改服务配置文件如下，touch /inexec；chmod 400 /inexec，sctl daemon-reload重新加载配置文件；sctl restart base启动服务，检查服务状态，有预期结果5：
[Unit]
Description=base service

[Service]
ExecStart=/inexec

```bash
[root@openeuler-riscv64 ~]# cat /usr/lib/sysmaster/system/base.service 
[Unit]
Description=base service

[Service]
ExecStart=/inexec
[root@openeuler-riscv64 ~]# touch /inexec
[root@openeuler-riscv64 ~]# chmod 400 /inexec
[root@openeuler-riscv64 ~]# sctl daemon-reload
[root@openeuler-riscv64 ~]# sctl restart base
[root@openeuler-riscv64 ~]# sctl status base
● base.service - base service
 Loaded: true            
 Active: failed (failed) 
 CGroup: base.service    
    PID: No process
[root@openeuler-riscv64 ~]# 
```

9、修改ExecStart=/inexec为ExecStart=/usr/bin/false；sctl daemon-reload重新加载配置文件；sctl restart base启动服务，检查服务状态，有预期结果5

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=/usr/bin/false
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true            
 Active: failed (failed) 
 CGroup: base.service    
    PID: No process
[root@openeuler-riscv64 system]# 
```

10、修改ExecStart=/usr/bin/false为ExecStart=-/usr/bin/false；sctl daemon-reload重新加载配置文件；sctl restart base启动服务，检查服务状态，有预期结果6

```bash
[root@openeuler-riscv64 system]# cat base.service 
[Unit]
Description=base service

[Service]
ExecStart=-/usr/bin/false
[root@openeuler-riscv64 system]# sctl daemon-reload
[root@openeuler-riscv64 system]# sctl restart base
[root@openeuler-riscv64 system]# sctl status base
● base.service - base service
 Loaded: true            
 Active: inactive (dead) 
 CGroup: base.service    
    PID: No process
[root@openeuler-riscv64 system]# 
```

