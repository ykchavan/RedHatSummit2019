# LAB Details

* You have a pre-installed Red Hat Enterprise Linux 8 system
~~~
[lab-user@bastion-GUID ~]# hostname
bastion-GUID.rhpds.opentlc.com
~~~


* You can use sudo to become root
~~~
[lab-user@bastion-GUID ~]# sudo -i
[root@bastion-GUID ~]#
~~~

* Following packages are already installed:
  * Web Console (cockpit)
  * virt-viewer
  * virt-install


* Web console is enabled
  ~~~
  [root@bastion-GUID ~]# systemctl enable cockpit.socket
  ~~~

# To access the Web Console
* Use hostname or IP with port 9090
  * Sample

  ~~~
  https://bastion-GUID.rhpds.opentlc.com:9090
  or
  https://<server IP>:9090
  ~~~
