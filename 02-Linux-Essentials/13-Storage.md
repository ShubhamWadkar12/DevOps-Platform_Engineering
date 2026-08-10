# 💾 Linux Storage

Linux storage management is about understanding how disks, partitions, filesystems, mount points, and files work together.

As a DevOps Engineer, you will work with storage when managing:

- Linux servers
- Cloud instances
- Application data
- Logs
- Backups
- Databases
- Docker volumes
- Kubernetes persistent storage

The basic storage flow is:

```text
Disk
 ↓
Partition
 ↓
Filesystem
 ↓
Mount Point
 ↓
Files & Directories
```

---

# 💽 Storage Devices

Linux represents storage devices under:

```text
/dev
```

Common device names include:

```text
/dev/sda
/dev/sdb
/dev/vda
/dev/nvme0n1
```

The exact naming depends on the hardware or virtualization environment.

---

# 🔍 `lsblk`

`lsblk` displays information about block devices.

```bash
lsblk
```

For filesystem information:

```bash
lsblk -f
```

You can see:

- Device
- Partition
- Filesystem
- UUID
- Mount point

Example:

```text
NAME        FSTYPE   MOUNTPOINTS
sda
├─sda1      ext4     /
└─sda2      swap     [SWAP]
```

---

# 🧩 Partitions

A disk can be divided into multiple partitions.

Example:

```text
/dev/sda
├── /dev/sda1
├── /dev/sda2
└── /dev/sda3
```

Partitions allow different parts of a disk to be managed separately.

Common reasons for partitioning include:

- Separating system and application data
- Creating swap space
- Isolating specific workloads
- Managing storage requirements

---

# 🔎 Viewing Partitions

Use:

```bash
lsblk
```

You can also use:

```bash
sudo fdisk -l
```

or:

```bash
sudo parted -l
```

⚠️ Partitioning tools can destroy data if used incorrectly. Never modify a production disk without understanding exactly what device you are changing.

---

# 🛠️ `fdisk`

`fdisk` is a command-line utility for managing disk partition tables.

View disks:

```bash
sudo fdisk -l
```

Open a disk for partition management:

```bash
sudo fdisk /dev/sdb
```

Do not experiment with `fdisk` on a disk containing important data.

---

# 🏗️ Filesystems

A filesystem determines how data is organized and stored on a partition or storage device.

Common Linux filesystems include:

```text
ext4
XFS
Btrfs
```

Check filesystem information:

```bash
lsblk -f
```

---

# 🐧 ext4

`ext4` is one of the most widely used Linux filesystems.

It is commonly used for:

- Linux installations
- Servers
- General-purpose storage

Example:

```text
/dev/sdb1 → ext4
```

---

# 🏢 XFS

XFS is a high-performance filesystem commonly used in enterprise Linux environments.

It is especially common in RHEL-based environments.

Check it with:

```bash
lsblk -f
```

---

# 🌳 Btrfs

Btrfs is a modern copy-on-write filesystem.

It supports features such as:

- Snapshots
- Subvolumes
- Checksums
- Compression

It is used by some Linux distributions and specialized environments.

---

# 🆔 Filesystem UUID

A filesystem can have a unique identifier called a UUID.

Display UUIDs:

```bash
blkid
```

Example:

```text
/dev/sdb1: UUID="xxxx-xxxx" TYPE="ext4"
```

UUIDs are commonly used in `/etc/fstab` for persistent mounts.

---

# 📍 Mounting

Mounting makes a filesystem accessible through a directory in the Linux filesystem tree.

For example:

```text
/dev/sdb1
     ↓
   /data
```

The filesystem on `/dev/sdb1` becomes accessible through:

```text
/data
```

---

# 📁 Creating a Mount Point

Create a directory:

```bash
sudo mkdir /data
```

Mount a filesystem:

```bash
sudo mount /dev/sdb1 /data
```

Verify:

```bash
df -h
```

or:

```bash
findmnt /data
```

---

# 🔍 `findmnt`

`findmnt` displays mounted filesystems.

```bash
findmnt
```

Check a specific mount point:

```bash
findmnt /data
```

---

# 📋 `mount`

Display mounted filesystems:

```bash
mount
```

Mount a filesystem:

```bash
sudo mount /dev/sdb1 /data
```

---

# ⏏️ Unmounting

To detach a filesystem:

```bash
sudo umount /data
```

Remember:

```text
umount
```

not:

```text
unmount
```

Verify:

```bash
findmnt /data
```

---

# ⚠️ Device is Busy

Sometimes you may get:

```text
target is busy
```

This means something is currently using the filesystem.

Check processes:

```bash
sudo lsof +D /data
```

or:

```bash
sudo fuser -vm /data
```

Also make sure your terminal is not currently inside the directory:

```bash
cd ~
```

Then try:

```bash
sudo umount /data
```

---

# 📋 `/etc/fstab`

The file:

```text
/etc/fstab
```

contains filesystem mount configuration.

View it:

```bash
cat /etc/fstab
```

A typical entry looks like:

```text
UUID=xxxx-xxxx  /data  ext4  defaults  0  2
```

The general structure is:

```text
<device> <mount-point> <filesystem> <options> <dump> <fsck>
```

---

# 🔄 Testing `/etc/fstab`

After modifying `/etc/fstab`, test the configuration:

```bash
sudo mount -a
```

Then verify:

```bash
findmnt
```

and:

```bash
df -h
```

⚠️ Incorrect `/etc/fstab` entries can cause boot or mounting problems, so always verify changes carefully.

---

# 📊 Disk Usage

## `df`

`df` shows filesystem-level disk usage.

```bash
df -h
```

Example:

```text
Filesystem      Size  Used Avail Use%
/dev/sda1        50G   20G   30G  40%
```

The `-h` option makes sizes human-readable.

---

# 📁 `du`

`du` shows how much space files and directories consume.

Check a directory:

```bash
du -sh /var/log
```

Check directories in the current location:

```bash
du -h --max-depth=1
```

Remember:

```text
df → Filesystem usage

du → File/directory usage
```

---

# 🧮 Inodes

Disk space is not the only storage resource.

Linux filesystems also use **inodes** to store metadata about filesystem objects.

Check inode usage:

```bash
df -i
```

A filesystem can have free disk space but still fail to create new files if it has run out of available inodes.

This can happen when a system contains a very large number of small files.

---

# 🔎 Finding Large Files

Find files larger than 100 MB:

```bash
find . -type f -size +100M
```

Find files larger than 1 GB:

```bash
sudo find / -type f -size +1G -exec ls -lh {} \;
```

Be careful when searching the entire filesystem.

---

# 🚨 `No space left on device`

If an application reports:

```text
No space left on device
```

First check:

```bash
df -h
```

Then check inodes:

```bash
df -i
```

Find large directories:

```bash
du -h --max-depth=1
```

For example:

```bash
sudo du -xhd1 /var | sort -h
```

Then investigate what is consuming the storage.

Never blindly delete files from system directories.

---

# 🗜️ Compression and Archives

Compression and archiving are commonly used for:

- Backups
- Log management
- Application packaging
- File transfers
- Deployment artifacts

Common tools include:

```text
tar
gzip
zip
```

---

# 📦 `tar`

`tar` creates and extracts archives.

Create an archive:

```bash
tar -cf backup.tar project/
```

Create a gzip-compressed archive:

```bash
tar -czf backup.tar.gz project/
```

Extract an archive:

```bash
tar -xf backup.tar
```

Extract a `.tar.gz` archive:

```bash
tar -xzf backup.tar.gz
```

List archive contents:

```bash
tar -tf backup.tar
```

---

# 🗜️ `gzip`

`gzip` compresses files.

```bash
gzip file.txt
```

This creates:

```text
file.txt.gz
```

Decompress:

```bash
gunzip file.txt.gz
```

Important:

```text
gzip → Compression

tar → Archiving
```

They are often used together:

```text
tar
 ↓
Archive
 ↓
gzip
 ↓
Compressed archive
```

Result:

```text
backup.tar.gz
```

---

# 📦 `zip`

Create a ZIP archive:

```bash
zip backup.zip file.txt
```

Create a ZIP archive from a directory:

```bash
zip -r backup.zip project/
```

Extract:

```bash
unzip backup.zip
```

List contents:

```bash
unzip -l backup.zip
```

---

# 🆚 tar vs gzip vs zip

| Tool | Main Purpose |
|---|---|
| `tar` | Archive multiple files/directories |
| `gzip` | Compress files |
| `zip` | Archive and compress files |

Example:

```text
tar
 ↓
backup.tar
```

```text
tar + gzip
 ↓
backup.tar.gz
```

```text
zip
 ↓
backup.zip
```

---

# 🌍 Real-World DevOps Example

Suppose you need to back up an application directory:

```text
/opt/myapp
```

Create a compressed backup:

```bash
tar -czf myapp-backup.tar.gz /opt/myapp
```

Check the archive:

```bash
tar -tf myapp-backup.tar.gz
```

You can then transfer or store the backup.

This type of operation is common in:

- Deployment workflows
- Backup scripts
- CI/CD pipelines
- Server migration
- Disaster recovery

---

# ☁️ Cloud Storage

Cloud providers offer different types of storage.

For example, AWS provides:

```text
EBS → Block Storage
S3  → Object Storage
EFS → Managed File Storage
```

A typical EC2 block-storage workflow is:

```text
EBS Volume
    ↓
Attach to EC2
    ↓
Linux detects disk
    ↓
Partition
    ↓
Filesystem
    ↓
Mount
    ↓
Application
```

---

# 🐳 Docker Storage

Containers have writable filesystem layers, but important application data should normally use persistent storage.

Conceptually:

```text
Container
    ↓
Volume
    ↓
Persistent Data
```

Docker volumes will be covered in detail during the Docker phase.

---

# ☸️ Kubernetes Storage

Kubernetes provides abstractions for persistent storage:

```text
PersistentVolume (PV)
        ↓
PersistentVolumeClaim (PVC)
        ↓
Storage Backend
```

StorageClasses can be used to dynamically provision storage.

Kubernetes storage will be covered in detail during the Kubernetes phase.

---

# 🛠️ Hands-on Practice

Check your storage:

```bash
lsblk
```

```bash
lsblk -f
```

```bash
df -h
```

```bash
df -i
```

Check mounted filesystems:

```bash
findmnt
```

Check directory size:

```bash
du -sh /var/log
```

Check filesystem UUIDs:

```bash
blkid
```

View persistent mount configuration:

```bash
cat /etc/fstab
```

---

# 🧪 Compression Practice

Create a practice directory:

```bash
mkdir -p ~/storage-lab
cd ~/storage-lab
```

Create files:

```bash
touch file1.txt file2.txt file3.txt
```

Create an archive:

```bash
tar -cf files.tar file1.txt file2.txt file3.txt
```

List the archive:

```bash
tar -tf files.tar
```

Create a compressed archive:

```bash
tar -czf files.tar.gz file1.txt file2.txt file3.txt
```

List it:

```bash
tar -tf files.tar.gz
```

Create a ZIP archive:

```bash
zip files.zip file1.txt file2.txt file3.txt
```

List it:

```bash
unzip -l files.zip
```

---

# 🧪 Practice Challenge

Perform a complete storage investigation.

### Step 1

Identify disks:

```bash
lsblk
```

### Step 2

Identify filesystems:

```bash
lsblk -f
```

### Step 3

Check available space:

```bash
df -h
```

### Step 4

Check inode usage:

```bash
df -i
```

### Step 5

Find large directories:

```bash
du -h --max-depth=1 ~
```

### Step 6

Check mounted filesystems:

```bash
findmnt
```

### Step 7

Create a compressed archive:

```bash
tar -czf storage-lab.tar.gz ~/storage-lab
```

### Step 8

Verify it:

```bash
tar -tf storage-lab.tar.gz
```

Document:

```text
Disk:
Partition:
Filesystem:
Mount Point:
Total Space:
Used Space:
Available Space:
Inode Usage:
```

---

# ⚠️ Storage Safety

Be extremely careful with:

```bash
fdisk
parted
mkfs
mount
umount
rm
```

Especially:

```bash
mkfs
```

because formatting a partition can destroy existing data.

Before making storage changes, verify:

```bash
lsblk
```

```bash
lsblk -f
```

```bash
df -h
```

Always confirm the exact device before performing destructive operations.

---

# 💼 Interview Questions

- **What is a partition?**  
  A partition is a logical division of a storage device that can be managed independently.

- **What is a filesystem?**  
  A filesystem defines how files, directories, and metadata are organized on storage.

- **What is mounting?**  
  Mounting makes a filesystem accessible through a directory in the Linux filesystem tree.

- **What is a mount point?**  
  A mount point is the directory where a filesystem is attached.

- **What is the purpose of `lsblk`?**  
  `lsblk` displays block devices, partitions, filesystems, and mount points.

- **What is the difference between `df` and `du`?**  
  `df` shows filesystem-level disk usage, while `du` shows the space consumed by files and directories.

- **What is `/etc/fstab`?**  
  `/etc/fstab` contains filesystem mount configuration used to define mounts, including persistent mounts.

- **Why are UUIDs used in `/etc/fstab`?**  
  UUIDs provide a stable identifier for a filesystem and avoid depending solely on device names.

- **What is `mkfs` used for?**  
  `mkfs` creates a filesystem on a device or partition. It can destroy existing data on the target.

- **What is the difference between `mount` and `umount`?**  
  `mount` attaches a filesystem to the filesystem tree, while `umount` detaches it.

- **What is an inode?**  
  An inode stores metadata about a filesystem object such as its permissions, ownership, timestamps, and references to its data.

- **Can a filesystem have free disk space but still be unable to create files?**  
  Yes. The filesystem may have exhausted its available inodes.

- **What is the difference between `tar` and `gzip`?**  
  `tar` is primarily used for archiving multiple files, while `gzip` compresses data. They are commonly used together to create `.tar.gz` archives.

- **What is a `.tar.gz` file?**  
  It is a tar archive that has been compressed using gzip.

- **What is the difference between `tar.gz` and `zip`?**  
  `tar` creates an archive and gzip can compress it, while ZIP combines archiving and compression in one format.

- **How would you troubleshoot `No space left on device`?**  
  Check `df -h` for disk capacity, `df -i` for inode exhaustion, and `du` to identify directories consuming significant space.

- **Why is storage knowledge important for DevOps?**  
  DevOps engineers manage server disks, cloud volumes, application data, logs, backups, containers, and Kubernetes persistent storage.

---

# 📚 Navigation

⬅️ Previous: **[12-Processes-and-Services.md](12-Processes-and-Services.md)**

➡️ Next: **[14-Package-Management.md](14-Package-Management.md)**
