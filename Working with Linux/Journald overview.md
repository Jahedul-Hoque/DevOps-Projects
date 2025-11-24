 # Understanding journald and journalctl

`journald` is the logging component of systemd, responsible for
collecting, storing and indexing logs from services, the kernel, and
system components. It provides powerful filtering, structured logs, and
precise timestamps that make troubleshooting significantly easier.

------------------------------------------------------------------------

## 1. What Is journald?

-   journald automatically captures logs from:
    -   System services
    -   The Linux kernel
    -   User sessions
    -   Authentication attempts
    -   Network and SSH components
-   Logs are stored in a structured, indexed format.
-   Logs are timestamped precisely.
-   Logs can be filtered by:
    -   Service
    -   Severity level
    -   Boot session
    -   Time ranges
    -   Real-time streaming

This makes journald far more capable than traditional plain-text logging
systems.

------------------------------------------------------------------------

## 2. Core journalctl Commands

Below are essential commands for troubleshooting with journald.

------------------------------------------------------------------------

### `journalctl -u <service>`

Shows logs for a specific systemd unit.

Example:

    journalctl -u ssh

Use when: - A service is failing - Authentication or SSH is broken - A
daemon is not starting or stopping correctly

------------------------------------------------------------------------

### `journalctl -u ssh -xe`

Shows recent logs with explanations.

Flags: - `-x` → explanations for log entries - `-e` → jump to the latest
logs

Use when: - A service is broken and you want detailed hints - Diagnosing
missing directories, permission issues, port conflicts, or dependency
failures

------------------------------------------------------------------------

### `journalctl -f -u <service>`

Follows logs live.

Example:

    journalctl -f -u ssh

Use when: - Debugging a service during startup - Reproducing a user
issue in real-time - Catching errors as they occur

------------------------------------------------------------------------

### `journalctl -b`

Shows logs from **the current boot only**.

Use when: - Troubleshooting issues that occur during startup -
Diagnosing mount failures, storage errors, or network issues after
reboot

------------------------------------------------------------------------

### `journalctl -p 0..7`

Filters logs by severity level.

Levels:

    0 = emergency
    1 = alert
    2 = critical
    3 = error
    4 = warning
    5 = notice
    6 = info
    7 = debug

Use when: - Logs are noisy and you only want to see serious problems

------------------------------------------------------------------------

### `journalctl --since "10 minutes ago"`

Filters logs by time.

Use when: - An issue happened recently (e.g., past 10 minutes, 1 hour,
etc.) - You need to locate specific events

------------------------------------------------------------------------

## 3. Troubleshooting With journalctl: NetworkManager Example

Use:

    journalctl -u NetworkManager

To diagnose: - Server not receiving an IP address - Network not coming
up after reboot - DNS issues - DHCP not assigning addresses - Wi-Fi
authentication problems - Interface up/down events

This command is essential for debugging connectivity problems.

------------------------------------------------------------------------

## Summary

-   journald collects structured, indexed logs for the entire system.
-   journalctl allows filtering by service, severity, time and boot
    session.
-   It is one of the most powerful tools for Linux troubleshooting.
-   Use it for SSH issues, network failures, service crashes, boot
    problems and more.