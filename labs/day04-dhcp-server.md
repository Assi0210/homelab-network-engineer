# HOMELAB JOURNAL
## Day 4 – Configure DHCP Server on pfSense

---

## Objective

Configure a DHCP server on pfSense to automatically assign IP addresses to clients in the LAN network.

The client should automatically receive:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server

---

## Lab Topology

```
                Internet
                    │
                    │
               pfSense
            WAN     LAN
             │       │
             │   10.10.30.1
             │       │
             │
        Ubuntu Client
        (DHCP Client)
```

Network configuration:

```
Network: 10.10.30.0/24
Gateway: 10.10.30.1
DHCP Pool: 10.10.30.100 – 10.10.30.200
```

---

## Step 1 – Enable DHCP Server on pfSense

Navigate to:

```
Services → DHCP Server
```

Enable DHCP on interface:

```
OPT1 / LAN
```

DHCP configuration:

```
Range Start : 10.10.30.100
Range End   : 10.10.30.200
Gateway     : 10.10.30.1
DNS Server  : default
```

Apply changes.

---

## Step 2 – DHCP Client Request

When the Ubuntu client connects to the network, the DHCP process occurs:

```
DHCP DISCOVER
DHCP OFFER
DHCP REQUEST
DHCP ACK
```

The DHCP server assigns an IP address from the configured pool.

---

## Step 3 – Verify IP Address on Ubuntu

Command:

```
ip a
```

Result:

```
inet 10.10.30.100/24 scope global dynamic enp3s0
```

Explanation:

```
dynamic → IP assigned by DHCP
```

---

## Step 4 – Verify Default Gateway

Command:

```
ip route
```

Result:

```
default via 10.10.30.1 dev enp3s0 proto dhcp
```

This confirms:

```
pfSense (10.10.30.1) is the gateway
```

---

## Step 5 – Verify DNS Configuration

Command:

```
cat /etc/resolv.conf
```

Result:

```
nameserver 127.0.0.53
search home.arpa
```

Ubuntu uses:

```
systemd-resolved
```

DNS queries flow through the local resolver first.

---

## Step 6 – Verify DHCP Lease on pfSense

Navigate to:

```
Status → DHCP Leases
```

Result:

```
IP Address : 10.10.30.100
Hostname   : minipc
MAC        : 00:60:72:30:31:99
```

This confirms the DHCP server successfully assigned an address.

---

## DHCP Address Allocation

Configured pool:

```
10.10.30.100 – 10.10.30.200
```

Assigned IP:

```
10.10.30.100
```

This is the first available address in the pool.

---

## Key Concepts Learned

DHCP automatically provides:

```
IP address
Subnet mask
Default gateway
DNS server
```

Benefits of DHCP:

```
Centralized IP management
Reduced configuration errors
Automatic address allocation
```

---

## Notes

pfSense shows a warning:

```
ISC DHCP has reached end-of-life
```

Future pfSense versions will migrate to:

```
Kea DHCP
```

---

## Result

```
DHCP Server: Working
IP Assignment: Successful
Gateway: Correct
Lease: Visible on pfSense
```

Lab Status:

```
SUCCESS
```

---
