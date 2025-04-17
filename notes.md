# Switch Interfaces

---

## show ip interface brief

This command gives you a simple, summarized view of all interfaces on a switch or router.

You’ll see a table like this:

| Interface | IP-Address | OK? | Method | Status | Protocol |
|-----------|------------|-----|--------|--------|----------|

**Interface** – The name of the interface, like `FastEthernet0/1` or `GigabitEthernet1/0/2`  
**IP-Address** – Shows any IP assigned to the interface (only used on Layer 3 interfaces)  
**OK?** – If the hardware is working correctly (usually always says "YES")  
**Method** – How the IP address was assigned (manual, DHCP, etc.)  
**Status** – Whether the port is administratively up or down  
**Protocol** – If the protocol is running (like if the port is connected and working)

---

## Switch vs Router Default Interface State

**Switch interfaces** are **enabled by default**, so they come up automatically when something is plugged in.

**Router interfaces** are **administratively down by default**, which means you have to manually enable them with `no shutdown`.

---

## shutdown & no shutdown

Used in interface configuration mode:

- `shutdown` puts the interface in an **administratively down** state.
- `no shutdown` brings it back **up**.

---

## interface [type/number]

To enter interface config mode for a specific interface:

```
Switch(config)# interface fastEthernet0/1
```

You can also configure multiple interfaces at once using a **range**:

```
Switch(config)# interface range fastEthernet0/1 - 24
```

This is useful when applying the same settings to many ports.

---

## Speed & Duplex

Each interface can have a **speed** and **duplex** setting:

```
speed 100         → Sets speed to 100 Mbps  
duplex full       → Sets to full-duplex (send and receive at the same time)
```

- **Speed** defines how fast the link can transfer data.
- **Duplex** determines if both devices can talk at once or take turns.

---

## Auto-Negotiation

By default, interfaces try to auto-negotiate both **speed** and **duplex**.

If both ends support this, it usually works fine.  
If one side is set manually and the other is set to auto, **mismatches** may happen — like one side running half-duplex and the other full. That causes **collisions and errors**.

---

## CSMA/CD

**Carrier Sense Multiple Access with Collision Detection**

Used when devices are in **half-duplex** mode (like on old hubs).  
If both devices can talk at once (**full-duplex**), CSMA/CD is not used.

---

## Interface Errors

Use this command to see interface error details:

```
show interfaces fastEthernet0/1
```

Common error fields:

---

### Runts

Frames that are **smaller than 64 bytes**. Usually caused by collisions or bad cabling.

---

### Giants

Frames **larger than the max allowed size**, usually 1518 bytes. Can happen due to jumbo frames or NIC misbehavior.

---

### CRC

CRC = **Cyclic Redundancy Check** errors.  
The frame was received, but its checksum didn’t match = **corrupted data**.  
Common causes: bad cables, interference, duplex mismatch.

---

### Frame

Non-CRC errors like misaligned frames or physical-layer problems.  
May indicate timing or cabling issues.

---

### Input Errors

**All incoming problems** – includes CRC, runts, giants, alignment errors, etc.  
If high, it’s likely a receive-side issue.

---

### Output Errors

**Sending-side problems** – includes late collisions, excessive traffic, software bugs, buffer issues.  
These are less common but serious when they appear.

---

Understanding switch interfaces and their settings is critical to troubleshooting.  
Always double-check interface states, speed/duplex settings, and monitor errors during setup.
