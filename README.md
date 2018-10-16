# Issues

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
