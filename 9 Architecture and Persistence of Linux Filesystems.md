# 9. Architecture and Persistence of Linux Filesystems

## Deep About Filesystem

- **File System:** It **organises, controls, and manages data**. A file system is essentially an **index of your data**.
- Each partition has its own unique file system.
- **Components:** A file system is a **collection of metadata** (the "bio-data" or properties of stored data, such as size and permissions). It specifically includes **blocks, inodes, inode tables, superblocks, and mount information**.

- **Inodes (Index Nodes):**
  - The inode number acts as a **"roll number" for your data**.
  - It is a **unique number** assigned to each file and folder.
  - The inode contains information like **ownership, size, access time, modify time, and change time**.

- **How to check:**
  - Use `ls -i [filename]` to see the index number of a specific file or directory.
  - Use `df -i` to view the overall status and details of inodes on the system.

## How to Check File System Without Mounted Partition

To inspect the details of a file system (such as `/dev/sdd1`) without having to mount it, use the following commands:

- `dumpe2fs /dev/sdd1`
- `tune2fs -l /dev/sdd1`

## Permanent Mounting and /etc/fstab

- Standard partition mounting is **temporary** and will be lost after a shutdown or restart.
- To mount partitions **permanently**, you must add an entry to **/etc/fstab**, which the system reads during the boot process.
- The /etc/fstab file is **critical**; a wrong entry (like a typo in the device or mount point) can force the system into **maintenance mode**.
- **How to edit:** Use `vim /etc/fstab` to add your partition details.
- **Structure of an entry:**
  - **Example:** `/dev/sdd1 /jet ext4 defaults 0 0`
- The **defaults** option includes several settings like read-write access, suid, and auto-mounting.
- **Verification:** After editing, run `mount -a` to mount all filesystems listed in fstab, and use `df -h` to verify they are active.

## Dump Backup Utility (5th Field)

This field determines if the partition should be backed up using the dump utility:

- **0:** Do **not** backup using dump.
- **1:** **Include** this partition in dump backups.

## Fsck Field (6th Field)

This field determines the order in which the system checks filesystems for errors during boot:

- **0:** **Do not check** the filesystem.
- **1:** Check the **root (/) filesystem first**.
- **2:** Check this partition **after** the root filesystem has been checked.

