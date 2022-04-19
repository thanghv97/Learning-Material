### 1. cpufrequtils
  + install:    
    + ubuntu
        ```
            sudo apt update
            sudo apt install cpufrequtils
        ```
  + application: 
    + [001. Set performance for cpu:](#001-set-performance-for-cpu)
### 2. iptables: 
  *a user-space application program allows configuring the tables provided by the Linux kernel firewall, as well as the chains and rules it store.*
  + install:
    + ubuntu 
        ```
            sudo apt-get update 
            sudo apt-get install iptables
        ```
  + application: 
    + [002]	
  + reference: 
    + https://blogd.net/linux/iptables-chuyen-sau/

### 3. gparted: 
  *a GTK front-end to GNU Parted and an offical GNOME partition-editing application. It is used for creating, deleting, resizing, moving, checking, and copying disk partitions and their file systems.*
  + install:
    + ubuntu  
        ```
            sudo apt update
            sudo apt install gparted
        ```
  + application: 
    + [006]
  + reference:
    + https://en.wikipedia.org/wiki/GParted (introduce background and supported features)

### 4. firewalld
  *Firewalld provides a dynamically managed firewall with support for network/firewall zones that define the trust level of network connections or interfaces. It has support for IPv4, IPv6 firewall settings, ethernet bridges and IP sets. There is a separation of runtime and permanent configuration options. It also provides an interface for services or applications to add firewall rules directly.*
  + install:
    + ubuntu
        ```
            sudo apt-get update
            sudo apt-get install firewalld
        ```
  + application:
    + [008]
  + reference:
    + https://firewalld.org/ 


# ------ Service -----------------------------------------
### 001. systemd-logind.service
  *systemd-logind is a system service that manages user logins*
  + application:
    + [009. Set mode handle(do nothing) when close laptop lib](#009-set-mode-handle-do-nothing-when-close-laptop-lib)

# ------ APPLICATION -------------------------------------
### 000. Display information of operating system
  - 
  ```
    uname
  ```
  - 
  ```
    lsb_release -id
  ```

### 001. Set performance for cpu:
```
    + echo 'GOVERNOR="performance"' | sudo tee /etc/default/cpufrequtils
    + sudo systemctl disable ondemand
    + sudo systemctl restart cpufrequtils
```
  + reference:
    + https://www.kernel.org/doc/Documentation/cpu-freq/governors.txt
    + https://askubuntu.com/questions/1021748/set-cpu-governor-to-performance-in-18-04

### 002. Open port TCP:
```	
    + iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
```

### 003. Check USB port:
```	
    + lsusb
```

### 004. Test send message:
```
    + nc(netcat)
```	
  + udp:
```	
    + server: nc -l -u 1711
    + client: nc -u 127.0.0.1 1711
```
### 005. Check UUID Harddisks or Partitions
```	
    + sudo blkid
```

### 006. Mount disk
**use gparted (GUI)**
```
    + sudo gparted (use gparted to config disk)
```

**use command line**
```
    + fdisk -l | grep '^Disk' (list all detected hard disks)
    + sudo vim /etc/fstab (add disk need to mounted to /etc/fstab)
        + ex: [file_system(name or uuid)]/dev/sda1 [mount_point]/home/thanghv7/data [type(cfg in gparted)]ext4 default 0 0
    + sudo mount -a (mount all file system in /etc/fstab)
```
  + reference:
    + https://linuxconfig.org/how-fstab-works-introduction-to-the-etc-fstab-file-on-linux

### 007. Unmount disk
```
    + sudo umount [file_system or mounting_point]
```
### 008. disable&enable firewall
**use firewalld**
```
    + sudo systemctl [start|stop|enable|disable] firewalld.service 
```

### 009. Set mode handle when close laptop lib
  + do nothing 
```
    + sudo -H gedit /etc/systemd/logind.conf
    + set HandleLidSwitch=ignore
    + sudo systemctl restart systemd-logind
```
  + reference: 
    + https://askubuntu.com/questions/15520/how-can-i-tell-ubuntu-to-do-nothing-when-i-close-my-laptop-lid