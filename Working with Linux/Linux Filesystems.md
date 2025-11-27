# Linux Filesystems -- Overview, Types, Permissions and ACLs

This document explains how Linux filesystems work, common filesystem
types, how to inspect disk/mount information, and how to manage
permissions and ACLs.

------------------------------------------------------------------------

## 1. What Does a Filesystem Do?

A filesystem is responsible for: - Organising files and directories -
Controlling how data is stored and retrieved - Tracking file space -
Storing **inodes** (files/directories) - Keeping metadata such as: -
Owner - Permissions - Timestamps

Every file and folder on Linux is represented by an inode.

------------------------------------------------------------------------

## 2. Checking Disk Usage

### Command:

    df -h

Shows: - Disk space usage - Filesystem sizes - Mounted partitions -
Human-readable output (`-h`)

------------------------------------------------------------------------

## 3. Checking Mounts

### Command:

    findmnt

Shows: - All mounted filesystems - Source devices - Mount points -
Filesystem type

This is the modern replacement for reading `/proc/mounts`.

------------------------------------------------------------------------

## 4. Common Linux Filesystem Types

### NFS -- Network File System

-   Linux-native network filesystem\
-   Server exports directory → client mounts it\
-   Common in shared team environments (e.g., shared home directories)

### SMB/CIFS

-   Windows file sharing protocol\
-   Linux mounts SMB via CIFS\
-   Ideal for mixed Windows/Linux office environments\
-   Integrates with Active Directory

### Bind Mounts

-   Makes one directory appear at another location\
-   Useful for containers, chroot environments, or reorganising folders

### EXT4

-   Common default Linux filesystem\
-   Reliable, fast and simple\
-   Good general-purpose filesystem

### XFS

-   High-performance filesystem (default in RHEL)\
-   Excellent for large files, scalability and throughput

### Btrfs

-   Advanced filesystem with:
    -   Snapshots
    -   Self-healing
    -   Data checksums
    -   Rollbacks

### VFAT

-   Used on USB drives and EFI partitions\
-   No journaling\
-   Compatible with Windows/macOS

### tmpfs

-   Temporary in-memory filesystem\
-   Very fast\
-   Used for `/run`, `/tmp` and caching

------------------------------------------------------------------------

## 5. Changing File Permissions

### Command:

    chmod 752 file.txt

Meaning: - Owner: `rwx` - Group: `r-x` - Others: `-w-`

------------------------------------------------------------------------

## 6. Changing Ownership

### Command:

    chown user1:group1 file.txt

Meaning: - `user1` is now the owner\
- `group1` is now the assigned group

------------------------------------------------------------------------

## 7. ACLs (Access Control Lists)

ACLs provide fine-grained permissions beyond traditional
owner/group/other.

### Give user access:

    setfacl -m u:alice:rwx /project

### Give group access:

    setfacl -m g:devteam:rx /logs

### Remove a user's ACL:

    setfacl -x u:alice /project

### Remove all ACLs:

    setfacl -b /project

------------------------------------------------------------------------

## Summary

-   Filesystems store data, metadata and inodes.\
-   `df -h` shows storage usage; `findmnt` shows mounts.\
-   Linux supports many filesystems: NFS, SMB, EXT4, XFS, Btrfs, tmpfs,
    etc.\
-   Use `chmod` and `chown` for classic permissions.\
-   Use ACLs for more detailed access control.