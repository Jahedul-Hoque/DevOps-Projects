# OpenSSH - A Complete Overview

This document explains what OpenSSH is, how SSH authentication works,
and how keys, known hosts and encrypted tunnels all fit together. It is
written as a foundational Linux and DevOps learning resource.

## 1. What Is OpenSSH?
 
OpenSSH is a secure method of remotely accessing a Linux endpoint. It
enables encrypted communication between a client and a server,
protecting data from interception, tampering or eavesdropping.

SSH is the modern and secure replacement for older protocols such as
Telnet.

## 2. SSH Key-Based Authentication

OpenSSH commonly uses public/private key authentication. This method
relies on a pair of cryptographic keys that together control access.

### Private Key

-   Stored locally on the client machine (the machine initiating the
    connection)

-   Found in the user's `.ssh` directory, typically:

        ~/.ssh/id_rsa
        ~/.ssh/id_ed25519

-   Must be kept secret and never shared

-   Used to prove identity to the server

### Public Key

-   Stored on the remote Linux machine you want to connect to

-   Added to the following file:

        ~/.ssh/authorized_keys

-   Can be shared freely

-   Used by the server to confirm that the connecting client has the
    matching private key

Authentication is only successful if the public key on the server
matches the private key stored on the client.

## 3. Public Key Formats

Public keys commonly begin with formats like:

    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ...
    ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIB...

These are found in the `.ssh` directory on the client system.

Linux:

    ~/.ssh/id_rsa.pub
    ~/.ssh/id_ed25519.pub

Windows (OpenSSH client):

    C:\Users\<Username>\.ssh\

## 4. SSH Encryption and Secure Tunnel

SSH establishes a fully encrypted tunnel between the client and server.
All communication that travels across this tunnel is encrypted,
providing confidentiality and integrity.

The SSH server (`sshd`) typically listens on:

    Port 22

This port can be changed, but 22 is the industry standard.

## 5. Known Hosts

The `.ssh` directory also contains a `known_hosts` file. This provides
an additional layer of security by verifying the identity of remote
machines.

### Purpose

When you connect to a server for the first time, SSH checks whether that
server's key exists in the known hosts file.

Each entry contains: 1. Hostname or IP address\
2. Key type (e.g., ssh-rsa, ssh-ed25519)\
3. Host key

### How It Works

-   If the server's signature is not present in the known hosts file,
    SSH warns that the identity is unknown.
-   The user must confirm whether they trust the server.
-   Once confirmed, the server's signature is added to the known hosts
    file.

This helps prevent man-in-the-middle attacks where someone attempts to
impersonate the server.

------------------------------------------------------------------------

## Summary

-   OpenSSH provides secure remote access to Linux systems.
-   Authentication uses a public/private key pair.
-   Private key stays on the client; public key sits in
    `authorized_keys` on the server.
-   SSH communication is encrypted through a secure tunnel, typically on
    port 22.
-   Known hosts verification protects against impersonation and
    interception.
