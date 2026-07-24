# Linux Filesystem Architecture and Persistence Management

Based on the provided source material from "7.pdf," here are the detailed notes on filesystem fundamentals, the concept of data persistence through remounting, and specialized storage tools.

## 1. Filesystem Fundamentals

The primary purpose of a filesystem is to organize, control, and manage data on a storage device.

- **Key Components**:
  - **Inodes**: Store metadata about files.
  - **Superblocks**: Contain critical information about the filesystem's structure and status.
  - **Blocks**: The actual units where data is stored.
  - **Inode Table**: A list maintaining all inodes within the filesystem.
  - **Filesystem Types**: Common types include **ext2, ext3, ext4, xfs, btrfs, cifs, zfs, nfs, hdfs, and raiserfs**.

- **Creating a Filesystem**: The process of "formatting" is used to create or recreate a filesystem on a partition. For example, `mkfs.ext4 /dev/sdc1` writes the inode tables and superblocks to the disk.

## 2. Remounting and Data Persistence

A critical concept in Linux storage is that data resides on the physical partition, not the directory (mount point) it is attached to. The sources demonstrate this through a step-by-step workflow:

- **Initial Mounting**: A formatted partition (e.g., /dev/sdc1) is mounted to a directory like /dir1 using `mount /dev/sdc1 /dir1`.
- **Data Creation**: Files created while the partition is mounted (e.g., file1 and file2) are physically stored on /dev/sdc1.
- **Unmounting**: When you run `umount /dev/sdc1`, the directory /dir1 appears empty. The data is not lost; it is simply no longer accessible through that specific mount point.
- **Remounting Elsewhere**: If you create a new directory (/dir2) and mount the same partition there (`mount /dev/sdc1 /dir2`), the original files (file1, file2) immediately reappear in the new location. This proves that data remains intact on the storage device regardless of where or if it is currently mounted.

## 3. Specialized Storage Tools

The sources categorize specialized tools used for maintaining or recovering data and managing hardware at a low level.

- **Data Recovery Tools**: Used to retrieve lost or deleted information.
  - `diskdrill`, `recova`, `r studio`, `photo rec`

- **Lower-Level Formatting & Erasure Tools**: Used for secure deletion or hardware-level preparation.
  - **DBAN**: Often used for total disk wiping.
  - **shred**: A command used to securely overwrite files so they cannot be recovered.
  - **sea tools**: Specialized diagnostic and formatting software for Seagate drives.
  - **hdd low level format**: Tools designed for deep formatting of hard drives.
