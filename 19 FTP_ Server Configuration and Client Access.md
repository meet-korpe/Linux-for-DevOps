# FTP Server Configuration and Client Access

## 1. FTP Fundamentals

**FTP (File Transfer Protocol)** is a standard network protocol used for the transfer of files between a client and a server on a computer network.

- **Usage:** Primarily used for **Internet File Transfer**.
- **Protocol Layer:** Operates on **TCP Protocol Layer 4**.
- **Port:** The standard port for FTP is **21**.
- **Authentication:** The service typically asks for a **username and password** to grant access.

## 2. FTP Service Packages

There are several software packages available to provide FTP services:

1. **VSFTPD (Very Secure FTP Daemon):** A popular, secure server package that uses **Port 21**.
2. **ProFTP:** Another server option using **Port 21**.
3. **FileZilla:** Both a client and server software using **Port 21**.
4. **SFTP (Secure File Transfer Protocol):** While similar in purpose, it uses the **SSH protocol** on **Port 22** for secure transfers.

## 3. Server-Side Configuration (VSFTPD)

The lecture demonstrated how to set up a VSFTPD server on a Linux system (IP: 192.168.1.181).

### A. Installation and Verification

- **Check Installation:** `rpm -qa | grep -i vsftpd`
- **Install Package:** `yum install vsftpd -y`
- **Configuration Directory:** Located at **/etc/vsftpd/**, containing critical files like vsftpd.conf, ftpusers, and user_list

### B. Service Management

- **Start Service:** `systemctl start vsftpd`
- **Enable at Boot:** `systemctl enable vsftpd`
- **Check Status:** `systemctl status vsftpd` or `systemctl is-active vsftpd`
- **Disable Firewall:** For testing purposes, the firewall may need to be stopped to allow traffic: `systemctl stop firewalld`
- FireWall Configuration:

```bash
firewall-cmd --permanent --add-service=ftp
firewall-cmd --permanent --add-service=ssh
firewall-cmd --reload
firewall-cmd --list-all
```

### C. Data Storage

- The default directory for files shared via FTP is **/var/ftp/**
- Files placed in this directory (e.g., using `touch /var/ftp/java`) will be visible to connected clients.

## 4. Client-Side Access

Clients can connect to the FTP server using various methods and tools.

- **Available Clients:**
  - Web browsers.
  - Command-line FTP clients.
  - Third-party tools: **lftp, Kasabalanca, FileZilla, and gftp**.

### Step-by-Step: How to Access the Server

- **Test Connectivity:** Ensure the server is reachable by running `ping 192.168.1.181` from the client.
- **Verify Port Access:** Check if port 21 is open on the server using **telnet**: `telnet 192.168.1.181`
- **Access via Browser:** Open a web browser and enter the URL: **ftp://192.168.1.181**
- **Download Files (CLI):** Use the wget utility to download specific files from the server:
  - Example: `wget ftp://192.168.1.181/java`
  - Example: `wget ftp://192.168.1.181/file1`

### Firewall Configuration

```bash
firewall-cmd --permanent --add-service=ftp
firewall-cmd --permanent --add-service=ssh
firewall-cmd --reload
firewall-cmd --list-all
```

- **Allow FTP:** `firewall-cmd --permanent --add-port=21/tcp`
- **Allow SFTP/SSH:** `firewall-cmd --permanent --add-port=22/tcp`
- **Apply Changes:** `firewall-cmd --reload`

