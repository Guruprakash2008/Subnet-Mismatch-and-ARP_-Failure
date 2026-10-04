# Subnet-Mismatch-and-ARP_-Failure
# Day 4 – Subnet Mismatch and ARP Failure

## 📌 Project Overview

This project demonstrates a **subnet mismatch** between two PCs connected through a switch in **Cisco Packet Tracer**.

The experiment shows how an incorrect subnet configuration can cause **ARP resolution failure and ping failure** in Simulation Mode.

## 🖥️ Network Topology

```text
PC0 ───────── 2960 Switch ───────── PC1
```

### Devices Used

* 2 PCs
* 1 Cisco 2960 Switch
* 2 Copper Straight-Through Cables
* No Router

---

## 🌐 Initial Configuration

### PC0

```text
IP Address:   192.168.10.10
Subnet Mask:  255.255.255.0
```

### PC1

```text
IP Address:   192.168.20.20
Subnet Mask:  255.255.255.0
```

The PCs are intentionally configured on **different subnets**.

```text
PC0 → 192.168.10.0/24
PC1 → 192.168.20.0/24
```

Since there is no router, communication between these different networks is not possible.

---

## 🔬 Simulation Procedure

### Step 1: Open Simulation Mode

Click **Simulation** at the bottom-right of Cisco Packet Tracer.

Or use:

```text
Shift + S
```

### Step 2: Configure Filters

Open **Edit Filters** and select only:

* ARP
* ICMP

### Step 3: Test Ping

Open:

**PC0 → Desktop → Command Prompt**

Run:

```text
ping 192.168.20.20
```

The ping fails because the destination is on a different subnet and there is no router.

---

## 🧪 ARP Failure Demonstration

To observe the ARP process, change the subnet mask of PC0 to:

```text
255.255.0.0
```

Keep PC1 as:

```text
IP Address:   192.168.20.20
Subnet Mask:  255.255.255.0
```

Now run:

```text
ping 192.168.20.20
```

Use **Capture/Forward** to observe the ARP packet.

The ARP request is broadcast through the switch, but the expected ARP reply is not received.

The ICMP packet remains waiting for MAC address resolution and eventually the ping fails.

---

## ❌ Problem Identified

The main problem is the **incorrect subnet configuration**.

PC0 and PC1 do not belong to the same subnet with their original `/24` masks.

```text
PC0 → 192.168.10.10/24
PC1 → 192.168.20.20/24
        ❌ Different Networks
```

---

## 🔧 Solution

Return to **Realtime Mode**.

Configure PC0:

```text
IP Address:   192.168.10.10
Subnet Mask:  255.255.255.0
```

Configure PC1:

```text
IP Address:   192.168.10.11
Subnet Mask:  255.255.255.0
```

Now both PCs belong to:

```text
192.168.10.0/24
```

---

## ✅ Final Ping Test

From PC0:

```text
ping 192.168.10.11
```

Expected result:

```text
Reply from 192.168.10.11: bytes=32 time<1ms TTL=128
```

This confirms successful communication between the two PCs.

---

## 🎯 Learning Objectives

This experiment helps understand:

* IP addressing
* Subnet masks
* Same-subnet communication
* ARP
* ICMP
* Packet Tracer Simulation Mode
* Packet drop analysis
* Basic network troubleshooting

## 📝 Conclusion

The experiment demonstrated that two directly connected PCs must be in the **same subnet** to communicate without a router. An incorrect subnet configuration can prevent successful ARP resolution and cause ping failure.

After correcting the IP addresses and subnet masks, communication was successfully established.

## 🛠️ Software Used

**Cisco Packet Tracer**

## 👨‍💻 Author

**Guruprakash K**

B.Tech – Computer Science and Business Systems
