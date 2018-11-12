# How to install Dspace 6 into Ubuntu Server 16.04 running on a VirtualBox

## System Information

<b>Host Machine</b>: Ubuntu Desktop 18.04

<b>VirtualBox</b>: Ubuntu Server 16.04

<b>Dspace Version</b>: 6.2 (Downloaded from [Here](https://github.com/DSpace/DSpace/releases/tag/dspace-6.2))

### Note: I am assuming this is a FRESH VirtualBox installation of Ubuntu Serevr 16.04

### Step 1: Install Ubuntu Server 16.04 in VirtualBox

- Download Ubuntu 16.04 from Here
- Downlaod VirtualBox in your host Ubuntu 18.04 `sudo apt-get install virtualbox`
- Open virtualBox and create new
- Use memorysize: 4096 MB (I have 16GB RAM in my laptop, use appropriate amount based on your current RAM)
- VirtualDisk size 35GB with all default configuration
- Insert Ubuntu Disk Image in the VMBox from Settings -> Storage
- Start VM
- Host Name: ubuntu
- Full Name of User: Dspace User
- Username for account: dspace
- Password: 123456 (it is up to your choice)
- Proxy: None
- Guided Installation - User entire disk and set up VLM
- select No automatic update
- Do not intall any software package

### Step 1 : Configure your VirtualBox OS to run from Host terminal (SSH)

Once installed, login to your Ubuntu Server 16.04 VBox, with your username(dspace) and password(123456)

- Run `sudo apt-get update`
- Install openSSH server with `sudo apt-get install openssh-server`
- Now check the network configuration with `ifconfig -a` and you shoud see two adapter `enp0s3` and `lo`
- Now shutdown you virtualBox with `sudo shutdown -h now`

Now in your VirtualBox Settings
- It is good practice to take snapshots of your VMBox so that if your do anything wrong and do not know how to right them, you can simply revert back.
- Select your VMBox and click on Settings
- Go to Network
- In Adapter 1, tick the <b>Enable Network Adapter</b> if not already and Attached to <b>Bridge Connection</b>
- Go to Adapter 2, tick the <b>Enable Network Adapter</b> if not already and Attached to <b>Host-Only Adapter</b>
- Click <b>OK</b>
- Now start your VM again.

Login to your VM,
- Run `ifconfig -a`
- You should see a third adapter `enp0s8`
- Now configure this third adapter with `sudo vim /etc/network/interfaces`
- At the end of the file start writing following (in Vim, press <b>`I`</b> to start writing, when done press <b>`Esc`</b> to jump out of writing mode and then press <b>`:w`</b> to save, press <b>`:q`</b> to get out of editor. Use <b>`:wq`</b> to save and exit at the same time)
```
auto enp0s8
iface enp0s8 inet dhcp
```
- Now reboot the VM with `sudo reboot`
- Once rebooted, login again and type `ifconfig -a`
- You should see the `enp0s8` with ip address. (Here mine is 192.168.56.101) We will use that IP address into our host os terminal.

In your host OS (ubuntu desktop 18.04)
- Open Terminal and type `ping 192.168.56.101` and you should receive the packages.
- Now type `ssh dspace@192.168.56.101` (here dspace is username)
- You would be prompted for password, enter your VM password (123456)
- You should now be logged in to your VM directly from your host terminal. Now you can work on full resolution rather than small window.
- You can exit out from VM by typing `exit` But <b>DO NOT</b> close the VM


