# Disk Geometry and Logical Volume Management Fundamentals

These notes are based on covering the technical definition of cylinders in disk storage and the complete workflow for **Logical Volume Management (LVM)**.

## 1. Understanding Disk Cylinders

In traditional disk geometry, a cylinder is a key unit of measurement for how data is organised physically on a drive.

- **Definition:** A cylinder is a collection of tracks across all platters that are located at the same radius.
- **Size Calculation:** The size of a cylinder is determined by the number of heads (platters/sides), sectors per track, and the number of bytes per sector.
- **Mathematical Example:**

```text
Heads = 64
Sectors per track = 32
Bytes per sector = 512
```

**Calculation:** $64 \times 32 \times 512 = 1,048,576$ bytes.

**Result:** 1 cylinder = 1 MB (Note: Some configurations may vary, such as 1 cylinder equaling 8 MB depending on the hardware).

## 2. Logical Volume Management (LVM)

**LVM** is a device driver layer that sits above regular partitions. Its primary advantage is flexibility; unlike normal partitions which are fixed in size, LVM allows for **extendable and reducible partitions**.

### A. The Three Layers of LVM

LVM organises storage into three distinct layers:

1. **Physical Volume (PV):** The physical disk or partition (e.g., /dev/sdc1).
2. **Volume Group (VG):** A "pool" of storage created by combining one or more Physical Volumes.
3. **Logical Volume (LV):** The actual "virtual partition" carved out of the Volume Group that is formatted and mounted for use.

### B. Step-by-Step LVM Configuration

To create an LVM-managed storage space, follow these steps:

- **Preparation:** Add a new hard drive (e.g., 2 GB) and discover it using the SCSI scan command.
- **Create Partition:** Use `fdisk /dev/sdc` to create a new partition (e.g., `/dev/sdc1`).
- **Crucial Step:** Change the partition type to **8e** (Linux LVM) so the system recognises it as an LVM member.
- **Update Kernel:** Run `partx -a /dev/sdc` to inform the kernel of the new partition table.
- **Initialise Physical Volume:**

```bash
pvcreate /dev/sdc1
pvdisplay
```

- **Create Volume Group:**

```bash
vgcreate netvg /dev/sdc1
vgdisplay
```

- **Create Logical Volume:**

```bash
lvcreate -L 300M -n netlv netvg
lvdisplay
```

- **Finalise and Use:**
- **Format:** `mkfs.ext4 /dev/netvg/netlv`
- **Mount Point:** `mkdir /airindia`
- **Mount:** `mount /dev/netvg/netlv /airindia`
- **Verify:** Use `df -h` to confirm the new, flexible storage is active.

### C. Identifying LVM Drivers

You can verify the active LVM paths in the system using `ls`:

- `ls /dev/netvg/netlv`
- `ls /dev/mapper/netvg-netlv`

