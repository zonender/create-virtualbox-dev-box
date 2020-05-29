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

- Scroll down to the Graphical Desktop Installation, or download it from [here.](https://sourceforge.net/projects/linuxvmimages/files/VirtualBox/C/7/CentOS_7.7.1908_VBG.zip/download)

- Unzip the ova image file.

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

- Under shared clipboard select bidirectional.

- Click on system.

- Click on the Motherboard tab.

- Under base memory type 2048 MB (preferably 4096 MB)

- Under pointing device select USB Tablet.

- Click on processor.

- Under processors slide to two processors.

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

