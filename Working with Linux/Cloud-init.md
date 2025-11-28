# Cloud-Init -- Automated Linux Configuration on First Boot

Cloud-init is the industry-standard tool used by cloud platforms to
automatically configure Linux virtual machines on their first boot. It
enables full automation of users, SSH keys, packages, networking,
scripts and more using a YAML configuration file.

Cloud-init is essential in environments such as OpenStack, AWS, Azure
and others.

------------------------------------------------------------------------

## 1. What Is Cloud-Init?

Cloud-init automatically configures a Linux virtual machine on its first
boot.

It can configure: - Users - SSH keys - Packages - Network settings -
Hostname - Filesystems and mounts - Writing files - Running scripts and
commands

This allows consistent, reproducible VM deployments with no manual
steps.

------------------------------------------------------------------------

## 2. How Cloud-Init Works

### Step 1: Metadata Service Detection

When a VM boots, it queries a metadata service, usually located at:

    169.254.169.254

The metadata service provides: - Instance ID - Hostname - User-data
(cloud-init YAML) - SSH keys - Networking configuration

### Step 2: Retrieve Configuration

Cloud-init retrieves the YAML user-data file and prepares configuration
tasks.

### Step 3: Execute Modules in Stages

#### Init Stage

-   Set hostname
-   Configure basic networking
-   Identify metadata

#### Config Stage

-   Create users
-   Install SSH keys
-   Install packages
-   Write files
-   Apply system configuration

#### Final Stage

-   Run scripts (runcmd)
-   Execute bootstrap logic
-   Finalize setup

After this, the VM is fully configured automatically.

------------------------------------------------------------------------

## 3. What a Cloud-Init YAML Can Do

A single YAML file can perform: - Hostname configuration - Creating
users and groups - Installing SSH keys - Installing packages - Running
commands or scripts - Writing configuration files - Mounting disks

All without manually accessing the VM.

------------------------------------------------------------------------

## 4. How OpenStack Uses Cloud-Init

OpenStack provisions VMs using a metadata service that cloud-init reads
on first boot.

Process: 

1. OpenStack exposes metadata to the VM on 169.254.169.254

2. Cloud-init retrieves user-data, SSH keys, hostnames and network
configs

3. Cloud-init configures the VM entirely: - Creates user accounts
- Injects SSH keys
- Configures networking
- Sets hostname
- Mounts filesystems
- Installs packages
- Runs bootstrap scripts
4. VM becomes fully ready for use

This eliminates issues like: - Missing hostnames
- No SSH access after provisioning
- Inconsistent VM configurations

Cloud-init ensures all VMs are consistent and repeatable.

------------------------------------------------------------------------

## Summary

-   Cloud-init automates first-boot configuration of Linux VMs.
-   It uses YAML to configure users, packages, SSH keys, networking and
    more.
-   Metadata is retrieved from 169.254.169.254.
-   Cloud-init runs in stages: init → config → final.
-   OpenStack relies on cloud-init to provision fully configured VMs.