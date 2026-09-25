# IP Address — Complete Explanation

An IP address is 32 bits long, written in dotted-decimal notation, and 
consists of 4 octets. Each octet can hold a value from 0 to 255 (max value 
255).

## Classes of IP Addresses
IP addresses are divided into five classes:

| Class | Range   | Use |
|-------|---------|-----|
| A     | 0–127   | Unicast |
| B     | 128–191 | Unicast |
| C     | 192–223 | Unicast |
| D     | 224–239 | Multicast |
| E     | 240–255 | Experimental/research |

### How to Identify the Class
Look at the first octet.

Example: **10.11.12.13** → first octet is 10 → falls between 0–127 → 
**Class A**.

## Subnet Mask
A subnet mask tells us which part of an IP address is the network portion 
and which part is the host portion.

- **1s** = network portion
- **0s** = host portion

### Default Subnet Masks
| Class | Default Subnet Mask |
|-------|---------------------|
| A     | 255.0.0.0           |
| B     | 255.255.0.0         |
| C     | 255.255.255.0       |

## Finding the Network ID

**Manual method:**
1. Convert the IP address to binary
2. Identify its class
3. Take the default subnet mask for that class
4. Convert the subnet mask to binary
5. Perform a bitwise AND between the IP and subnet mask
6. Convert the result back to decimal → this is the Network ID

**Short method (no binary needed):**
- **Class A:** keep 1st octet, rest become 0
  → `10.11.12.13` → Network ID = `10.0.0.0`
- **Class B:** keep first 2 octets, rest become 0
  → `172.168.10.10` → Network ID = `172.168.0.0`
- **Class C:** keep first 3 octets, last becomes 0
  → `223.10.10.11` → Network ID = `223.10.10.0`

**One-line concept:** To find the Network ID, keep the network portion of 
the IP address the same and change the host portion to 0.