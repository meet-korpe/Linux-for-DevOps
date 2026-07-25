# LVM Resizing

## 1. Recap: Extending LVM (The Easy Way)

Extending an LVM partition is relatively safe and can often be done while the partition is still mounted (online).

- **Step 1:** `lvextend -L +100M /dev/myvg/mylv` (Increases the Logical Volume size).
- **Step 2:** `resize2fs /dev/myvg/mylv` (Expands the filesystem to fill the new space).

## 2. Reducing LVM (The Careful Way)

Reducing a partition is a high-risk operation because it can **destroy your data** if not done in the correct order. Unlike extension, reduction **must be done offline** (unmounted).

### Step-by-Step Reduction Workflow

- **Unmount the Partition**: You cannot safely shrink a filesystem while it is in use.

```bash
umount /jet
```

- **Check for Errors (e2fsck)**: Always perform a forced filesystem check to ensure data integrity before shrinking.

```bash
e2fsck -f /dev/newvg/newlv
```

This process involves five passes: checking inodes, directory structure, connectivity, reference counts, and group summary.

- **Shrink the Filesystem (resize2fs)**: You must shrink the filesystem **before** you shrink the Logical Volume.

```bash
resize2fs /dev/newvg/newlv 500M
```

(This resizes the filesystem to exactly 500MB).

- **Shrink the Logical Volume (lvreduce)**: Now that the filesystem is small enough, you can reduce the container holding it.

```bash
lvreduce -L 500M /dev/newvg/newlv
```

- **Warning:** The system will prompt you with a warning: *"THIS MAY DESTROY YOUR DATA."* You must confirm with y.
- **Remount and Verify**:

```bash
mount /dev/newvg/newlv /jet
df -h
```

- `df -h`: Check the new size to ensure the operation was successful.