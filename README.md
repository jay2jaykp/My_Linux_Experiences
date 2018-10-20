# Issues
## SSD Optimizatio in Ubuntu
This is a real thing. I did not know about it before I search for how to partition Ubuntu and there were dispute in the resources that I fouind between only SSD and hybrid drives (SSD + HDD). Some mentioned TRIM (i dont know what it is) to be enable and some ignores it all along. Some say do not use SWAP as it wears down the SSD and some say it is OK. Here some guides that I think should be informative and trustworthy however I haven't found any official <b>best practice on partitioning SSD for Ubuntu</b>.
1. https://www.youtube.com/watch?v=8OKjSOUgLJU this video is on point. must watch.
2. https://help.ubuntu.com/community/PartitioningSchemes this is official ubuntu community guide but no mention of SSD only setups. Very dissapointing.
3. https://sites.google.com/site/easylinuxtipsproject/ssd this is a very extensive resource but not for ubuntu but linuxMint. I think it should be more or less same.

## Screen Flickering Issue
I have noticed extreme screen flickering in my PC when installed Ubuntu 18.04 (do not know about previous version though). A signle google search lead me to [github issue link](https://github.com/rolandguelle/razer-blade-stealth-linux/issues/7#issuecomment-344150633) that solved the issue. 
- Open Terminal 
- ```sudo nano /etc/default/grub```
- change the line ```GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"``` to ```GRUB_CMDLINE_LINUX_DEFAULT="quiet splash i915.enable_rc6=0"``` 
- save the file with ```ctrl + O``` and exit the editor with ```ctrl + x```
- reboot the PC
This should work.
### Reference 
1. Razer Blade Screen flicker: https://github.com/rolandguelle/razer-blade-stealth-linux/issues/7#issuecomment-344150633
2. How to change kernel boot parameter: https://askubuntu.com/questions/19486/how-do-i-add-a-kernel-boot-parameter


## Trackpad pointer jumps unevenly
This is also an issue I have faced with the first boot of Ubuntu. But after installing Microcode as per the suggestion of same [github project](https://github.com/rolandguelle/razer-blade-stealth-linux#install), running ```sudo apt install intel-microcode``` fix the problem.
This should work.
### Reference
1. Razer Blade Linux: https://github.com/rolandguelle/razer-blade-stealth-linux#install

## Everything Froze
While writing this repository, my ubuntu stopped working suddenly and froze the whole system including mouse and keyboard. Quick google search led to [askubuntu forum](https://askubuntu.com/questions/4408/what-should-i-do-when-ubuntu-freezes) but the solution requires the ```SysRq``` key but Razer Blade Stealth does not have that.

I have tweeted to [@rolandguelle](https://twitter.com/rolandguelle) asking some help for the guide available to best partitioning practice for SSD only PCs.
Found two links that explain the partitioning on SSD.
1. https://sites.google.com/site/easylinuxtipsproject/ssd (I find this one more useful as per my understanding level of Ubuntu and hardware-software in general)
2. http://www.ocsmag.com/2016/04/30/using-solid-state-drives-on-linux/

Still Pending...
### Reference
1. Frozen ubuntu: https://askubuntu.com/questions/4408/what-should-i-do-when-ubuntu-freezes

# Installation

## Google Chrome
Google Chrome is a must have web browser in my opinion. Initially, not seeing it in Ubuntu App Store dissapointed me but then I found out that it needs to be installed through normal downloading the .deb file and install it. 
This should works.

## VirtualBox
Downlaod .deb file from Oracle V box [official website](https://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html)
Double click and isntall.
It is raising an error as below when I run any irtual environment.

```
The VirtualBox Linux kernel driver (vboxdrv) is either not loaded or there is a permission problem with /dev/vboxdrv. Please reinstall the kernel module by executing

'/sbin/vboxconfig'

as root.

where: suplibOsInit what: 3 VERR_VM_DRIVER_NOT_INSTALLED (-1908) - The support driver is not installed. On linux, open returned ENOENT. 
```
Installing VirtualBox by downloading and running was a bad idea I suppose.

Quick fix was to run ```sudo apt-get install virtualbox``` and run ```virtualbox```
This should work.

## Flashing Android ROM
One thing I often do is flashing custom ROMs to my OneplusOne device. I needed to get the access of storage system of mobile device in my ubuntu system when it is on fastboot mode or recovery mode. One thing perticularly I wanted is to access internal storage once fully wiped down in recovery to add the rom at that point of time (for fresh install).

I forund this amazing [amazing](http://bernaerts.dyndns.org/linux/74-ubuntu/354-ubuntu-xenial-android-adb-fastboot-qtadb) that allow me to install appropriate drivers and tools. I have run the code as it is given in the page but for the sake of preservation I will note them down here.

1. Install Android Tools
```sudo apt-get install android-tools-adb android-tools-fastboot```
2. Update to latest ADB and fastboot
```
#check adb version before
adb version

wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip

sudo unzip -d /usr/local/sbin platform-tools-latest-linux.zip

sudo wget -O /usr/local/sbin/adb https://raw.githubusercontent.com/NicolasBernaerts/ubuntu-scripts/master/android/adb

sudo wget -O /usr/local/sbin/fastboot https://raw.githubusercontent.com/NicolasBernaerts/ubuntu-scripts/master/android/fastboot

sudo chmod +x /usr/local/sbin/platform-tools/adb /usr/local/sbin/adb

sudo chmod +x /usr/local/sbin/platform-tools/fastboot /usr/local/sbin/fastboot

#check adb version after
adb version
```
3. Declare vendor ID for ADB
I think it is not necessary for me as my phone is old enough (5 year old to be precise) to recognized by any version of adb as of 2018.
But I would note down to code regardless.
```
mkdir --parent $HOME/.android

wget -O $HOME/.android/adb_usb.ini https://raw.githubusercontent.com/NicolasBernaerts/ubuntu-scripts/master/android/adb_usb.ini
```
4. Setup ADB Udev Rule 
Your device ned to be in USB debugging mode for the next step.
```lsusb```
You should found your phone in the list.
```
sudo wget -O /etc/udev/rules.d/51-android.rules https://raw.githubusercontent.com/NicolasBernaerts/ubuntu-scripts/master/android/51-android.rules

sudo chmod a+r /etc/udev/rules.d/51-android.rules

sudo service udev restart
```
5. Allow ADB trusted connection
```adb devices```
Allow the request of adb in your phone and rerun the command for your pc to recognize the device.
6. Install QtADB
Prerequisite: Your phone needs to be rooted and install app [BusyBox](https://play.google.com/store/apps/details?id=stericson.busybox)
Run the following command to confirm the BusyBox install.
```adb shell busybox ls -l -a```

Installation process
```
sudo apt-get -y install libqtgui4 libqt4-network libqt4-declarative

wget -O qtadb.tar.gz http://motyczko.pl/qtadb/QtADB_0.8.1_linux64.tar.gz

tar -xvf qtadb.tar.gz

sudo mv ./QtADB*/QtADB /usr/local/sbin/qtadb

sudo chmod +x /usr/local/sbin/qtadb

rm qtadb.tar.gz

rm -R QtADB*
```

7. It might crash at this point when run the following
```qtadb```

fix this crash by following
```
mkdir --parents $HOME/.config/Bracia

wget $HOME/.config/Bracia/QtADB.conf https://raw.githubusercontent.com/NicolasBernaerts/ubuntu-scripts/master/android/QtADB.conf
```
rerun the above command to confirm fix.
8. Create application launcher with icon and place in all applications
```
sudo wget -O /usr/share/icons/qtadb.png https://github.com/NicolasBernaerts/ubuntu-scripts/raw/master/android/qtadb.png

sudo wget -O /usr/share/applications/qtadb.desktop https://raw.githubusercontent.com/NicolasBernaerts/ubuntu-scripts/master/android/qtadb.desktop
```

### Reference
1. Ubuntu 16.04 LTS - Install Android Tools (ADB, Fastboot & QtADB) By Nicolas Bernaerts : http://bernaerts.dyndns.org/linux/74-ubuntu/354-ubuntu-xenial-android-adb-fastboot-qtadb
