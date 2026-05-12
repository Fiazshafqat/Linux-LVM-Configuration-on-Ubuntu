# Linux LVM Configuration on Ubuntu

This project demonstrates how to configure **LVM (Logical Volume Manager)** on Ubuntu Linux using two physical hard drives. It includes creating Physical Volumes (PV), Volume Groups (VG), Logical Volumes (LV), formatting with EXT4, mounting storage, and configuring persistent mounts using `/etc/fstab`.

---

# Lab Environment

| Component | Value |
|---|---|
| Operating System | Ubuntu Linux |
| Disk 1 | `/dev/sdb` (1.5G) |
| Disk 2 | `/dev/sdc` (3.0G) |
| Volume Group Name | `volume-group1` |
| Logical Volume Name | `lv1` |
| Mount Point | `/mnt/data` |
| Filesystem | EXT4 |

---

# Architecture Overview

- Two physical disks are combined into a single Volume Group.
- A Logical Volume is created from the Volume Group.
- EXT4 filesystem is configured on the Logical Volume.
- Storage is mounted persistently using `/etc/fstab`.

---

# Step 1 — Verify Available Disks

Check available disks and block devices:

```bash
lsblk
```

---

# Step 2 — Install LVM Package

Update packages and install LVM utilities:

```bash
sudo apt update
sudo apt install lvm2 -y
```

Verify installation:

```bash
lvm version
```

---

# Step 3 — Create Physical Volumes (PV)

Initialize disks as Physical Volumes:

```bash
sudo pvcreate /dev/sdb /dev/sdc
```

Verify PV creation:

```bash
sudo pvs
```

---

# Step 4 — Create Volume Group (VG)

Create a Volume Group named `volume-group1`:

```bash
sudo vgcreate volume-group1 /dev/sdb /dev/sdc
```

Verify Volume Group:

```bash
sudo vgs
```

---

# Step 5 — Create Logical Volume (LV)

Create a Logical Volume named `lv1` with size `4.5G`:

```bash
sudo lvcreate -L 4.5G -n lv1 volume-group1
```

Verify Logical Volume:

```bash
sudo lvs
```

Logical Volume path:

```bash
/dev/volume-group1/lv1
```

---

# Step 6 — Create Filesystem

Format the Logical Volume with EXT4 filesystem:

```bash
sudo mkfs.ext4 /dev/volume-group1/lv1
```

---

# Step 7 — Create Mount Point

Create a directory for mounting storage:

```bash
sudo mkdir -p /mnt/data
```

---

# Step 8 — Mount Logical Volume

Mount the Logical Volume:

```bash
sudo mount /dev/volume-group1/lv1 /mnt/data
```

Verify mounted filesystem:

```bash
df -h
```

---

# Step 9 — Configure Persistent Mount

Edit the `/etc/fstab` file:

```bash
sudo vim /etc/fstab
```

Add the following entry:

```bash
/dev/volume-group1/lv1   /mnt/data   ext4   defaults   0   2
```

Test the configuration:

```bash
sudo mount -a
```

This ensures the Logical Volume automatically mounts after every reboot.

---

# Verification Commands

Check Physical Volumes:

```bash
sudo pvs
```

Check Volume Groups:

```bash
sudo vgs
```

Check Logical Volumes:

```bash
sudo lvs
```

Check mounted storage:

```bash
df -h
```

---

# Key Learning Outcomes

✅ Understanding LVM architecture  
✅ Creating Physical Volumes (PV)  
✅ Managing Volume Groups (VG)  
✅ Creating Logical Volumes (LV)  
✅ Formatting and mounting storage  
✅ Persistent storage configuration using `/etc/fstab`  
✅ Linux storage management best practices  

---

# Technologies Used

| Technology | Purpose |
|---|---|
| Ubuntu Linux | Operating System |
| LVM2 | Logical Volume Management |
| EXT4 | Filesystem |
| `/etc/fstab` | Persistent Mount Configuration |

---

# Project Screentshots

## 1. Create Physical Volume from 2 disks
![image alt](https://github.com/Fiazshafqat/Linux-LVM-Configuration-on-Ubuntu/blob/main/create%20physical%20volume.jpg?raw=true)

## 2. Create Volume Group
![image alt](https://github.com/Fiazshafqat/Linux-LVM-Configuration-on-Ubuntu/blob/main/create%20vloume%20group.jpg?raw=true)

## 3. Create Logical Voluume
![image alt](https://github.com/Fiazshafqat/Linux-LVM-Configuration-on-Ubuntu/blob/main/create%20logical%20vloume.jpg?raw=true)

## 4. Make filesystem ext4
![image alt](https://github.com/Fiazshafqat/Linux-LVM-Configuration-on-Ubuntu/blob/main/make%20partition%20file%20system%20or%20format.jpg?raw=true)

## 5. Add mount point locations of volume
![image alt](https://github.com/Fiazshafqat/Linux-LVM-Configuration-on-Ubuntu/blob/main/mount%20logical%20volume.jpg?raw=true)

## 6. Verify list of volume with their mount point
![image alt](https://github.com/Fiazshafqat/Linux-LVM-Configuration-on-Ubuntu/blob/main/verify%20volumes.jpg?raw=true)

## 7. Configured and verify a persistent mount point in Ubuntu by adding the filesystem entry to the /etc/fstab file, ensuring the disk or partition automatically mounts after every system reboot.
![image alt](https://github.com/Fiazshafqat/Linux-LVM-Configuration-on-Ubuntu/blob/main/set%20in%20fstab%20etc%20.jpg?raw=true)

# Author

**Muhammad Faisal**  
Network Systems Engineer | Cloud & Infrastructure Enthusiast

---

# Tags

`Linux` `Ubuntu` `LVM` `Storage` `Linux-Administration` `DevOps` `System-Administration` `Filesystem` `EXT4`
