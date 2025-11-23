# Linux Boot Sequence -- Full Breakdown

This document explains the full Linux boot process from the moment a
machine powers on to when the user reaches the login prompt.
Understanding this flow is essential for systems administration,
troubleshooting and DevOps engineering.

------------------------------------------------------------------------

## Stage 1: BIOS / UEFI

### Power-On

The boot process begins as soon as the machine is powered on.

### BIOS/UEFI Initialization

The system firmware (BIOS or UEFI) starts running and performs a
**Power-On Self-Test (POST)**.\
POST checks memory, CPU, disk controllers and other hardware to ensure
they are functioning correctly.

### Bootloader Search

After POST, BIOS/UEFI searches for a **bootable device**.\
This may include: - HDD/SSD - USB - CD/DVD - Network boot (PXE)

It locates and loads the **bootloader** from either: - The **Master Boot
Record (MBR)**\
- The **EFI System Partition (ESP)** in UEFI systems

------------------------------------------------------------------------

## Stage 2: Bootloader (e.g., GRUB)

### Bootloader Loading

BIOS/UEFI hands off control to a bootloader such as **GRUB** (GRand
Unified Bootloader).\
GRUB is responsible for managing and loading operating systems.

### Kernel Selection

GRUB may present a menu allowing selection between: - Multiple installed
Linux kernels - Recovery mode - Other operating systems (dual-boot)

### Kernel Loading

Once selected, GRUB loads: - The Linux **kernel** - The **initramfs**
(initial RAM filesystem)

Both are placed into memory and executed.

------------------------------------------------------------------------

## Stage 3: Kernel

### Kernel Initialization

The kernel performs several critical tasks: - Decompresses into memory\
- Initializes CPU, memory management and device drivers\
- Detects hardware (via udev)\
- Sets up kernel subsystems

### Root Filesystem Mount

The kernel mounts the **root filesystem** so it can access system files,
libraries and userland tools.

If required drivers are missing, it uses the **initramfs** to load extra
drivers needed to mount the root filesystem.

------------------------------------------------------------------------

## Stage 4: Init Process (PID 1)

### Init Program Execution

After the kernel completes initialization, it starts the **init
process**.\
This is always **PID 1**, the first user-space program on the system.

Modern Linux systems use: - **systemd** (most common) - SysVinit
(older) - OpenRC (some distros) - runit/s6 (minimalist systems)

### System Initialization

The init system takes over: - Mounts extra filesystem targets\
- Starts essential services and daemons (networking, logging, cron,
etc.)\
- Handles dependencies between services\
- Applies boot targets such as `multi-user.target` or `graphical.target`

### Login Prompt

When initialization is complete, Linux presents: - A terminal login
(TTY)\
- Or a graphical login manager (GDM, LightDM, SDDM)

The system is now fully operational.

------------------------------------------------------------------------

## Summary

-   BIOS/UEFI performs hardware checks and finds the bootloader.\
-   GRUB loads the kernel and initramfs.\
-   The kernel configures hardware and mounts the root filesystem.\
-   systemd (PID 1) starts services and prepares the user environment.\
-   The system reaches the login prompt, completing the boot sequence.