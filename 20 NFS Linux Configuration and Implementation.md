# NFS Linux Configuration and Implementation

## 1. NFS (Network File System) Fundamentals

**NFS** is a network sharing protocol used specifically for **Linux-to-Linux file sharing**. It is considered a **homogeneous (homo)** protocol because it connects similar operating systems.

- **Default Port:** **2049**
- **Supporting Service:** It relies on the **rpcbind.service** to function

## 2. Server-Side Configuration

The server is the machine that "exports" or shares its directories with others on the network.

### A. Installation and Service Management

- **Installation:** Use yum install rpcbind.service to ensure the necessary remote procedure call service is available.

```bash
yum install -y nfs-utils rpcbind
yum install rpcbind.service
```

- **Start Services:**

```bash
systemctl start nfs
systemctl start rpcbind.service
```

- **Enable at Boot:** systemctl enable nfs ensures the service starts automatically when the server reboots.

```bash
systemctl enable nfs
```

- **Verification:** Use `netstat -tulnp | grep -i 2049` to confirm the server is actively listening on the NFS port.

```bash
netstat -tulnp | grep -i 2049
```

### B. Exporting Directories (/etc/exports)

To share a folder, you must define it in the **/etc/exports** configuration file.

- **Editing the file:** Use `vi /etc/exports`
- **Entry Syntax:** `[directory_path] [client_IP_or_*]([options])`.
- **Example:** `/opt/resume *(sync)` — Shares the "resume" folder with **all hosts (*)** and uses the **sync** option to ensure data is written to disk immediately.
- **Example:** `/opt/tomcat (ro,sync)` — Shares the folder as **read-only (ro)**.
- **Applying Changes:** After editing the file, run `exportfs -rv` to reload the configuration without restarting the entire service.

## 3. Client-Side Configuration

The client is the machine that "mounts" the shared directory from the server to access its files.

### A. Testing Connectivity

Before mounting, the client must verify it can reach the server:

1. **Ping:** `ping 192.168.1.181` (Tests general network reachability).
2. **Telnet:** `telnet 192.168.1.181 2049` (Tests if the specific NFS port is open).
3. **Showmount:** `showmount -e 192.168.1.181` (Displays the list of directories the server is currently exporting).

### B. Mounting the Remote Directory

- **Create a Mount Point:** Create a local directory where the remote files will appear.

```bash
mkdir /myresume
```

- **Mount the Share:** Link the server's exported folder to your local mount point.

```bash
mount 192.168.1.181:/opt/resume /myresume
```

- **Verify:** Use **df -h** to see the new network drive in your filesystem list

## 4. Troubleshooting Summary

- **Firewall:** If connections fail, you may need to stop the firewall on the server using `systemctl stop firewalld` for testing
- **Reloading:** Always use `exportfs -rv` on the server after making any changes to shared folders.
- **IP Information:** Use ip r l to check your current IP and routing configuration if you cannot reach the server.

