# IPv4 Static Routing and Network Troubleshooting Lab

## Project Overview

This hands-on Cisco Packet Tracer lab demonstrates IPv4 network configuration, static routing, routing table analysis, connectivity verification, and systematic network troubleshooting.

Completed as part of my preparation for the Cisco CCNA 200-301 certification, specifically Domain 3.3 — IP Connectivity.

## Technologies Used

- Cisco Packet Tracer 9.0.1
- Cisco IOS CLI
- Cisco 1941 Routers
- IPv4 Addressing and Subnetting
- Static Routing
- ICMP
- ARP

## Network Topology

PC1 — R1 — R2 — PC2

| Device | Interface | IP Address | Prefix |
|---|---|---|---|
| PC1 | Fa0 | 192.168.1.10 | /24 |
| R1 | G0/0 | 192.168.1.1 | /24 |
| R1 | G0/1 | 10.0.0.1 | /30 |
| R2 | G0/1 | 10.0.0.2 | /30 |
| R2 | G0/0 | 192.168.2.1 | /24 |
| PC2 | Fa0 | 192.168.2.10 | /24 |

## Routing Configuration

R1 — Network Static Route:

`ip route 192.168.2.0 255.255.255.0 10.0.0.2`

R2 — Default Static Route:

`ip route 0.0.0.0 0.0.0.0 10.0.0.1`

These configurations establish forward and return routing between the two LANs.

## Troubleshooting Incident

**Problem:** PC2 experienced 100% packet loss when attempting to ping R1's transit interface at 10.0.0.1.

**Troubleshooting methodology:**

1. Repeated the ping to rule out an initial ARP-related timeout.
2. Verified R1's static route using `show ip route`.
3. Confirmed R2's default route was correctly configured.
4. Tested direct router-to-router connectivity, achieving a 100% success rate.
5. Isolated the issue to the end-device configuration.
6. Inspected PC2's IPv4 settings and identified the root cause.

**Root cause:** PC2's default gateway address had been incorrectly entered into the DNS server field, leaving the default gateway unconfigured.

**Resolution:** Configured the correct default gateway of 192.168.2.1 and cleared the incorrect DNS entry.

**Result:** Successfully restored connectivity from PC2 to R1 and PC1.

## Cisco IOS Commands Practiced

- `enable`
- `configure terminal`
- `hostname`
- `interface gigabitEthernet`
- `ip address`
- `no shutdown`
- `ip route`
- `show ip interface brief`
- `show ip route`
- `ping`
- `copy running-config startup-config`

## Key Takeaways

- Physical connectivity does not guarantee end-to-end communication.
- Successful bidirectional communication requires forward and return routing.
- Default routes handle destinations without a more specific matching route.
- End-device misconfigurations can cause connectivity failures even when router configurations are correct.
- Systematic troubleshooting helps isolate problems without making unnecessary configuration changes.

## Project Status

Completed — IPv4 static routing configured, verified, and successfully troubleshot.

## Next Steps

- IPv6 static routing
- IPv4 and IPv6 host routes
- Floating static routes and failover
- Single-area OSPFv2
