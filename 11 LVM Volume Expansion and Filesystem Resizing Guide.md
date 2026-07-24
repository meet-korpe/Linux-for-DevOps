# LVM Volume Expansion and Filesystem Resizing Guide

Here are the detailed notes on how to extend an LVM (Logical Volume Management) partition. The primary advantage of LVM is its flexibility, allowing you to increase the size of a partition even while it is mounted and in use.

## The Two-Step Extension Process

Extending a partition in LVM is a **two-step process**. First, you must increase the size of the Logical Volume (LV), and then you must inform the filesystem of the new space so it can expand to fill it.

## Step 1: Extend the Logical Volume (lvextend)

The lvextend command is used to add space from the Volume Group (VG) to a specific Logical Volume. There are two common ways to specify the new size:

### By Specific Size (-L)

```bash
lvextend -L +100M /dev/newvg/newlv
```

- **Function:** This adds exactly 100 MB to the existing size of the logical volume.
- **Example:** You can also use larger units like `+2G` for gigabytes.

### By Percentage of Free Space (-l)

```bash
lvextend -l +100%FREE /dev/newvg/newlv
```

- **Function:** This is a "task" command that tells the system to take **all** remaining free space in the Volume Group and add it to the Logical Volume.
- **Example:** You can also use specific percentages like `+75%FREE`.

## Step 2: Resize the Filesystem

After the Logical Volume is extended, the operating system still sees the old filesystem size. You must use a "driver" or utility to resize the filesystem itself. **Note:** The command depends on the type of filesystem you are using.

### For ext3 and ext4 Filesystems

```bash
resize2fs /dev/newvg/newlv
```

- **Function:** This performs an **on-line resize**, meaning the partition remains mounted and accessible during the process.

### For XFS Filesystems

```bash
xfs_growfs [mount_point]
```

- **Note:** Unlike resize2fs, xfs_growfs typically targets the mount point rather than the device pat.

## 3. Verification

Once both steps are complete, you should verify that the new space is correctly recognised by the system:

- **df -h:** Use this command to see the updated size, used space, and available space for your mount point (e.g., /java).
- **vgdisplay:** Use this to check the remaining "Free PE / Size" in your Volume Group to ensure your changes were applied.
- **lvdisplay:** Use this to see the new total size of the Logical Volume.

