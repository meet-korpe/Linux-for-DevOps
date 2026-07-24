# Linux Storage Management and Disk Partitioning Workflow

## 1. Storage Hardware Fundamentals

Linux represents hardware devices as files (e.g., in /dev/). Understanding the physical media is the first step in storage management.

- **Hard Disk Types**:
  - **HDD (Hard Disk Drive)**: Uses a rotating spindle. Common interfaces include **SATA, SAS, SCSI, PATA, and AATA**.
  - **SSD (Solid State Disk)**: No moving parts. Faster IOPS (Input/Output Operations Per Second) and data transfer speeds. Types include **SSD 2.5, M.2, NVME, and PCI Express 5**.

- **Data Storage Levels**:
  - **Block Level Data**: Direct access to the storage hardware (e.g., /dev/sda, /dev/sdb). This is used by databases like **MySQL, Oracle, and MS SQL**.
  - **File Level Data**: Access through a network or file system (e.g., **NFS, Samba, or File Servers**).

## 2. Identifying and Scanning for Storage

When new storage is added to a running system (like a virtual machine), Linux may not see it immediately.

- **List Block Devices**: Use lsblk to view all currently recognized disks and their partitions.
- **Scanning for New Disks**: To discover a newly added hard drive without rebooting, you can trigger a scan of the SCSI hosts:

```bash
echo "- - -" > /sys/class/scsi_host/host0/scan
echo "- - -" > /sys/class/scsi_host/host1/scan
echo "- - -" > /sys/class/scsi_host/host2/scan
```

- **Disk Naming**: Disks are typically named alphabetically (e.g., sda is the first disk, sdb is the second).

## 3. Partitioning with fdisk

The fdisk utility is used to create and manage partitions on a disk.

- **Accessing a Disk**: `fdisk /dev/sdb`
- **Common fdisk Internal Commands**:
  - `m`: View the help menu
  - `n`: Add a **new** partition
  - `p`: **Print** the current partition table
  - `d`: **Delete** a partition
  - `w`: **Write** changes to the disk and exit
  - `q`: Quit without saving changes

- **Informing the Kernel**: After saving partitions, the kernel may not see the new table immediately. Use the partx command to update it:

```bash
partx -a /dev/sdb
```

The command adds the new partitions to the kernel's awareness.

## 4. File System Creation and Mounting

A partition must be formatted with a file system and "mounted" to a directory before it can be used.

- **Formatting (mkfs)**: Creates a file system on the partition.

```bash
mkfs.ext4 /dev/sdb1
```

The command formats the first partition of disk sdb with the ext4 file system.

- **Creating a Mount Point**: Create an empty directory where the disk will be attached.

```bash
mkdir /jet
```

- **Mounting**: Connects the partition to the directory.

```bash
mount /dev/sdb1 /jet
```

- **Verifying Mounts**:

```bash
df -h
lsblk
```

The commands show all mounted file systems, their sizes, and used/available space in human-readable format, and confirm the mount point for specific partitions.