# MAC Address

MAC stands for Media Access Control — also called a Hardware Address or 
Physical Address.

A MAC address is assigned to the NIC (Network Interface Card) of a laptop, 
computer, or other network device, generally by the manufacturer/vendor of 
the network interface.

## Structure
A MAC address is 48 bits long, normally represented in hexadecimal, and 
divided into two parts of 24 bits each:

- **First 24 bits — OUI (Organizationally Unique Identifier):** identifies 
  the organization/manufacturer associated with the MAC address. Vendors 
  obtain OUIs through **IEEE** (the IEEE Registration Authority).
- **Remaining 24 bits:** used to create individual MAC addresses for that 
  vendor's devices.

Since 24 bits allow 2²⁴ possible combinations, a single OUI provides a 
limited number of unique identifiers — if a vendor needs more, it obtains 
another OUI.

## MAC Address & Identification
If a device is involved in a security incident, its IP address may help 
identify it on the network. On a local network, the IP address can be 
associated with the device's MAC address using mechanisms like **ARP**.

The first 24 bits (OUI) can indicate the organization/manufacturer 
associated with a MAC address. However, the MAC address itself normally 
does **not** directly reveal the individual person who owns the device — 
manufacturers generally don't provide a public record linking a MAC address 
to a specific customer.

**Important note:** MAC addresses can sometimes be changed or spoofed, so a 
MAC address should not be treated as a permanent way to identify or track a 
person.
