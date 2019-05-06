<audio controls style="width: 700px; display: block" src="files/audio/section3.ogg"></audio>

# Add Secondary Servers

A secondary Cockpit server must have:
* The *cockpit* packages installed
* An SSH server running and available over port 22
* SSH configured to support password or key-based authentication

**To add a new secondary server:**

1. From the *Dashboard* tab, next to the system name, click the plus (+) button.
2. Enter the IP or host name of the server you're adding, and select a color label for it.
3. Click **Add**.

<center><img src="files/images/add_host.png" alt="Add a secondary system"></center>

4. When prompted, sign in to the system with a user name and password:

<center><img src="files/images/add_host_passwd.png" alt="Provide credentials for the secondary system"></center>

In your lab environment, add **classroom.example.com** to your Cockpit interface.

<hr/>
<span style="font-size:10pt"><details>
  <summary>Show transcript</summary>
  <p>
  A secondary Cockpit server must have the "cockpit" packages installed,
  SSH server running and available over port 22, and SSH configured to
  support password or key-based authentication. The steps here show how to
  add a new secondary server in the Cockpit interface. In your lab environment,
  use this procedure to add classroom.example.com to your lab's Cockpit
  Dashboard. See the lab environment details at the beginning of this training
  for the host name, IP, and user credentials for the "classroom" system.
  </p>
</details></span>
