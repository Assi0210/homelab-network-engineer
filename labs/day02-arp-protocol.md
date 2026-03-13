# Day 2 - ARP Protocol

## Objective

Understand how devices resolve IP addresses to MAC addresses using ARP.

This lab demonstrates how a host discovers the MAC address of its gateway before sending packets.

---

## Network

Ubuntu Server  
IP: 10.10.30.5  
Interface: enp3s0

Gateway (pfSense OPT1)  
IP: 10.10.30.1

---

## Step 1 - Check ARP Table

Command

ip neigh

Result

10.10.30.1 dev enp3s0 lladdr 60:be:b4:29:8c:90 REACHABLE

Explanation

Ubuntu already knows the MAC address of the gateway and stores it in the ARP cache.

---

## Step 2 - Flush ARP Cache

Command

sudo ip neigh flush all

Check again

ip neigh

The ARP entry may appear again if the system communicates with the gateway.

---

## Step 3 - Generate ARP Request

Command

ping 10.10.30.1 -c 3

After ping, check ARP table again

ip neigh

Result

10.10.30.1 dev enp3s0 lladdr 60:be:b4:29:8c:90 REACHABLE

Explanation

Ubuntu sent an ARP request asking:

Who has 10.10.30.1?

pfSense replied with its MAC address.

---

## Step 4 - Check Local MAC Address

Command

ip a

Interface

enp3s0

MAC address

00:60:72:30:31:99

---

## Knowledge Learned

IP communication inside a LAN requires MAC addresses.

When a device only knows the IP address, it uses ARP to discover the MAC address.

The discovered MAC address is stored in the ARP cache.

This process is essential for Layer 2 communication in Ethernet networks.
