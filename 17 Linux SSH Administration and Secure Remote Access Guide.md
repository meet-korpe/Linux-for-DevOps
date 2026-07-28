# Linux SSH Administration and Secure Remote Access Guide

## SSH (Secure Shell) Fundamentals and Configuration

**SSH (Secure Shell)** is a protocol used for **secure remote access** to Linux servers over a network.

- **Default Port:** 22.
- **Protocol:** Uses **TCP** (Transmission Control Protocol).
- **Service Name:** The background daemon is **sshd**.
- **Remote Clients:** Common third-party tools used to connect to Linux servers include **Putty** and **MobaXterm**.

## Step-by-Step Guide: How to use SSH

To connect from a client machine to a remote Linux server, follow these steps as demonstrated in the sources:

- **Verify Network Connectivity:** Before attempting to connect, ensure the remote server is reachable using the ping command.
  - Example: `ping 192.168.1.181`
- **Check Service Status:** On the target server, ensure the SSH service is active and listening on port 22.
  - Command: `systemctl status sshd`
  - Verification: `netstat -tulnp | grep -i 22`
- **Initiate Connection:** Use the ssh command followed by the username and the IP address of the remote server.
  - Command: `ssh root@192.168.1.181`
- **Accept ECDSA Key Fingerprint:** If this is your first time connecting, the system will ask if you want to continue. Type **yes** to add the server to your known_hosts file.
- **Enter Password:** Provide the password for the user account you are logging into.
- **Execute Commands Remotely:** Once logged in, you can run commands (like `df -h` to check disk space) as if you were sitting at the physical machine.
- **Terminate Session:** Type **exit** or **logout** to close the remote connection and return to your local terminal.

## Advanced SSH Management and Security

The primary configuration file for SSH is located at **/etc/ssh/sshd_config**. Modifying this file allows for granular security control:

### Security Configurations

| Setting | Effect |
|---|---|
| `PermitRootLogin no` | Disables direct root login for better security. |
| `AllowUsers [name]` | Creates a whitelist (e.g., AllowUsers ramu shamu tom) so only specific users can connect. |
| `DenyUsers [name]` | Specifically blocks certain users from accessing the server. |
| `AllowGroups / DenyGroups` | Restricts access based on group membership (e.g., AllowGroups cartoon). |
| `PubkeyAuthentication yes` | Enables the use of SSH keys for authentication. |
| `LoginGraceTime 2m` | Sets the time window a user has to authenticate before being disconnected. |

### Applying Changes

- **Testing Syntax:** Before restarting the service, use `sshd -t` to check the configuration file for errors.
- **Restarting:** Use `systemctl restart sshd` to apply any changes made to the configuration file.

## Troubleshooting Connections

- **Port Testing:** Use `telnet [IP] 22` to check if the SSH port is open and accepting connections.
- **Error: "No route to host"**: This often indicates an incorrect IP address or a firewall blocking the connection.
- **Installation:** If the service is missing, it can be installed via `yum install openssh-server -y`.

