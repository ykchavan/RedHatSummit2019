# Create custom RHEL images using Image Builder
## Lab instructions

Presenters:
* Yogesh Chavan
* Nenad Peric
* Karan Rai

Table of Contents:

1. [ LAB Details ](#details)
2. [ Lab 1.1 - Install Image Builder ](#install)
3. [ Lab 1.2 - Create a Blueprint ](#create)
4. [ Lab 1.3 - Add packages to the Blueprint ](#add)
5. [ Lab 1.4 - Create Image ](#createimage)
6. [ Lab 1.5 - Test the new image ](#testimage)
7. [ Lab 2.1 - Customize the blueprint configuration file ](#custom)
8. [ Lab 2.2 - Test the new image with virt-install ](#testvirt)
9. [ Resources ](#resource)

<a name="details"></a>
# LAB Details


* You have a pre-installed Red Hat Enterprise Linux 8 system
~~~
[lab-user@bastion-LAB-GUID ~]$ hostname
bastion-LAB-GUID.rhpds.opentlc.com
~~~
Here  LAB-GUID  is the number provided to you on the 'Lab information' page

* Following packages are already installed:
  * Web Console (cockpit)
  * virt-viewer
  * virt-install


* Web console is enabled
  ~~~
  [root@bastion-LAB-GUID ~]# systemctl is-enabled cockpit.socket
  enabled
  ~~~
# To access the Red Hat Web Console
* Use hostname with port 9090
  ~~~
  https://bastion-LAB-GUID.rhpds.opentlc.com:9090
  ~~~
* Login as lab-user and password to-be-provided
* Check - "Reuse my password for privileged tasks"

  <a name="install"></a>
# Lab 1.1 - Install Image Builder

* On the web console go to the **terminal** tab
* Use sudo to become root
~~~
[lab-user@bastion-LAB-GUID ~]$ sudo -i
[root@bastion-LAB-GUID ~]#
~~~

* Install *Image Builder* with the CLI and the web console plugin:
~~~
[root@bastion-LAB-GUID ~]# yum install lorax lorax-composer composer-cli cockpit-composer
~~~

* Enable and start composer service
~~~
[root@bastion-LAB-GUID ~]# systemctl enable --now lorax-composer.socket
~~~

* Restart cockpit service to load newly installed plugin
~~~
[root@bastion-LAB-GUID ~]# systemctl restart cockpit.service
~~~

  **Note**: Restarting the web console will log you out, you need to relogin

* Now you should be able to see the "Image Builder" tab on left hand side of the Web Console.
<center><a href="ib1.png" target="_blank"><img src="ib1.png" alt="Image Builder"></a><br/>Click image to view at full size.</center>

<a name="create"></a>
# Lab 1.2 - Create a Blueprint

* On the Image Builder tab, click on **Create Blueprint** button on the top right corner.
* Give a name something like - summit2019
<center><a href="ib1.png" target="_blank"><img src="ib1.png" alt="Create Blueprint"></a><br/>Click image to view at full size.</center>

**Note:** Remember the Blueprint name, you will need it in the later section of this lab.

<a name="add"></a>
# Lab 1.3 - Add packages to the Blueprint

* On the *Edit Blueprint* page search the available packages in *Available Components* search box for "bison" package

* Click on the "+" icon to add the packages
* Add more packages if you like

<br>
<br>
<center><a href="ib2.png" target="_blank"><img src="ib2.png" alt="Add packages"></a><br/>Click image to view at full size.</center>

<a name="createimage"></a>
# Lab 1.4 - Create Image

* After adding the packages, click on you blueprint on the top left corner "summit2019"
* Verify the packages that you have added in the "Selected Components" table
* Next click on the **images** tab and click on **Create Image**
* Select the **Image Type** as **QEMU QCOW2 Image**(qcow2)


<br>
<br>
<center><a href="ib3.png" target="_blank"><img src="ib3.png" alt="Create Blueprint"></a><br/>Click image to view at full size.</center>


**Note** Creation of a new Image may take 5 to 10 minutes

<a name="testimage"></a>

# Lab 1.5 - Test the new image

On the terminal run:

* Get the GUID of the image
~~~
[root@bastion-LAB-GUID ~]# composer-cli compose list
99ed96cd-b783-4cad-838f-c8173e038431 FINISHED summit2019 0.0.2 qcow2                                                                                                                                 
~~~

* Login to the GUI of the server

* Test the image with virt-viewer
~~~
[root@bastion-LAB-GUID ~]# virt-install --name RHEL8Lab2 --memory 2048 --vcpus 2 --os-variant rhel8.0 --import --disk /var/lib/lorax/composer/results/<GUID number for that image>/disk.qcow2
~~~

<br>
<hr>
<a name="custom"></a>
<h1>LAB 2 - Customize the RHEL image using composer-cli</h1>

# Lab 2.1 - Customize the blueprint configuration file

* Download a copy of the blueprint configuration file from Image Builder

~~~
[root@bastion-LAB-GUID ~]# composer-cli blueprints save summit2019
~~~
* You will get a file **summit2019.toml**

* Append the following lines to the summit2019.toml file
~~~
[[customizations.user]]
name = "myuser"
password = “mypassword”
groups = ["users", "wheel"]
~~~

* Push the revised blueprint configuration file back to Image Builder
~~~
[root@bastion-LAB-GUID ~]# composer-cli blueprints push summit2019.toml
~~~

* Verify that your changes appear in the configuration file
~~~
[root@bastion-LAB-GUID ~]# composer-cli blueprints show summit2019
~~~


  <a name="testvirt"></a>

# Lab 2.2 - Test the new image with virt-install

* Get GUID of the image
~~~
[root@bastion-LAB-GUID ~]# composer-cli compose list
~~~

* Run this command to test the image with *virt-viewer*

~~~
[root@bastion-LAB-GUID ~]# virt-install --name RHEL8Lab2 --memory 2048 --vcpus 2 --os-variant rhel8.0 --import --disk /var/lib/lorax/composer/results/<GUID number for that image>/disk.qcow2
~~~

* Verify the VM

  * Login as myuser and password as mypassword
  * Run **id** command to verify if myuser is a member of *users* and *wheel* group
  * Verify that the package you added in the blueprint earlier are installed in the VM
  ~~~
  [root@vm ~]# rpm -qa | grep -i <package-name>
  ~~~

<a name="resource"></a>
# Resources

[Building custom system images with composer)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/installation_guide/chap-composer-x86)

[Building custom system images with Composer](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8-beta/html/installing_and_deploying_rhel/building-custom-system-images-with-composer_graphical-installation)

[Download the Presentation](ImageBuilder-Summit.pdf)
