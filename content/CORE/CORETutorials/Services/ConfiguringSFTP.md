---
title: "Configuring SFTP"
weight: 20
---


## Configuring SFTP Service

SSH File Transfer Protocol (SFTP), is available by enabling SSH remote access to the TrueNAS system.
SFTP is more secure than standard FTP as it applies SSL encryption on all transfers by default.

Go to **Services**, find the **SSH** entry, and click the <i class="material-icons" aria-hidden="true" title="Configure">edit</i>.

![ServicesSSHOptions](/images/CORE/12.0/ServicesSSHOptions.png "SSH Options")

Set **Allow Password Authentication** and decide if **Log in as Root with Password** is needed. 
SSH with root is a security vulnerability as it allows full remote control over the NAS with a terminal, not just SFTP transfer access. 
Review the remaining options and configure according to your environment or security needs.

### SSH Service Options

Use the **SSH** screen to configure the system for SFTP. See [SSH Screen]({{< relref "/CORE/UIReference/Services/SSHScreen.md" >}}) for information on SSH screen settings.

### SFTP Connections

Similar to the FTP setup, open FileZilla or another FTP client, or command line.
This example uses FileZilla.
Using FileZilla, enter **SFTP://*TrueNAS IP***, *username*, *password*, and port **22** to connect. Where *TrueNAS IP* is the IP address for your system, and *username* and *password* are those you use to connect to the FTP client. Or enter **SFTP://'TrueNAS IP'**, *'username'*, *'password'*, and port **22** to connect.

{{< hint warning >}}
SFTP does not have chroot locking. 
While chroot is not 100% secure, the lack of chroot allows users to easily move up to the root directory and view internal system information. 
If this level of access is a concern, FTP with TLS may be the more secure choice.
{{< /hint >}}

### SFTP in a TrueNAS Jail

Another way to allow SFTP access without granting read access to other areas of the NAS itself is to set up a jail and enable SSH.

{{< expand "Setting up a Jail for SFTP" "v" >}}
Go to **Jails > Add**.
Provide a name for the jail and pick a target FreeBSD image.
This example uses 11.3.

Set the networking options to either DHCP or a static IP and confirm to create.

![JailsAddNetworking](/images/CORE/12.0/JailsAddNetworking.png "Jail Networking Options")

After the jail is created, click the expand icon **>** on the right-hand side of the jail to open it.
Click **START** and open **SHELL**.

Similar to the initial FTP setup, create a user in the jail.
Enter command `adduser` and follow the prompts including the password and home directory location.
When complete, the jail asks to confirm the credentials.

![JailsShellUserAdd](/images/CORE/12.0/JailsShellUserAdd.png "Adding a new user to a jail")

Enable SSH by editing the <file>/etc/rc.conf</file> file.
Type command `vi /etc/rc.conf` or `ee /etc/rc.conf` depending on preference, add `sshd_enable = "YES"` to the file, save, and exit.
Type command `service sshd enabled` to enable the service (enabled vs start indicates whether sshd starts one time or on every reboot).

![JailsShellEditRCConf](/images/CORE/12.0/JailsShellEditRCConf.png "Enabling SSH in a jail")

Using an FTP client, such as FileZilla, log in with the jail IP address and user credentials. Like with SSH on TrueNAS, browsing to other folders and locations beyond the user home directory is possible, but unlike running on TrueNAS directly, only the components of the jail are available.

![FilezillaJailConnectSFTP](/images/CORE/FilezillaJailConnectSFTP.png "Filezilla SFTP Connect to TrueNAS Jail")
{{< /expand >}}

## Additional Information

[SSH Screen]({{< relref "/CORE/UIReference/Services/SSHScreen.md" >}})