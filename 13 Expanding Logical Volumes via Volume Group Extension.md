# Expanding Logical Volumes via Volume Group Extension

## Extending LVM when Volume Group is Fully Utilised

If your Volume Group (VG) is fully utilised, you cannot directly extend a Logical Volume. You must first add more physical storage to the pool.

### Step-by-Step Workflow

- **Add a New Physical Disk**: Physically or virtually attach a new hard drive to the system.
- **Create a New Partition**:

```bash
fdisk /dev/sdd
```

Use a tool like fdisk to create a partition on the new disk (e.g., `/dev/sdd1`).

- **Change Partition ID**: Set the partition type to **8e** (Linux LVM).
- **Update the Kernel**: Run `partx -a /dev/sdd` so the system recognises the new partition.
- **Initialise the Physical Volume (PV)**:

```bash
pvcreate /dev/sdd1
```

- **Extend the Existing Volume Group (VG)**: Add the new Physical Volume to your current Volume Group to increase its total capacity.

```bash
vgextend newvg /dev/sdd1
```

- **Extend the Logical Volume (LV)**: Now that the VG has free space, you can increase the size of the Logical Volume.

```bash
lvextend -L +500M /dev/newvg/newlv
```

- **Resize the Filesystem**: Finally, expand the filesystem to use the newly allocated space.

```bash
resize2fs /dev/newvg/newlv
```

## Monitoring and Verification Commands

The lesson highlights several shorthand commands to quickly check the status of your LVM layers:

- `pvs`: View a summary of Physical Volumes.
- `vgs`: View a summary of Volume Groups.
- `lvs`: View a summary of Logical Volumes.
- `lsblk`: List all block devices and their mount points to see the final disk layout.
- `vgdisplay / lvdisplay`: Used for more detailed information about groups and volumes during the process.
