Getting started
============

To set up your system as middlebox, just use our installation script `sh install-requirements.sh`. 

If you want to do everything by hand you can use the following guide.

If you already installed all requirements, you can go further to [Usage](/usage.md)

#### Install required packages
Just use your command line
```sh
sudo apt-get update -y
sudo apt-get -y -q install git doxygen hugepages build-essential \
linux-headers-`uname -r` libdpdk-dev libmnl0 libmnl-dev libkmod2 \
libkmod-dev libnuma-dev libelf1 libelf-dev libc6-dev-i386 autoconf \
flex bison libncurses5-dev libreadline-dev python3 graphviz \
python3-pyelftools libboost-all-dev plantuml

pip3 install --user meson ninja

uname -r #Kernel >= 3.16 required
ldd --version #glibc >= 2.7 required
```

Install required [sparsehash](https://github.com/sparsehash/sparsehash) Densemap

#### install DPDK
1. Download from [DPDK Website](https://github.com/DPDK/dpdk)
2. extract:  tar xf dpdk.tar.gz
3. into folder:  cd dpdk
4. build lib, driver, test:  
  ```sh
    meson build     # include all examples: meson -Dexamples=all build
    ninja -C build
  ```
5. include dpdk to path
  - only for session: `export PATH=$PATH:</path/to/file>`
  - permanently add `export PATH=$PATH:</path/to/file>` to your `~/.bashrc` file (at end of file).

or with apt `sudo apt install dpdk`

#### Hugepages
1. reserve Hugepages (in runtime): 
    1. configure Hugepages
    `echo 64 > /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages`
    `echo 32 > /sys/devices/system/node/node0/hugepages/hugepages-1048576kB/nr_hugepages`
    2. create directory for mounting 
    `mkdir -p /mnt/huge`
    `mountpoint -q /mnt/huge`
    `mount -t hugetlbfs nodev /mnt/huge`
    3. Check hugpages `grep Huge /proc/meminfo`
2. Run poll mode driver test:  `build/app/dpdk-testpmd -c7 --vdev=net_pcap0,iface=eth0 --vdev=net_pcap1,iface=eth1 -- -i --nb-cores=2 --nb-ports=2 --total-num-mbufs=2048`

##### in boot time
Modify Linux boot time parameters inside `/etc/default/grub`. Huge pages will be spread equally between all NUMA sockets.
`GRUB_CMDLINE_LINUX="default_hugepagesz=1G hugepagesz=1G hugepages=32"`

Update the grub configuration file and reboot.
```sh
grub2-mkconfig -o /boot/grub2/grub.cfg
reboot
```
Create a folder for a permanent mount point of hugetlbfs `mkdir /mnt/huge` 

Add the following line to the `/etc/fstab` file: `nodev /mnt/huge hugetlbfs defaults 0 0`

Persistent huge pages are never swapped by the Linux kernel!

#### Mac, IP & PCI adress
1. `ifconfig -a` to view MAC and IP adress
2. `ethtool -i <interface name>` to get PCI adress
3. Load ibuverbs on each reboot with `modprobe -a ib_uverbs`

##### Test your DPDK installation 
TX side
```sh
testpmd \
  -l <core-list> \
  -n <num of mem channels> \
  -w <pci address of the device you plan to use> \
  --vdev="net_vdev_netvsc<id>,iface=<the iface to attach to>" \
  -- --port-topology=chained \
  --nb-cores <number of cores to use for test pmd> \
  --forward-mode=txonly \
  --eth-peer=<port id>,<receiver peer MAC address> \
  --stats-period <display interval in seconds>
```

RX side
```sh
testpmd \
  -l <core-list> \
  -n <num of mem channels> \
  -w <pci address of the device you plan to use> \
  --vdev="net_vdev_netvsc<id>,iface=<the iface to attach to>" \
  -- --port-topology=chained \
  --nb-cores <number of cores to use for test pmd> \
  --forward-mode=rxonly \
  --eth-peer=<port id>,<sender peer MAC address> \
  --stats-period <display interval in seconds>
```

#### Problems at Crash
DPDK won't free hugepages and can therefore not be restartet with no hugepages free in system.

Issue could be like you removed `/mnt/huge` and trying to modify the nr_hugepage
```sh
echo 0 > /sys/devices/system/node/node0/hugepages/hugepages-2048kB/nr_hugepages #Numa case
echo 0 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages #non-NUMA case
```

steps to follow while un-mapping hugepage:
1. `ls -l /mnt/huge/ `
2. `rm -rf rtemap_*` if there are any "rtemap_*" delete all
3. `mount | grep huge`
    hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime,seclabel)
4. `ls /dev/hugepages`
    ```sh
    rtemap_0  rtemap_1202  rtemap_1408  rtemap_1613  rtemap_1819  rtemap_2023  rtemap_387  rtemap_592  rtemap_798
    rtemap_1  rtemap_1203  rtemap_1409  rtemap_1614  rtemap_182   rtemap_2024  rtemap_388  rtemap_593  rtemap_799
    ```
5. If above files are present delete all of them.
    1. `sudo umount /mnt/huge`
    2. `sudo rm -R /mnt/huge`
    3. Then write 0 to nr_hugepages mentioned at start
