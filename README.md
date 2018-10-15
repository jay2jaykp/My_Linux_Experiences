#Issues
-
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

