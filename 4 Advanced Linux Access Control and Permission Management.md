# Advanced Linux Access Control and Permission Management

These notes are based on numeric permissions, advanced Access Control Lists (ACL), special permissions (SUID, SGID, Sticky Bit), and sudoer configuration.

## 1. Octal (Numeric) Permission Mode

In addition to symbolic mode (u+x), Linux uses a numeric system to set permissions. Each permission type is assigned a specific number:

| Permission | Value |
|---|---|
| `r` (Read) | 4 |
| `w` (Write) | 2 |
| `x` (Execute) | 1 |

To set permissions, you sum the numbers for each category (Owner, Group, Others). For example:

- `777`: Full permissions for everyone (4+2+1=7)
- `666`: Read and write for everyone (4+2=6)
- `755`: Owner has full access; Group and Others have read and execute access
- `644`: Owner has read/write; Group and Others have read-only access
- `700`: Full access for the owner; no access for anyone else
- `000`: No permissions for anyone

## 2. Access Control Lists (ACL)

ACLs provide a more granular way to manage permissions, allowing you to grant access to specific users or groups without changing the primary owner or group of the file.

- Viewing ACLs: Use `getfacl [filename]` to view the extended permissions of a file
- Setting/Modifying ACLs: Use `setfacl -m` followed by the user or group designation and permissions
- User Example: `setfacl -m u:chintu:rw file2` (Grants user "chintu" read and write access to "file2")
- Group Example: `setfacl -m g:market:rx file2` (Grants the "market" group read and execute access)
- Removing Specific ACL entries: Use `setfacl -x` followed by the user or group
- Example: `setfacl -x u:chintu file2`
- Removing ALL ACL entries: Use `setfacl -b [filename]` to clear all extended permissions and return to standard mode

## 3. Advanced Special Permissions

These special bits change how files and directories behave for different users.

### SUID (Set User ID)

- Set with: `chmod u+s [filename]`
- Function: If the SUID bit is set on an executable file, any user running that file will gain the privileges of the file's owner (often root)
- Example: Setting SUID on `/sbin/fdisk` allows regular users to run the disk management tool with root privileges

### SGID (Set Group ID)

- Set with: `chmod g+s [directory]`
- Function: When set on a parent folder, any new files or directories created inside it will automatically inherit the group of the parent folder, rather than the primary group of the user who created them

### Sticky Bit

- Set with: `chmod o+t [directory]`
- Function: When set on a directory, only the owner of a file (or the root user) can delete that file, even if other users have write permissions to the directory

## 4. Sudoers and Command Delegation

The `/etc/sudoers` file controls which users can run administrative commands.

- Editing the File: Always use the command `visudo` to edit this file, as it checks for syntax errors before saving
- Syntax for User Permissions:

```bash
chintu ALL=/sbin/fdisk
%market ALL=/sbin/fdisk
NOPASSWD: ALL
```

- Basic Command Access: `chintu ALL=/sbin/fdisk` (Allows user "chintu" to run fdisk as root)
- Group Access: `%market ALL=/sbin/fdisk` (Allows all members of the "market" group to run fdisk)
- No Password Requirement: Use `NOPASSWD: ALL` to allow the user to run commands without being prompted for their password
- Usage: Once configured, a user runs the delegated command using `sudo`, such as `sudo fdisk -l`

