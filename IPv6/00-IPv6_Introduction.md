# IPv6 Addresses

1. IPv6 addresses are written using **hexadecimal notation**, as opposed to dotted decimal in IPv4.

2. Because a hexadecimal digit represents 4 bits, an IPv6 address consists of **32 hexadecimal digits** (128 bits), compared to 32 bits in IPv4.

3. An IPv6 address uses **128 bits**.

4. These digits are grouped into **8 blocks of 4 hexadecimal digits** (16 bits each). The groups are separated by colons (`:`).

5. Example IPv6 address:
   `2001:0:9D38:6AB8:1C48:3A1C:A95A:B1C2`

6. The first **64 bits** are used for **network routing**, consisting of:

   * The first **48 bits** as the **Global Routing Prefix** (equivalent to a public network ID).
   * The next **16 bits** as the **Subnet ID**.

7. There are **four types of IPv6 addresses**:

   * **Global Unicast Address** – Internet-routable (public).
   * **Link-Local Address** – Used for communication within a link; not routed beyond the local link.
   * **Unique Local Address** – Routable internally (like IPv4 private addresses), not Internet-routable.
   * **Loopback Address** – `::1`, used for local testing like `127.0.0.1` in IPv4.

---

# A. Global and Public Addresses

Global addresses are routable on the Internet and typically start with **2000::/3** (commonly `2001::/16`).

* These are known as **Global Unicast Addresses**, equivalent to IPv4 public addresses.
* They are assigned by Internet authorities to ISPs, who allocate them to customers.

🔗 Reference: [IANA IPv6 Unicast Assignments](https://www.iana.org/assignments/ipv6-unicast-address-assignments/ipv6-unicast-address-assignments.xhtml)

---

# B. Internal Addresses – Link Local and Unique Local

In IPv4, internal addresses use these reserved ranges:

* `10.0.0.0/8`
* `172.16.0.0/12`
* `192.168.0.0/16`
* `169.254.0.0/16` (APIPA)

IPv6 has two internal address types:

1. **Link-Local**
2. **Unique Local**

---

## B-1. Link-Local Addresses

* Used for communication on the **same local link** (like ARP or routing protocols).
* Equivalent to IPv4 APIPA `169.254.0.0/16`.
* Always starts with the prefix `fe80::/10`.
* Not routable beyond the link.
* **Automatically assigned** by the operating system.
* **Mandatory** on every IPv6-enabled interface, even without a router.

> ✅ **Note:** Link-local is required and often used by routing protocols such as OSPFv3 and EIGRP for IPv6.

---

## B-2. Unique Local Addresses (ULA)

* Used within an organization or VPN.
* **Not routed on the Internet**.
* Equivalent to IPv4 private address ranges.
* Prefix: `fc00::/7` (commonly `fd00::/8` is used).

### FC00::/8 vs FD00::/8

| Prefix     | Intended Use                         | In Practice   |
| ---------- | ------------------------------------ | ------------- |
| `FC00::/8` | Centrally assigned (not implemented) | Not used      |
| `FD00::/8` | Locally assigned, pseudo-random      | Commonly used |

> Manual assignment of private IPv6 addresses should use the `fd00::/8` range.

**Example:**

```
FD00:1234:5678:9ABC:DEF0:1234:5678:9ABC
```

---

# IPv6 Addressing Scheme Example

```
2001:8003:500a:8001:e772:2e08:1def:7f8f
```

```
2001:0DB8:4545:0003:0200:F8FF:FE21:67CF
\__________/ \_/ \_____________________/
     A       B             C
```

* **A**: Routing Prefix (Global Routing Prefix)
* **B**: Subnet ID
* **C**: Interface ID

---

## Routing Prefix Sub-Schema

```
2001:0DB8:4545::/48
```

* `2001:0DB8` — From Internet registry.
* `xxxx:xxxx:4545` — Regional/Site allocation by ISP.

### Subnets from `2001:0DB8:4545::/48`

* First subnet: `2001:0DB8:4545:0000::/64`
* Last subnet: `2001:0DB8:4545:FFFF::/64`

There are **65,536** possible /64 subnets in a /48 prefix (`2^16`).

---

## Small End User Allocation Example — /60

* ISP allocates a **/60** prefix:

```
2001:ACAD:1234:1230::/60
```

* 60 bits for network = 4 bits for subnetting
* Allows for `2^4 = 16` /64 subnets

### Subnet Range:

* First subnet: `2001:ACAD:1234:1230::/64`
* Last subnet: `2001:ACAD:1234:123F::/64`

---

## What If Prefix Is Not a Multiple of 4 or 16?

Example:

```
2001:0DB8:4545:5003:0200:F8FF:FE21:67CF /53
```

* Prefix bits: `2001:0DB8:4545:5000::/53`
* Network mask ends in the middle of the 4th block.

---

# Example Subnetting with Unique Local Addressing

**Organization: Contoso Corp**

| Site      | IPv6 ULA Assignment     |
| --------- | ----------------------- |
| Sydney    | `FD6D:8D64:AF0C::/64`   |
| Melbourne | `FD6D:8D64:AF0C:1::/64` |
| Brisbane  | `FD6D:8D64:AF0C:2::/64` |
| Adelaide  | `FD6D:8D64:AF0C:3::/64` |

---
