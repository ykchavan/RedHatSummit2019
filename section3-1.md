# Configuring Key-Based Authentication

1.  If you have keys generated on the primary server, you need to add them to the target server, in the ~/.ssh/authorized_keys file. If you do not have keys, use the following command:
~~~
$ ssh-keygen
$ ssh-copy-id classroom.example.com
~~~

* Then, return to the user interface on the primary server, click the top right corner menu with the user name on it, choose **Authentication**, and enable the preloaded key.<br><br>
![alt text](files/images/key_auth_on.png "Key Auth")

* After you type in the IP when adding the new system to the Dashboard, change the Authentication type to Use available credentials.


<hr/>
<span style="font-size:10pt"><details>
  <summary>Show transcript</summary>
  <p>
  FIXME...
  </p>
</details></span>
