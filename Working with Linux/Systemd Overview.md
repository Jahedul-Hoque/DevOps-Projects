# Understanding systemd

systemd is the primary service manager on modern Linux distributions. It
is responsible for booting the system, managing and supervising
services, handling dependencies, and managing logs through **journald**.

This file provides a concise overview of systemd concepts, commands and
unit types.

------------------------------------------------------------------------
 
## 1. What systemd does

systemd is responsible for:

-   Booting the operating system\
-   Starting, stopping and supervising services\
-   Logging system and service output through journald\
-   Managing dependencies between services\
-   Handling system targets (boot stages)\
-   Managing mounts, sockets, timers and many other system components

It replaces older init systems such as SysV init.

------------------------------------------------------------------------

## 2. Core systemctl Commands

These commands control system services:

    systemctl status <service>      # Checks service status
    systemctl start <service>       # Starts a service
    systemctl stop <service>        # Stops a service
    systemctl restart <service>     # Restarts a service

    systemctl enable <service>      # Enables service on boot
    systemctl disable <service>     # Disables service on boot

    systemctl daemon-reload         # Reloads unit files after changes

------------------------------------------------------------------------

## 3. What Is a Unit File?

A systemd unit file describes how a component behaves.\
For services, the unit file defines:

-   How the service starts\
-   What dependencies it needs\
-   Restart policies\
-   Logging behaviour\
-   Required ordering during boot

Unit files typically live in:

    /etc/systemd/system/

------------------------------------------------------------------------

## 4. Systemd Dependencies

Systemd handles dependencies at boot and runtime using:

### `Requires=`

Hard dependency. The service will not start unless the required unit is
active.

### `Wants=`

Soft dependency. systemd will attempt to start the dependency, but the
main service will still run even if the dependency fails.

### `After=`

Ordering rule. Ensures a service starts only after the specified unit
has started.\
(Does not imply dependency unless paired with Requires or Wants.)

------------------------------------------------------------------------

## 5. Common systemd Unit Types

Systemd relies on many unit types to manage the system:

### `.service`

Represents a long-running service managed by systemd (daemons).

### `.target`

Represents a boot stage or system state (e.g., multi-user.target,
graphical.target).

### `.timer`

Schedules and triggers services, replacing cron with a more reliable
system.

### `.mount`

Defines filesystem mount points.

### `.socket`

Handles socket-based activation for network or IPC services.

------------------------------------------------------------------------

## Summary

-   systemd manages the entire system lifecycle: booting, services,
    logs, dependencies and more.\
-   `systemctl` controls all systemd units.\
-   Unit files describe how services run and depend on each other.\
-   systemd supports many unit types including services, timers,
    targets, mounts and sockets.
