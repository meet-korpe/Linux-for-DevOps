# Linux File Permissions and Ownership Management

Based on the provided source material, here are in-depth notes on **Linux File Permissions** and **Ownership and Group Management**.

## 1. Linux File Permissions

Permissions in Linux determine what actions different users can perform on a file or directory. These are categorized into three types and assigned to three different entities.

### Permission Types

| Type | Meaning |
|---|---|
| `r` (Read) | Allows viewing the content of a file |
| `w` (Write) | Allows making changes, editing, or saving the file |
| `x` (Execute) | Allows running the file as a program or script |

### Permission Entities

| Entity | Meaning |
|---|---|
| `u` (Owner/User) | The individual who owns the file |
| `g` (Group) | A collection of users with shared access |
| `o` (Others) | Every other user on the system who is not the owner or part of the group |

### The `chmod` Command (Change Modification)

The `chmod` command is used to add, remove, or set specific permissions.

#### Adding/Removing Permissions (Symbolic Mode)

```bash
chmod u+w file1
chmod u-x file1
chmod g+wx file1
chmod o-rwx file1
chmod a+x file2
```

- `chmod u+w file1`: Adds **write** permission for the **owner**
- `chmod u-x file1`: Removes **execute** permission for the **owner**
- `chmod g+wx file1`: Adds **write and execute** permissions for the **group**
- `chmod o-rwx file1`: Removes **read, write, and execute** permissions for **others**
- `chmod a+x file2`: Adds **execute** permission to **all** (owner, group, and others)

#### Setting Specific Permissions

```bash
chmod ugo=rwx file2
chmod u=rwx,g=wx,o=x file2
chmod ugo=r file2
```

- `chmod ugo=rwx file2`: Grants **full permissions** (read, write, execute) to everyone
- `chmod u=rwx,g=wx,o=x file2`: Assigns different specific permissions to each entity in one command
- `chmod ugo=r file2`: Sets the file to **read-only** for everyone

## 2. Ownership Management

Ownership defines which specific user has primary control over a file.

### The `chown` Command (Change Owner)

This command is used to transfer file ownership to a different user.

```bash
chown [username] [filename]
```

- Example: `chown ramu file2` changes the owner of "file2" to the user "ramu"

## 3. Group Management

Groups are used to manage permissions for multiple users simultaneously.

### Creating and Viewing Groups

- Add a Group: `groupadd [groupname]` (e.g., `groupadd cartoon`)
- View Groups: Groups are stored in the `/etc/group` file
- Use `cat /etc/group` to see all groups
- Use `cat /etc/group | grep -i [groupname]` to find a specific group

### Managing Group Membership (`usermod`)

The `usermod` command modifies a user's account, including their group assignments.

- Assigning a Group: `usermod -G cartoon tom` assigns the user "tom" to the "cartoon" group
- Appending a Group: `usermod -aG market tom` appends the "market" group to the user "tom" without removing them from their existing groups

### Changing File Group Ownership (`chgrp`)

The `chgrp` command changes which group is associated with a file.

```bash
chgrp [groupname] [filename]
```

- Example: `chgrp cartoon file2` changes the group ownership of "file2" to the "cartoon" group

### Checking User Identity

- `id` command: Displays the UID (User ID), GID (Group ID), and all groups a user belongs to (e.g., `id jerry`)

