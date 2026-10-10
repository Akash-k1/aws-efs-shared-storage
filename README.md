# AWS EFS Shared Storage Across Three EC2 Instances

## Project Overview

This project demonstrates mounting Amazon Elastic File System (EFS) on three Amazon EC2 instances using Linux commands and verifying shared file access across the servers.

## Objectives

- Configure and access Amazon EFS from multiple EC2 instances.
- Mount a shared filesystem using NFSv4.1.
- Create and access files through the shared filesystem.
- Understand shared storage in an AWS environment.

## AWS Services and Technologies

- Amazon EC2
- Amazon EFS
- Amazon VPC (default VPC)
- Amazon Linux
- Linux command line
- NFSv4.1

## Architecture

Three EC2 instances connect to the same EFS filesystem through an EFS mount target within the VPC.

**Flow:**

EC2 Instance 1 ─┐  
EC2 Instance 2 ─┼── Amazon EFS  
EC2 Instance 3 ─┘

All three instances mount the same filesystem, allowing them to access shared files.

## Implementation Steps

### 1. Create the EFS Filesystem

- Created an Amazon EFS filesystem.
- Used the default VPC for the lab.
- Used the EFS mount target IP address to connect from the EC2 instances.

### 2. Create Mount Directories

On each EC2 instance, created a directory to use as the mount point.

```bash
mkdir folder3
```

### 3. Mount EFS Using NFS

Mounted the EFS filesystem using a Linux NFS command.

```bash
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport <EFS-MOUNT-TARGET-IP>:/ folder3
```

Replace `<EFS-MOUNT-TARGET-IP>` with the actual EFS mount target IP address.

### 4. Verify Shared File Access

Navigated to the mounted directory and listed its contents.

```bash
cd folder3
ls
```

Created and accessed files on the shared filesystem and verified their visibility across the three EC2 instances.

## Key Learnings

- Amazon EFS shared filesystem concepts.
- Mounting network filesystems on Linux.
- NFSv4.1 and EFS mount target connectivity.
- Shared file access across multiple EC2 instances.
- Basic AWS networking and Linux administration.

## Cleanup

Unmount the EFS filesystem from each instance when finished and delete the EFS filesystem and unused lab resources when they are no longer needed to avoid ongoing charges.
