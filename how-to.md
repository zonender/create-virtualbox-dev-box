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
> #### **_Option 1 - Download a pre-configured VirtualBox (VB) image (ova file)_**
<!-- ========================================================== -->

- Install the latest VirtualBox version from: https://www.virtualbox.org/ 

- Go to: https://www.linuxvmimages.com/

- Locate the Centos 7 VB image, or go to: https://www.linuxvmimages.com/images/centos-7/

IMPORTANT: please take not of the username and password located under the image page, it is usually:

username: centos
password: centos

- Scroll down to the Graphical Desktop Installation, or download it from [here.](https://sourceforge.net/projects/linuxvmimages/files/VirtualBox/C/7/CentOS_7.7.1908_VBG.zip/download)

- Unzip the ova image file.

- On the host desktop create a folder called "sharedwithvb", for example, this folder will be shared between the VM and the host.

- open VB.

- Go to: File and click on Import Appliance

- Browse to the location of the ova file.

- Change the name as desired.

- Under Mac Address Policy select Create New...

- Uncheck Import Hard Drive as VDI.

- Click on Import.

- Click on Agree.

- After the import completes, select the VM you just imported to highlight it.

- Click on settings.

- Click on General

- Go to the Advanced tab.

- Under shared clipboard select bidirectional.

- Under Drag n Drop select bidirectional.

- Click on system on the left panel

- Click on the Motherboard tab.

- Under base memory type 2048 MB (preferably 4096 MB)

- Under pointing device select USB Tablet.

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

- Once the VM starts, To Adjust the screen size and on the menu bar go to View then go to Virtual Screen 1, then select auto scaled output or the desired percentage.

NOTE: after every screen scale change restore the VM window then maximize it.

- switch to root user:

```bash
sudo su -
```

- Create your user:

```bash
useradd myuser
```

- Set your password:

```bash
passwd myuser
```

- Give your user admin rights

```bash
usermod -a -G wheel myuser
```

- update the system:

```bash
yum update -y
```

Allow your user to access the shared folder:

```bash
usermod -a -G vboxsf myuser
```

Allow your user to use sudo without a password by adding this line to the sudoers file:

Open the sudoers file by running:

```bash
visudo
```

scroll to the very end and click the i button.

and add this line at the very end:

```
myuser ALL=(ALL) NOPASSWD: ALL
```

save the file by hitting the escape button, then hitting the colon button then hit the x button, finally hit enter.

Then Reboot:

```bash
reboot now
```

- login using your user:

- delete the old user:

```bash
sudo userdel -r centos
```

- Update guest additions, by clicking on the Devices menu on the menu bar of the VM window, then click on Insert Guest Additions CD.

- A popup window will appear, click on run, you will be prompted to enter your user password.

- Wait untill you are asked to hit enter to close the window, then reboot.

- 




<!-- ========================================================== -->
> #### **_Option 2 - Start from scratch_**
<!-- ========================================================== -->



 - Go to https://wiki.centos.org/Download

 - 




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
> ## **_ Install important dev apps _** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

python3.7

python3.8

pipenv

aws cli

nodejs

docker

ansible

terraform

tfenv

linuxbrew

pipenv

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
> ## **_ Tips and Tricks _** 
<!-- 
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
#>>>>>>>>>>>>>>>>>>>>>>>>>>>><<<<<<<<<<<<<<<<<<<<<<<<<<<
 -->

- Backup monthly.

- Always keep two previous images.

- Upload the image to Google Drive or Microsift One Drive.

