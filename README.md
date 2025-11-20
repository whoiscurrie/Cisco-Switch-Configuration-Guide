# Cisco Switch Configuration Guide

A comprehensive collection of Cisco switch configuration commands and best practices for real-world networking.

## 📋 Overview

This guide contains essential configuration commands and verification steps for Cisco switches, covering fundamental networking concepts required for practical network administration.

**Purpose**: Core setup and verification commands for Cisco switches

## 🎯 Topics Covered

- **Basic Configuration** - Hostname, passwords, banners, and management interface setup
- **Port Security** - Protect switch ports from unauthorized access and MAC flooding
- **VLAN Configuration** - Network segmentation for improved security and traffic management
- **Trunk Configuration** - Inter-switch VLAN communication using 802.1Q
- **VTP (VLAN Trunking Protocol)** - Centralized VLAN management across switches
- **STP (Spanning Tree Protocol)** - Loop prevention and network redundancy
- **SSH Setup** - Secure remote access configuration
- **Verification Commands** - Essential commands to validate your configurations

---

## 🚀 Basic Configuration

Start by setting the hostname, securing passwords, encrypting them, adding a login banner, and saving your configuration to ensure persistence after reboot.

```cisco
hostname SW1                          # Set switch hostname
enable secret cisco                   # Secure privileged exec mode with encrypted password
service password-encryption           # Encrypt all plaintext passwords in config
banner motd # UNAUTHORIZED ACCESS IS PROHIBITED #   # Display legal warning on login
interface vlan 1                      # Enter VLAN 1 interface (default management VLAN)
ip address 172.16.1.1 255.255.255.0   # Assign static IP address
no shutdown                           # Enable the interface
copy running-config startup-config    # Save current config to NVRAM
```

---

## 🔒 Port Security

Enhance network protection by limiting the number of devices that can connect to a switch port. This helps prevent unauthorized access and MAC flooding attacks.

```cisco
interface fastEthernet 0/x           # Replace x with actual port number
switchport port-security             # Enable port security
switchport port-security maximum 2   # Allow max 2 MAC addresses
switchport port-security violation restrict  # Restrict traffic if violation occurs
switchport port-security mac-address sticky  # Learn and save MAC addresses automatically
```

---

## 🏢 VLAN Configuration

Create VLANs to logically segment your network — for example, separating HR, Sales, and Admin departments. This improves efficiency, security, and traffic management.

```cisco
vlan 10                               # Create VLAN 10
name Sales                            # Name the VLAN
interface fastEthernet 0/1           # Enter interface config mode
switchport mode access                # Set port to access mode
switchport access vlan 10            # Assign port to VLAN 10
```

---

## 🔗 Trunk Configuration

Enable trunk links between switches to allow multiple VLANs to pass through a single connection. It's essential for inter-switch communication in larger networks.

```cisco
interface fastethernet 0/1           # Trunk port between switches
switchport mode trunk                # Enable trunking
switchport trunk encapsulation dot1q # Use 802.1Q encapsulation
switchport trunk allowed vlan add 10 # Allow VLAN 10 on trunk
```

---

## 🌐 VTP Configuration

Simplify VLAN management across multiple switches by using VTP. It ensures VLAN information is consistent throughout your network.

```cisco
vtp mode server                      # Set VTP mode (server/client/transparent)
vtp domain ABC                      # Set VTP domain name
vtp password Cisco                   # Set VTP password (case-sensitive)
vtp version 2                        # Use VTP version 2
show vtp status                      # Verify VTP settings
```

---

## 🌳 STP (Spanning Tree Protocol)

Prevent network loops and ensure redundancy by configuring STP. It keeps your topology stable and your network resilient.

### STP Verification Commands

```cisco
show spanning-tree                   # View STP status for all VLANs
show spanning-tree vlan 1            # View STP for VLAN 1
show spanning-tree vlan 1 root       # Show root bridge info
show spanning-tree vlan 1 bridge     # Show local bridge info
debug spanning-tree events           # Monitor STP topology changes
```

---

## 🔐 SSH Setup (Secure Remote Access)

Configure SSH for secure remote management of your switch. This is more secure than Telnet.

```cisco
ip domain-name mydomain.com          # Set domain name for SSH key generation
crypto key generate rsa              # Generate RSA key (choose 1024 bits or higher)
username admin password cisco        # Create local user for SSH login
line vty 0 15                        # Configure virtual terminal lines
login local                          # Use local login database
transport input ssh                  # Enable SSH only (disable Telnet)
```

### Optional: Disable Telnet

```cisco
transport input telnet ssh           # Allow both (use 'ssh' only to disable Telnet)
```

---

## ✅ Verification Commands

Always verify your setup — check VLANs, trunk ports, port security status, VTP domain, and spanning-tree operations. Verification helps ensure everything is working as expected.

```cisco
show vlan brief                      # List VLANs and port assignments
show interfaces trunk                # Show trunk port status
show interfaces fastethernet 0/1 switchport  # Show switchport details
show mac address-table               # View MAC address table
show running-config                  # View current config
show startup-config                  # View saved config
show vtp status                      # Confirm VTP domain and mode
show cdp neighbors                   # View directly connected Cisco devices
show cdp neighbors detail            # Detailed info on CDP neighbors
```

---

## 📚 Learning Path

1. Start with **Basic Configuration** to secure and prepare your switch
2. Implement **Port Security** to protect individual ports
3. Create **VLANs** for network segmentation
4. Configure **Trunks** for inter-switch communication
5. Set up **VTP** for efficient VLAN management
6. Understand **STP** for network stability
7. Enable **SSH** for secure remote access

---

## ⚠️ Important Notes

- Always save configurations with `copy running-config startup-config`
- Use `service password-encryption` to protect passwords
- Test configurations in a lab environment before production deployment
- Keep backup copies of working configurations
- Document changes and maintain change logs

---

## 🛠️ Prerequisites

- Cisco switch (physical or Packet Tracer/GNS3)
- Console cable or SSH access
- Basic understanding of networking concepts
- Familiarity with Cisco IOS command-line interface



**⭐ If you find this guide helpful, please consider giving the repository a star!**

*Mastering these switch configurations will prepare you for real-world networking success!*

---

