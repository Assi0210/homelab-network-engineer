# Day 1 - Basic Routing and Connectivity

## Objective

Understand how routing works between subnets using pfSense.

---

## Network

LAN subnet  
10.10.20.0/24

OPT1 subnet  
10.10.30.0/24

Router  
pfSense

---

## Lab Tasks

1. Verify routing table on Ubuntu
2. Test connectivity to gateway
3. Test routing between networks
4. Verify connectivity from pfSense

---

## Commands

Check routing table

ip route

Add default gateway

sudo ip route add default via 10.10.30.1

Ping gateway

ping 10.10.30.1

Ping pfSense LAN

ping 10.10.20.1

---

## Results

Ubuntu can reach:

10.10.30.1  
10.10.20.1

pfSense can reach:

10.10.30.5

---

## Knowledge Learned

Default gateway is required for communication between different networks.

Without default route the host cannot reach external subnets.

Routing is handled by pfSense between LAN and OPT1 networks.
