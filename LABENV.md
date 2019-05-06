<audio controls style="width: 700px; display: block" src="files/audio/labenv.ogg"></audio>

# Lab Environment

Successful completion for this training includes hands-on lab activities hosted in a cloud-based lab environment.

> #### Note::
>
> **Red Hat Partners** do NOT follow the instructions given on this page.
> Instructions for launching and managing your learning environment are available at [http://www.opentlc.com/ssh.html](http://www.opentlc.com/ssh.html).
> For this module, use the OPENTLC catalog with the name **cee-rl-802-v2.0**

<br/>
<p style="background-color:#DEDEDE; padding:2px 10px;"><b>SET UP SSH KEYS</b></p>

Public SSH keys are configured for the root user for all machines to allow external SSH access.

To install the private key pair on your local workstation, first download the key using this command:
~~~
$ curl --create-dirs -o ~/.ssh/\#1 training.gsslab.rdu2.redhat.com/{gssTrng0_rsa}
~~~

Then, modify permissions for the key:
~~~
$ chmod 600 ~/.ssh/gss*
~~~

<br/>
<p style="background-color:#DEDEDE; padding:2px 10px;"><b>LAUNCH</b></p>

Use *ravshello* as described in [DOC-987131](https://mojo.redhat.com/docs/DOC-987131) with this blueprint: **cee-rl-802-v2.0**<br/>
**NOTE:** The environment may take **up to 10 minutes** to reach a "STARTED" state.

<br/>
<p style="background-color:#DEDEDE; padding:2px 10px;"><b>SYSTEM INFO</b></p>

| System | IP | Credentials | Description |
| --- | --- | --- | --- |
| servera.example.com | 172.25.250.10 | CLI: root/redhat web UI: root/RedHat1! | Server to be used for the RHEL 8 web console|

<br/>
<p style="background-color:#DEDEDE; padding:2px 10px;"><b>COMMAND LINE ACCESS (SSH)</b></p>

(1) Change to the application directory in *ravshello*.

(2) Enter the **query_status** command every minute or so to check whether the application shows being in a "STARTED" state.

(3) After the app shows as "STARTED", locate the *ssh* command from that output for the system indicated in your lab activity.

(4) Enter that command into a new terminal, and proceed as instructed in the lab activity.

<br/>
<p style="background-color:#DEDEDE; padding:2px 10px;"><b>CONSOLE ACCESS</b></p>

(1) Change to the application directory in *ravshello*.
~~~
cd /apps
new cee-rl-802-v2.0
~~~

(2) Enter the **query_status** command.

(3) After all systems are in a "STARTED" state in this status output, locate the URL in that output for the system indicated in your lab activity.

(4) Use that URL in your web browser to open the console for that system. This URL rotates after a few minutes, so if you close the console, run *query_status* again to get the current URL.

<br/>
<p style="background-color:#DEDEDE; padding:2px 10px;"><b>WEB CONSOLE IP & PORT</b></p>

While in ravshello, note of the public IP and port on *servera.example.com*. That port is mapped to the web console port on *servera*. You will need this information later to access the RHEL 8 web console from a web browser on your local system.

In this example, it is **35.244.24.166** and port **10001**:
~~~
servera.example.com
     State:            STARTED
     Hostnames:        servera.example.com
     NIC nic1
     Internal IP:    172.25.250.10
     PubIP DNAT:     35.244.24.166 (serveraexamplecom-kkraiceerl802v100-vgfj60oa.srv.ravcloud.com)
     External Svc:   cockpit port 10001/TCP maps to internal port 9091
~~~

**NOTE:** The URLs and public IPs will be different for every application.

<br/>
<p style="background-color:#DEDEDE; padding:2px 10px;"><b>SSH access to classroom</b></p>

To log in to *servera.example.com* using SSH :
~~~
$ ssh -i ~/.ssh/gssTrng0_rsa -p 10003 root@classroomexampleco-kkraiceerl802v100-mhcm9ckg.srv.ravcloud.com
[root@servera ~]#
~~~

If you need more information then watch this [video](labvideo.md).
<hr/>
<span style="font-size:smaller;"><details>
  <summary>Show transcript</summary>
  <p>
  Successful completion for this training includes hands-on lab activities.
  Use the information on this page to launch the cloud-based lab environment,
  and to access it in the ways described here. Pay particular attention to the
  web console IP and port section as you will use your local web browser to
  access this during the labs.
  </p>
</details></span>
