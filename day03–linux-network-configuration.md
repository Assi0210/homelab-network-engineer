# HOMELAB JOURNAL
## Day 3 – Linux Network Configuration

---

## Objective

Configure a static IP address on an Ubuntu server and verify network connectivity with the pfSense router.

Goals:

- Configure static IP using Netplan
- Define default gateway
- Verify routing table
- Test connectivity to the network gateway

---

## Lab Topology

```
                pfSense
            WAN        LAN
             │          │
             │      10.10.30.1
             │          │
             │
        Ubuntu Server
        10.10.30.5
```

Network configuration:

```
Network: 10.10.30.0/24
Gateway: 10.10.30.1
Ubuntu IP: 10.10.30.5
```

---

## Step 1 – Configure Static IP with Netplan

Edit the netplan configuration file:

```
sudo nano /etc/netplan/00-installer-config.yaml
```

Configuration:

```yaml
network:
  version: 2
  ethernets:
    ens18:
      dhcp4: no
      addresses:
        - 10.10.30.5/24
      routes:
        - to: default
          via: 10.10.30.1
```

Apply configuration:

```
sudo netplan apply
```

---

## Step 2 – Verify IP Address

Command:

```
ip a
```

Expected output:

```
inet 10.10.30.5/24
```

This confirms the static IP configuration was applied.

---

## Step 3 – Verify Routing Table

Command:

```
ip route
```

Expected result:

```
default via 10.10.30.1
10.10.30.0/24 dev ens18
```

Explanation:

```
default via 10.10.30.1 → pfSense gateway
```

---

## Step 4 – Test Network Connectivity

Ping the gateway:

```
ping 10.10.30.1
```

Expected result:

```
64 bytes from 10.10.30.1
```

Successful replies confirm the server can communicate with the router.

---

## Key Concepts Learned

Static IP configuration ensures that the server always uses the same address.

Components of a static network configuration:

```
IP address
Subnet mask
Default gateway
```

Default gateway allows the host to reach external networks.

---

## Notes

Netplan is the default network configuration tool in modern Ubuntu systems.

Netplan configuration files are stored in:

```
/etc/netplan/
```

Changes require applying:

```
sudo netplan apply
```

---

## Result

```
Static IP configured successfully
Routing table verified
Connectivity with pfSense confirmed
```

Lab Status:

```
SUCCESS
```

---
