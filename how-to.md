<!-- 
Markdown cheat cheet:
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
 -->

<!-- 
#######################################################################################################################################
#######################################################################################################################################
#######################################################################################################################################
#######################################################################################################################################
 -->
# <center> _**Creating a virtual development environment/server/box**_ </center>
<!-- 
#######################################################################################################################################
#######################################################################################################################################
#######################################################################################################################################
#######################################################################################################################################
 -->


<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_Create the VM_** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

<!-- ========================================================== -->
> #### **_Option 1 - Download a pre-installed VirtualBox (VB) image (ova file)_**
<!-- ========================================================== -->

- Install the latest VB version from: https://www.virtualbox.org/ 

- Go to: https://www.linuxvmimages.com/

- Locate the Centos 7 VB image, or go to: https://www.linuxvmimages.com/images/centos-7/

IMPORTANT: please take not of the username and password located under the image page, it is usually:

username: centos
password: centos

- Scroll down to the Graphical Desktop Installation, or download it from [here.](https://sourceforge.net/projects/linuxvmimages/files/VirtualBox/C/7/CentOS_7.7.1908_VBG.zip/download)

- Unzip the ova image file and place it on the desktop

- open VB.

- Go to: File and click on Import Appliance

- Browse to the location of the ova file.

- Change the name as desired.

- Under Mac Address Policy select Create New...

- Uncheck Import Hard Drive as VDI.

- Click on Import.

- Click on Agree.

- Proceed to the section: [VB VM SETTINGS](#vb-vm-settings) to set the rest of the setting, before launching.

- Launch the vm.

- Then proceed to the section: [SETUP GUEST ADDITIONS AND SHARED HOST FOLDER](#setup-guest-additions-and-shared-host-folder)

- switch to root user:

```bash
sudo su -
```

- Create your user:

```bash
useradd admin
```

- Set your password:

```bash
passwd admin
```

- Give your user admin rights

```bash
usermod -a -G wheel admin
```


- login using your user:

- delete the old user:

```bash
sudo userdel -r centos
```

- Update guest additions, by clicking on the Devices menu on the menu bar of the VM window, then click on Insert Guest Additions CD.

- A popup window will appear, click on run, you will be prompted to enter your user password.

- Wait until you are asked to hit enter to close the window, then reboot.




<!-- ========================================================== -->
> #### **_Option 2 - Start from scratch_**
<!-- ========================================================== -->

 - Go to https://wiki.centos.org/Download

 - Under CentOS Linux Version 7 Minor Release 8 (2003) click on RPMs, or click [here](http://isoredirect.centos.org/centos/7/isos/x86_64/) then click on one of the images in the list, place the iso file: CentOS-7-x86_64-DVD-2003.iso on your desktop.

 - Open VB.

 - On the menu bar go to Machines - New

 - Under name call it devbox or any name you choose.

 - Leave the machine folder at the default value: C:\Users\username\VirtualBox VMs

 - Under Type select Linux.

 - Under version select Redhat 64-bit then click next.

 NOTE: If you do not see any 64-Bit versions and only 32-Bit versions, go [here](http://www.fixedbyvonnie.com/2014/11/virtualbox-showing-32-bit-guest-versions-64-bit-host-os/#.XtHduzpKhHY) to fix the issue.

 - Set RAM preferably 4096 MB, but 2048 MB should work fine, then click next.

 - Under hard disk select create a virtual hard disk now, then click next.

 - Under hard disk file type select VHD then click next.

 - Under storage on physical hard disk select dynamic allocation, then click next.

 - Under file location and size, leave the default location: C:\Users\username\VirtualBox VMs\devbox\devbox.vhd and set the size to 30 GB then click create.

- select the VM you just created devbox to highlight it.

- Click on settings.

- On the left panel click on storage.

- Under Controller: IDE click on the optical disk icon that says Empty.

- on the right where it says optical drive, click on the optical disk icon, then click on Choose a disk file, then browse to the location of the iso file we downloaded earlier named: CentOS-7-x86_64-DVD-2003.iso on your desktop.

- Click ok, this will boot the VM from optical disk

- Proceed to the "VB VM SETTINGS" section to set the rest of the setting, before launching.

- After completing the VM setting section, the VM will launch.

- If you are prompted to select an optical disk, click cancel.

- The first screen is the Centos 7 welcome screen, select English and click continue.

- Wait for the second screen "INSTALLATION SUMMARY" to load then click on "SOFTWARE SELECTION".

- Click on Server with GUI, then on the right side select the following:

  - Compatibility Libraries
  - Development Tools
  - System Administration Tools.

  Then click on Done.

- Wait for the "INSTALLATION SUMMARY" to load all sections.

- Click on INSTALLATION DESTINATION.

- Click on Automatically Configure partitioning, then click on Done.

- Wait for the "INSTALLATION SUMMARY" to load all sections.

- Click on NETWORK & HOSTNAME

- Click on both adapters and click on the On Button to connect, then underhost name type devbox then click on apply, finally click on Done.

- Wait for the "INSTALLATION SUMMARY" to load all sections.

- Click on begin installation.

- While the installation is running, click on user creation.

- Under Full name type: Dev Admin or your desired name.

- Under username type: admin or the desired username

- Click on both: Make this user an admin and click on Require a password to use this account.

- Under password type: admin or the desired password

- Click Done.

- Click on root password.

- Type the password: admin or any desired password.

- If the password is too short you will get a warning, just click on Done again.

- Wait for the installation to finish.

- Click on the reebot when installation is done.

- After rebboting, accept the license, then click on finish configuration.

- login with user: admin and password: admin

- open the terminal by going to application - system tools then click on terminal.

- and run this command to update the system:

```bash
sudo yum update -y
sudo reboot now
```

- Go to the section: [SETUP GUEST ADDITIONS AND SHARED HOST FOLDER](#setup-guest-additions-and-shared-host-folder)

- Done.

- At this point you might want to save this image as-is by creating an ova file, this machine state represent a contos 7 server with gui that has nothing installed on it and can be a good starting point for any further installation.

Follow this naming convention to recognize the image:

DATE - LINUX DISTRO - KERNEL VERSION - VIRTUALBOX VERSION - GUEST ADDITIONS VERSION
30-MAY-2020 - CENTOS7 SERVER WITH GUI - 3.10.0-1127.8.2.el7.x86_64 - VB6.1.8 - GA6.1.8.ova

You can maintain it periodically by downloading the ova file launching the VM tunning a system update then create an ova file out of it and uploading it.

- Go to the section: [BACKING UP THE VM USING VB OVA FILES](#backing-up-the-vm-using-vb-ova-files)


<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_VB VM SETTINGS_** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

- On the host desktop create a folder called "sharedwithvb", for example, this folder will be shared between the VM and the host.

- select the VM you just imported to highlight it.

- Click on settings.

- Click on General

- Go to the Advanced tab.

- Under shared clipboard select bidirectional.

- Under Drag n Drop select bidirectional.

- Click on system on the left panel

- Click on the Motherboard tab.

- Under base memory, type 2048 MB (preferably 4096 MB)

- Under boot order, uncheck floppy disk and network.

- Make sure the optical drive is on top of the hard disk.

- Under pointing device select USB Tablet.

- click on display on the left panel.

- Set the video memory to the max: 128 MB

- Click on processor on the left panel

- Under processors slide to two processors.

- Click on Network on the left panel

- Click on Adapter 1

- Check "Enable Network Adapter"

- Under attached to select host oly adapter.

- Click on Adapter 2

- Check "Enable Network Adapter"

- Under attached to select NAT.

- Click on Shared folders on the left panel

- Click on the add button.

- Under folder path select other and browse to the folder we created earlier: sharedwithvb

- Check Auto-mount and click ok.

- Click OK.

- Right click on the VM, then, under start select detachable start.


<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_SETUP GUEST ADDITIONS AND SHARED HOST FOLDER_** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

Guest additions allow for fullscreen improved resolution and bidirectional clipboard.

- Make sure you covered the [VB VM SETTINGS](#vb-vm-settings) section first.

- Start the VM.

- Go to the menu bar of the VM and click on Devices then insert Guest Additions disk.

- enter your user pass when prompted.

- wait for the installation to complete then reboot.

- Allow your user to access the shared folder:

```bash
usermod -a -G vboxsf admin
```

Then Reboot:

```bash
reboot now
```

NOTE: This might take a while

- login using your user.

- To check screen resolution go to the VM's menu bar and click on view - virtual screen 1 then select the desired scale, preferably 100%, to apply changes restore the vm window then maximize again, you should now see the desired resolution.

- copy and paste text between the host and the vm to test the bidirectional clipboard.

- Make sure you can access the shared folder and can read and write files.

- DONE!


<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_SYSTEM CONFIGURATION_** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

<!-- ========================================================== -->
> #### **_Adding the user to the sudoers file_**
<!-- ========================================================== -->

- Allow your user to use sudo without a password by adding this line to the sudoers file:

Open the sudoers file by running:

```bash
sudo visudo
```

- scroll to the very end and hit "i".

and add this line at the very end:

```ini
admin ALL=(ALL) NOPASSWD: ALL
```

save the file by hitting the escape button, then hitting the colon button then hit the "x", finally hit enter.

<!-- ========================================================== -->
> #### **_.bashrc_**
<!-- ========================================================== -->


























<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_BACKING UP THE VM USING VB OVA FILES_** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

- First launch the vm and update the system:

```bash
sudo yum update -y
```

- run this command to get the latest kernel version and take note of it:

```bash
uname -r
```

Example result: 3.10.0-1127.8.2.el7.x86_64

- reboot the vm:

```bash
sudo reboot now
```

- Make sure the vm is running normally.

- Shutdown the vm.

- Create a backup ova file by first selecting and highlighting the vm, click on the vm name on the left panel.

- get the VB version by going to the menu bar and clicking on help then about, take note of VB version.

- On the menu bar go to file - export appliance.

- under format select 2.0

- under file browse to the desktop and name your ova file as follows:

DATE - LINUX DISTRO - KERNEL VERSION - VIRTUALBOX VERSION - GUEST ADDITIONS VERSION

Example:

29-MAY-2020 - CENTOS7 - 3.10.0-1127.8.2.el7.x86_64 - VB6.1.8 - GA6.1.8.ova

- Under MAC Address Policy select include all network adampter MAC Addresses

- Check write manifest file (for error checking)

- uncheck include ISO

- Click on export

- DONE!

- Now you can save this image on google drive or microsoft one drive for high avaialbility accessibility.

<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_Upgrading VB and Guest Additions_** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->


- Make sure the vm is shutdown.

- select the vm on the left panel.

to upgrade virtualbox:

- update the system first:

```bash
sudo yum update -y
sudo shutdown now
```

- go to: https://www.virtualbox.org/wiki/Downloads to get the latest VB version and install it.

- Launch the vm, then go to the vm menu bar and select "Devices: then "insert guest additions cd"

- You will be prompted for your password.

- Wait until you are promted to hit enter to close the terminal.

- Reboot.

```bash
sudo reboot now
```

- Make sure your vm runs normally by making sure the resolution is correct and that it scales as required by restoring the vm window and then maximizing it, also test the bidirectional clipboard, and make sure you can access (read and write) the shared folder.

- DONE!































<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_ Install important system packages _** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

This must come before installing any other software on the vm.

- update the system:

```bash
yum update -y
```

- Libraries needed during compilation to enable all features of Python:

```bash
yum install -y wget epel-release zlib-devel bzip2-devel openssl openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel expat-devel libffi-dev gcc gcc-c++ zlib libffi-devel
```

- Make sure the developmet tools are installed:

```bash
sudo yum groupinstall -y "Development Tools"
```

- Reboot.



<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_ Install python (2.7 - 3.7 - 3.8), pip and pipenv _** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

- Python2.7 will be preinstalled, you might need to install pip:

```bash
sudo su -
wget https://bootstrap.pypa.io/get-pip.py
```

then run:

```bash
python2.7 get-pip.py
```

To upgrade pip:

```bash
sudo su -
python2.7 -m pip install --upgrade pip
```

- Install python 3.7

```bash
sudo su -
cd /root
wget http://python.org/ftp/python/3.7.5/Python-3.7.5.tar.xz
tar xf Python-3.7.5.tar.xz
cd Python-3.7.5
./configure --prefix=/usr/local --enable-shared LDFLAGS="-Wl,-rpath /usr/local/lib"
make && make altinstall


```

- Then upgrade pip3.7

```bash
sudo su -
python3.7 -m pip install --upgrade pip
```

- Install pipenv on the user level (not globally):

```bash
pip3.7 install --user pipenv
```

Make sure the path: $HOME/.local/bin is added to your ~/.bashrc file, pipenv needs this.


<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_ Install development software _** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->


- Install aws cli:

```bash
pip3.7 install --user awscli
```

- Install git 2:

```bash
sudo yum -y install https://packages.endpoint.com/rhel/7/os/x86_64/endpoint-repo-1.7-1.x86_64.rpm
sudo yum install git


```

- Install VSCode:

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo yum install code -y


```






Then:

linux brew

nodejs

docker

ansible

terraform

tfenv

linuxbrew

Git

jq

vscode

sublime text

Chrome



<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_ Configure _** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

Open the file ~/.bashrc remove every thing and add the following:

```bash
# .bashrc

########################################
# Source global definitions
########################################
# Get the aliases and functions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

########################################
# Color LS output to differentiate between directories and files
########################################

export LS_OPTIONS="--color=auto"
export CLICOLOR="Yes"
export LSCOLOR=""

########################################
# No brainer, default to Vim
########################################
export EDITOR="vim"

########################################
# User specific environment and startup programs
########################################
export PATH=$PATH:$HOME/scripts:$HOME/.local/bin:$HOME/bin:$HOME/terraform:/usr/local/bin:/usr/local/lib:/usr/bin:/bin
export PATH="/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin/:$PATH"
export MANPATH="/home/linuxbrew/.linuxbrew/share/man:$MANPATH"
export INFOPATH="/home/linuxbrew/.linuxbrew/share/info:$INFOPATH"
########################################//

########################################
# Uncomment the following line if you don't like systemctl's auto-paging feature:
########################################
# export SYSTEMD_PAGER=

########################################
# User specific aliases and functions
########################################
alias ll='ls -Filah --color=auto'


########################################
# Git branch in prompt.
########################################
# get current branch in git repo
function parse_git_branch() {
  BRANCH=`git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\1/'`
  if [ ! "${BRANCH}" == "" ]
  then
    STAT=`parse_git_dirty`
    echo "(${BRANCH}${STAT})"
  else
    echo ""
  fi
}

# get current status of git repo
function parse_git_dirty {
  status=`git status 2>&1 | tee`
  dirty=`echo -n "${status}" 2> /dev/null | grep "modified:" &> /dev/null; echo "$?"`
  untracked=`echo -n "${status}" 2> /dev/null | grep "Untracked files" &> /dev/null; echo "$?"`
  ahead=`echo -n "${status}" 2> /dev/null | grep "Your branch is ahead of" &> /dev/null; echo "$?"`
  newfile=`echo -n "${status}" 2> /dev/null | grep "new file:" &> /dev/null; echo "$?"`
  renamed=`echo -n "${status}" 2> /dev/null | grep "renamed:" &> /dev/null; echo "$?"`
  deleted=`echo -n "${status}" 2> /dev/null | grep "deleted:" &> /dev/null; echo "$?"`
  bits=''
  if [ "${renamed}" == "0" ]; then
    # bits=">${bits}"
    bits="renamed${bits}"
  fi
  if [ "${ahead}" == "0" ]; then
    # bits="*${bits}"
    bits="ahead${bits}"
  fi
  if [ "${newfile}" == "0" ]; then
    # bits="+${bits}"
    bits="newfile${bits}"
  fi
  if [ "${untracked}" == "0" ]; then
    # bits="?${bits}"
    bits="untracked${bits}"
  fi
  if [ "${deleted}" == "0" ]; then
    # bits="x${bits}"
    bits="deleted${bits}"
  fi
  if [ "${dirty}" == "0" ]; then
    # bits="!${bits}"
    bits="dirty${bits}"
  fi
  if [ ! "${bits}" == "" ]; then
    echo " ${bits}"
  else
    echo ""
  fi
}

# user and ostname removed:
# export PS1="\[\e[36m\]\W\[\e[m\]\[\e[32m\]\`parse_git_branch\`\[\e[m\] $ "

# user and hostname included
export PS1="[\u@\h \W]\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "

########################################
# This will allow you to enter your credentials only once during the session, update to match your github user
########################################

# to cache creds:
git config --global credential.helper "cache --timeout=360000"
git config --global user.name "Fname Lname"
git config --global user.email user@email.com

########################################
# my personal welcome message
########################################

echo "welcome $USER to your interactive non login shell .bashrc"
```


<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->
> ## **_ Tips and Tricks _** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

- Backup monthly.

- Always keep two previous images.

- Upload the image to Google Drive or Microsift One Drive.

