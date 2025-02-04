---
---

**Path**

| Name | Description |
|------|-------------|
| **Directory** | Browse to an existing directory to use for storage. Some devices can require a specific directory name. Consult the documentation for that device to see if there are any restrictions. Click the <span class="material-icons-round">arrow_right</span> to the left of **/mnt** to open a list of directories. |

**Connection**

| Name | Description |
|------|-------------|
| **Host** | The default host to use for TFTP transfers. Enter an IP address. For example, *192.0.2.1* or in **Shell** `192.0.2.1` |
| **Port** | The UDP port number that listens for TFTP requests. For example, *8050* or in **Shell** `8050`. |
| Username | Select the account to use for TFTP requests from the dropdown list of options that includes but not limted to **root**, **daemon**, **operator**, **nobody** and all the other usernames on the system. This account must have permission to the what is specified in **Directory**. |

**Access**

| Name | Description |
|------|-------------|
| **File Permissions** | Adjust the file permissions using the **Read**, **Write** and **Execute** permissions for the **User** and **Group** checkboxes. Select all that apply. |
| **Allow New Files** | Select when network devices need to send files to the system. |

**Other Options**

| Name | Description |
|------|-------------|
| **Auxiliary Parameters** | Add more options from [tftpd](https://manpages.debian.org/bullseye/tftpd-hpa/tftpd.8.en.html). Add one option on each line. |