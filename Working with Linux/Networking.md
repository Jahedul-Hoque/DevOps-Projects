# Linux Networking - Fundamentals and Troubleshooting

This document provides a structured overview of essential Linux
networking tools and troubleshooting methodology. It covers interface
inspection, IP addressing, routing, DNS, port inspection, packet
capture, system logging and diagnostic layers.

------------------------------------------

The best way to diagnose networking issues is to follow the OSI-inspired
layered method:

------------------------------------------------------------------------

### Layer 1: Physical Link

**Command:**

    ip link

Checks whether: - Interface is up\
- NIC is detected\
- Cable/physical signal exists

------------------------------------------------------------------------

### Layer 2: Ethernet / MAC

**Command:**

    ip addr

Checks whether: - IP address exists\
- DHCP assigned correctly\
- MAC address is correct

If DHCP failed → no IP address.

------------------------------------------------------------------------

### Layer 3: Routing

**Commands:**

    ip route
    traceroute <IP>

Checks: - Correct default gateway\
- Whether gateway is reachable\
- Whether packets leave LAN

If you can reach LAN but not outside → routing problem.

------------------------------------------------------------------------

### Layer 4: Connectivity

**Command:**

    ping <IP>

If ping fails on IP → not DNS, problem is network-level.\
If ping works on IP but not hostname → DNS issue.

------------------------------------------------------------------------

### Layer 5: DNS

**Commands:**

    dig google.com
    nslookup google.com

Checks: - Can hostnames resolve?\
- Are DNS servers correct?\
- Is systemd-resolved functioning?

------------------------------------------------------------------------

### Layer 6: Services & Ports

**Command:**

    ss -tulpn

### Meaning of flags:

-   ss → socket statistics\
-   t → TCP\
-   u → UDP\
-   l → listening sockets\
-   p → show processes\
-   n → numeric output

Checks: - Is the service listening?\
- Is the correct port open?\
- Is another program using the port?

------------------------------------------------------------------------

### Layer 7: Logs

**Command:**

    journalctl -u NetworkManager

Checks failures related to: - DHCP\
- Drivers\
- VLAN\
- Wi-Fi\
- Interface initialization

------------------------------------------------------------------------

## 5. Using Traceroute

### When to use:

-   External addresses cannot be reached\
-   Identify routing loops\
-   Diagnose firewall blocks\
-   Trace slow upstream hops

------------------------------------------------------------------------

## 6. Using tcpdump

`tcpdump` inspects raw packets on the network interface.

### What it tells you:

-   Whether packets hit the NIC\
-   DNS queries and responses\
-   If an issue is internal or external

Example: If you see DNS queries but no responses → firewall or DNS
server issue.

------------------------------------------------------------------------

## 7. What Is systemd-resolved?

systemd-resolved manages DNS configuration and resolution per interface.

Useful for: - Checking which DNS servers are being used\
- Debugging DNS failures

Commands:

    resolvectl
    journalctl -u systemd-resolved -xe

------------------------------------------------------------------------

## 8. DIG vs NSLookup

Both perform DNS lookups.

### DIG:

-   More detailed\
-   Preferred for troubleshooting

### NSLookup:

-   Quick and simple\
-   Works on Windows and Linux

------------------------------------------------------------------------

## Summary

-   Use `ip link`, `ip addr`, `ip route` for low-level diagnostics.\
-   Use `ss -tulpn` to inspect listening services.\
-   Use traceroute for upstream routing issues.\
-   Use tcpdump for packet inspection.\
-   Use dig/nslookup + systemd-resolved for DNS problems.\
-   Use journalctl for service-level debugging.