# Centos7 Setup
## Enable LVM Disk Partitioning
```
yum update -y
pvs
pvcreate /dev/sdb
vgcreate vg01 /dev/sdb
vgdisplay
lvcreate -n lv_data -l 100%FREE vg01
lvdisplay
mkfs.ext4 /dev/vg01/lv_data
mkdir /data
mount /dev/vg01/lv_data /data
cd /data
```
<br/>

## Install packages needed for VMWare Workstation
```
yum install -y git unzip rsync libXtst libXinerama libXcursor libX11-devel
yum groupinstall "Development tools"
yum install -y kernel-devel elfutils-libelf-devel open-vm-tools
```
<br/>

## Download packages/tarballs
```
wget https://download.nomachine.com/download/6.11/Linux/nomachine_6.11.2_1_x86_64.rpm
wget https://releases.hashicorp.com/packer/1.6.2/packer_1.6.2_linux_amd64.zip
wget https://golang.org/dl/go1.15.linux-amd64.tar.gz
tar xzf go1.15.linux-amd64.tar.gz
export GOPATH=/data/go
export PATH=$PATH:$GOPATH/bin
# Download VMWare Workstation and OVFTools
```
<br/>

## Enable GUI
```
wget https://download.nomachine.com/download/6.11/Linux/nomachine_6.11.2_1_x86_64.rpm

yum groupinfo "Server with GUI"
yum groupinfo "GNOME Desktop"
yum groupinstall 'GNOME Desktop'
systemctl enable graphical.target --force
ls -l /etc/systemd/system
rm -rf '/etc/systemd/system/default.target'
ln -s '/usr/lib/systemd/system/graphical.target' '/etc/systemd/system/default.target'
reboot
```
<br/>
