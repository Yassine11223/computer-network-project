# Cisco Packet Tracer Computer Network Project

This repository contains a Cisco Packet Tracer computer network project for CSC230 Computer Networks.

The project focuses on designing, building, configuring, testing, and documenting a complete enterprise-style network using VLANs, VLSM, routing protocols, DHCP, NAT, IPsec VPN, wireless networking, and network management services.

## Project Information

* University: Misr International University
* Faculty: Faculty of Computer Science
* Course: CSC230 Computer Networks
* Project: Project S26
* Tool: Cisco Packet Tracer
* Team Leader: Yehia Mohammed Adel

## Project Objectives

The project is divided into the following parts:

1. Design and implement a VLSM addressing scheme.
2. Build the network and configure basic device settings and interface addressing.
3. Configure VLANs, trunking, inter-VLAN routing, and EtherChannel.
4. Configure routing protocols.
5. Configure a DHCP server.
6. Configure Dynamic NAT with PAT and Static NAT.
7. Configure network management features.
8. Configure and verify a site-to-site IPsec VPN.
9. Configure a wireless home router.
10. Verify connectivity.
11. Prepare documentation and handover files.

## Network Overview

The network includes:

* Main branch network
* S building network
* N building network
* R building network
* MIU gateway router
* ISP router
* Branch gateway router
* Wireless home router
* DHCP server
* Email server
* Web server
* DNS server
* NTP/Syslog server
* Wired and wireless clients

The network uses VLSM to divide the `10.0.0.0/8` address space into smaller subnets based on host requirements.

---

# VLSM Subnet Table

| Subnet          | VLAN ID | Required Hosts | Network Address/CIDR | First Usable | Last Usable | Broadcast  | Subnet Mask     |
| --------------- | ------: | -------------: | -------------------- | ------------ | ----------- | ---------- | --------------- |
| Main            |     110 |             61 | 10.0.0.0/26          | 10.0.0.1     | 10.0.0.62   | 10.0.0.63  | 255.255.255.192 |
| R               |     170 |             31 | 10.0.0.64/26         | 10.0.0.65    | 10.0.0.126  | 10.0.0.127 | 255.255.255.192 |
| Main            |     120 |             30 | 10.0.0.128/27        | 10.0.0.129   | 10.0.0.158  | 10.0.0.159 | 255.255.255.224 |
| N               |     160 |             29 | 10.0.0.160/27        | 10.0.0.161   | 10.0.0.190  | 10.0.0.191 | 255.255.255.224 |
| R               |     180 |             25 | 10.0.0.192/27        | 10.0.0.193   | 10.0.0.222  | 10.0.0.223 | 255.255.255.224 |
| S               |     140 |             20 | 10.0.0.224/27        | 10.0.0.225   | 10.0.0.254  | 10.0.0.255 | 255.255.255.224 |
| N               |     150 |             15 | 10.0.1.0/27          | 10.0.1.1     | 10.0.1.30   | 10.0.1.31  | 255.255.255.224 |
| S               |      25 |             12 | 10.0.1.32/28         | 10.0.1.33    | 10.0.1.46   | 10.0.1.47  | 255.255.255.240 |
| P2P: SW-S to GW |       - |              7 | 10.0.1.48/28         | 10.0.1.49    | 10.0.1.62   | 10.0.1.63  | 255.255.255.240 |
| P2P: Main to GW |       - |              2 | 10.0.1.64/30         | 10.0.1.65    | 10.0.1.66   | 10.0.1.67  | 255.255.255.252 |
| P2P: N to GW    |       - |              2 | 10.0.1.68/30         | 10.0.1.69    | 10.0.1.70   | 10.0.1.71  | 255.255.255.252 |
| P2P: S to GW    |       - |              2 | 10.0.1.72/30         | 10.0.1.73    | 10.0.1.74   | 10.0.1.75  | 255.255.255.252 |
| P2P: R to GW    |       - |              2 | 10.0.1.76/30         | 10.0.1.77    | 10.0.1.78   | 10.0.1.79  | 255.255.255.252 |

---

# Addressing Table

| Device   | Interface        | IP Address      | Subnet Mask     | VLAN |
| -------- | ---------------- | --------------- | --------------- | ---- |
| Main-MLS | VLAN 110         | 10.0.0.1        | 255.255.255.192 | 110  |
| Main-MLS | VLAN 120         | 10.0.0.129      | 255.255.255.224 | 120  |
| S-MLS    | VLAN 25          | 10.0.1.33       | 255.255.255.240 | 25   |
| S-MLS    | VLAN 140         | 10.0.0.225      | 255.255.255.224 | 140  |
| N-MLS    | VLAN 150         | 10.0.1.1        | 255.255.255.224 | 150  |
| N-MLS    | VLAN 160         | 10.0.0.161      | 255.255.255.224 | 160  |
| R-MLS    | VLAN 170         | 10.0.0.65       | 255.255.255.192 | 170  |
| R-MLS    | VLAN 180         | 10.0.0.193      | 255.255.255.224 | 180  |
| MIU-GW   | Gig0/1/0 to Main | 10.0.1.65       | 255.255.255.252 | -    |
| MIU-GW   | Gig0/3/0 to N    | 10.0.1.69       | 255.255.255.252 | -    |
| MIU-GW   | Gig0/1 to R      | 10.0.1.77       | 255.255.255.252 | -    |
| MIU-GW   | Gig0/2/0 to S    | 10.0.1.73       | 255.255.255.252 | -    |
| MIU-GW   | Gig0/0 to WAN    | 209.165.200.226 | 255.255.255.240 | -    |

---

# Host Address Table

| PC/Server         | VLAN ID | IP Address  | Subnet Mask     | Default Gateway |
| ----------------- | ------: | ----------- | --------------- | --------------- |
| PC-1              |     110 | 10.0.0.2    | 255.255.255.192 | 10.0.0.1        |
| PC-2              |     110 | 10.0.0.3    | 255.255.255.192 | 10.0.0.1        |
| PC-3              |     120 | 10.0.0.130  | 255.255.255.224 | 10.0.0.129      |
| PC-4              |      25 | 10.0.1.34   | 255.255.255.240 | 10.0.1.33       |
| PC-5              |      25 | 10.0.1.35   | 255.255.255.240 | 10.0.1.33       |
| PC-6              |     140 | 10.0.0.226  | 255.255.255.224 | 10.0.0.225      |
| PC-7              |     150 | 10.0.1.2    | 255.255.255.224 | 10.0.1.1        |
| PC-8              |     160 | 10.0.0.162  | 255.255.255.224 | 10.0.0.161      |
| PC-9              |     170 | 10.0.0.66   | 255.255.255.192 | 10.0.0.65       |
| PC-10             |     180 | 10.0.0.194  | 255.255.255.224 | 10.0.0.193      |
| PC-11             |       2 | 192.168.2.2 | 255.255.255.0   | 192.168.2.1     |
| PC-12             |       3 | 192.168.3.2 | 255.255.255.0   | 192.168.3.1     |
| DHCP Server       |       - | 10.0.1.50   | 255.255.255.240 | 10.0.1.49       |
| Email Server      |       - | 10.0.1.51   | 255.255.255.240 | 10.0.1.49       |
| Web Server        |       - | 10.0.1.52   | 255.255.255.240 | 10.0.1.49       |
| DNS Server        |       - | 10.0.1.53   | 255.255.255.240 | 10.0.1.49       |
| NTP/Syslog Server |       - | 10.0.1.54   | 255.255.255.240 | 10.0.1.49       |

---

# Required Project Tasks

## Part 1: VLSM Addressing Scheme

Design and implement a VLSM addressing scheme using the `10.0.0.0/8` network.

Tasks:

* Calculate subnets based on required hosts.
* Assign network addresses, first usable addresses, last usable addresses, broadcast addresses, and subnet masks.
* Fill in the subnet table.
* Fill in the device addressing table.
* Fill in the host addressing table.

## Part 2: Basic Device Settings and Interface Addressing

Configure basic settings on all routers and switches.

Required settings:

* Disable DNS lookup.
* Configure hostnames.
* Set minimum password length to 10 characters.
* Configure console password: `MIU1234567`
* Configure enable secret password: `CSC1234567`
* Encrypt all clear-text passwords.
* Configure an MOTD banner.
* Configure interface IP addresses according to the addressing table.
* Configure SSH on all routers.

Example basic commands:

```bash
enable
configure terminal
no ip domain-lookup
hostname DEVICE_NAME
security passwords min-length 10
enable secret CSC1234567
service password-encryption
banner motd #Unauthorized access is prohibited#

line console 0
password MIU1234567
login
exit
```

## Part 3: VLANs, Trunking, Inter-VLAN Routing, and EtherChannel

Tasks:

* Create VLANs on all switches.
* Configure access ports for PCs.
* Verify VLANs using:

```bash
show vlan brief
```

* Configure 802.1Q trunk links between switches.
* Configure SVI interfaces on multilayer switches.
* Configure routed ports between multilayer switches and MIU-GW.
* Configure router-on-a-stick subinterfaces on Branch-GW.
* Configure LACP EtherChannels as shown in the topology.
* Verify EtherChannel using:

```bash
show etherchannel summary
```

## Part 4: Routing Protocols

The network uses OSPF, EIGRP, static routes, default routes, and redistribution.

### OSPFv2

Configure OSPF process ID `100` on:

* MIU-GW
* Main-MLS
* S-MLS

Tasks:

* Configure router IDs.
* Advertise connected networks.
* Configure passive interfaces for LAN interfaces.
* Configure MIU-GW to propagate a default route.
* Verify using:

```bash
show ip ospf neighbor
show ip protocols
show ip route ospf
```

### EIGRP

Configure EIGRP AS number `10` on:

* MIU-GW
* N-MLS
* R-MLS

Tasks:

* Advertise connected networks.
* Configure passive interfaces for LAN interfaces.
* Verify using:

```bash
show ip eigrp neighbors
show ip protocols
show ip route eigrp
```

### Redistribution

Configure redistribution between OSPF and EIGRP.

Tasks:

* Redistribute OSPF routes into EIGRP.
* Redistribute EIGRP routes into OSPF.
* Verify full network convergence.

### Static and Default Routes

Tasks:

* Configure default routes on MIU-GW and Branch-GW pointing to ISP.
* Configure static routes on ISP pointing to MIU-GW, Branch-GW, and the home network.

## Part 5: DHCP Server

### Main Branch DHCP

Configure the DHCP server to provide IP addresses for:

* VLAN 110
* VLAN 120
* VLAN 25
* VLAN 140

Tasks:

* Exclude the first three usable addresses from each pool.
* Assign IP address, default gateway, and DNS server.
* Configure Main-MLS and S-MLS as DHCP relay agents.
* Test DHCP on PC1, PC2, PC3, PC4, PC5, and PC6.

### Branch-GW DHCP

Configure Branch-GW as a DHCP server for:

* VLAN 2
* VLAN 3

Tasks:

* Exclude the first five usable addresses from each pool.
* Create DHCP pools named `B-LAN2` and `B-LAN3`.
* Configure network address, default gateway, and DNS server.
* Verify DHCP and connectivity.

## Part 6: NAT

Configure NAT on MIU-GW.

Tasks:

* Configure Dynamic NAT with PAT.
* Use the third address from `209.165.200.224/28` as the public PAT address.
* Configure Static NAT for the `miu.edu.eg` web server.
* Use the fourth address from `209.165.200.224/28` for static NAT.
* Configure inside and outside NAT interfaces.
* Verify NAT translations.

Verification commands:

```bash
show ip nat translations
show ip nat statistics
```

## Part 7: Network Management Features

### NTP and Syslog

Tasks:

* Configure all devices to use the NTP/Syslog server.
* Verify time synchronization.
* Verify Syslog messages.

### DNS Server

Configure DNS records:

| Domain Name      | Target Server   |
| ---------------- | --------------- |
| miu.edu.eg       | Web Server IP   |
| email.miu.edu.eg | Email Server IP |

Verify using:

```bash
ping miu.edu.eg
ping email.miu.edu.eg
nslookup miu.edu.eg
nslookup email.miu.edu.eg
```

### Email Server

Configure the email server:

* Domain: `email.miu.edu.eg`
* Enable SMTP.
* Enable POP3.

Create users:

| Username | Password |
| -------- | -------- |
| user1    | cs1      |
| user2    | cs2      |

Test email:

* Send email from user1 to user2.
* Send email from user2 to user1.
* Verify delivery.

### Web Server

Tasks:

* Configure the web server.
* Set website domain to `miu.edu.eg`.
* Add the MIU logo to the homepage.
* Test from PC1, PC7, PC9, PC11, and the laptop.

## Part 8: Site-to-Site IPsec VPN

Tasks:

* Verify connectivity before VPN configuration.
* Configure site-to-site IPsec VPN between MIU-GW and Branch-GW.
* Verify VPN tunnel operation.
* Test secure communication between sites.

## Part 9: Wireless Home Router

Configure the wireless home router.

Wireless settings:

| Setting       | Value         |
| ------------- | ------------- |
| SSID          | MIU-CSC230    |
| Frequency     | 2.4 GHz       |
| Security Mode | WPA2 Personal |
| Encryption    | AES           |
| Passphrase    | miu_csc230    |

Tasks:

* Configure the wireless router.
* Connect the laptop, tablet, and smartphone.
* Test wireless connectivity.

## Part 10: Verification

Verify connectivity between all devices.

Required evidence:

* Ping tests between devices.
* Screenshots of ping tests.
* IP interface information for each device.
* Routing table for each router and multilayer switch.
* Traceroute tests from different PCs.

Useful commands:

```bash
show ip interface brief
show vlan brief
show interfaces trunk
show ip route
show ip protocols
show cdp neighbors
show cdp neighbors detail
show etherchannel summary
show spanning-tree
show running-config
ping
tracert
```

## Part 11: Documentation and Handover

Prepare final documentation in DOCX or PowerPoint format.

The documentation should include:

* Network topology.
* VLSM table.
* Addressing table.
* Host addressing table.
* Device configurations.
* DHCP configuration.
* NAT configuration.
* OSPF and EIGRP configuration.
* Redistribution configuration.
* VPN configuration.
* Wireless router configuration.
* DNS, Email, Web, NTP, and Syslog configuration.
* Ping and traceroute screenshots.
* Routing table screenshots.
* Troubleshooting steps if any issues occurred.

---

# Suggested Repository Structure

```text
computer-network-project/
├── README.md
├── packet-tracer/
│   └── network-project.pka
├── docs/
│   ├── Tables(updatedv2).pdf
│   ├── Command Guide.pdf
│   └── project-requirements.txt
├── configs/
│   ├── Main-MLS.txt
│   ├── S-MLS.txt
│   ├── N-MLS.txt
│   ├── R-MLS.txt
│   ├── MIU-GW.txt
│   ├── ISP.txt
│   └── Branch-GW.txt
├── screenshots/
│   ├── ping-tests/
│   ├── routing-tables/
│   └── services-tests/
└── tests/
    └── verification-commands.md
```

---

# Final Notes

* The project should be tested inside Cisco Packet Tracer.
* All devices must follow the latest addressing table.
* The final submission should include configuration files, screenshots, and documentation.
* Connectivity should be verified between internal VLANs, branch networks, servers, WAN links, and wireless clients.

