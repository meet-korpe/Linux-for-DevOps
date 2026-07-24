# Linux Storage Architecture and Disk Partitioning Management

Based on the latest source material, these notes provide a detailed look at disk partitioning strategies, the differences between partition table types, and the practical commands used to manage storage devices.

## 1. Partitioning Strategies and Cases

Linux disks can be partitioned in various ways depending on the requirements for primary, extended, and logical partitions.

- **Primary Partitions**: These are the basic divisions of a hard drive. Under certain table types, there is a limit to how many can be created.
  - **Case 1 (All Primary)**: A disk (e.g., /dev/sdc) can be divided into four primary partitions: sdc1, sdc2, sdc3, and sdc4.

- **Extended and Logical Partitions**: If more than four partitions are needed on an MBR disk, one primary partition must be designated as an **Extended Partition**.
  - **Case 2**: Three primary partitions (sdc1, sdc2, sdc3) and one **Extended Partition** (sdc4). Inside the extended partition, multiple **Logical Partitions** (labeled l1, l2, l3, l4 and mapped to sdc5, sdc6, etc.) can be created.
  - **Case 3**: An extended partition (e.g., sdc3) can hold logical partitions starting from index 5 (sdc5, sdc6, sdc7), while sdc1, sdc2, and sdc4 remain primary or reserved.

## 2. Partition Table Types

There are two main types of partition tables used to define how data is organized on the disk:

- **MS-DOS / MBR (Master Boot Record)**:
  - Supports a maximum of **4 Primary Partitions**.
  - To exceed 4 partitions, you must use an **Extended Partition**, which can then support many logical partitions.

- **GPT (GUID Partition Table)**:
  - A more modern standard that supports up to **128 Primary Partitions**.
  - Does not require the primary/extended/logical distinction used by MBR.

