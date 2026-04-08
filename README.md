# Aruba AOS-CX Syntax Highlighter for VS Code

A VS Code extension providing comprehensive syntax highlighting for Aruba AOS-CX switch configuration files.

## Features

Highlights the following AOS-CX configuration constructs:

### Interface Declarations
- Physical interfaces (`interface 1/1/1`, sub-interfaces `1/1/1.100`)
- VLAN interfaces (`interface vlan 10`)
- LAG interfaces (`interface lag 1`)
- Loopback interfaces (`interface loopback 0`)
- Tunnel interfaces (`interface tunnel 1`)
- VXLAN interfaces (`interface vxlan 1`)
- Management interface (`interface mgmt`)

### Switching
- VLAN declarations and ranges
- Access/trunk/native VLAN mode
- Spanning tree (MSTP/RSTP/RPVST) configuration
- LACP mode and LAG membership
- LLDP parameters
- Storm control
- Private VLANs
- ARP inspection / DHCP snooping
- IGMP/MLD snooping

### Routing
- OSPF / OSPFv3 (process, area, cost, timers, passive-interface, graceful-restart)
- BGP (AS number, neighbor, peer-group, address-family, l2vpn-evpn, route-reflector)
- RIP
- Static routes (`ip route`, `ipv6 route`)
- Route maps, prefix lists, community lists and their sub-commands
- VRF definitions with RD/RT values
- BFD (Bidirectional Forwarding Detection)

### VXLAN / EVPN / NVO (NEW in v1.1.0)
- `interface vxlan` declarations with VNI mappings
- NVO (Network Virtualization Overlay) blocks
- EVPN configuration with RD/RT auto and explicit values
- VTEP, flood-list, arp-suppression, nd-suppression
- Type-2 / Type-5 routes, symmetric/asymmetric IRB
- Route Distinguisher / Route Target values (ASN:NN format)

### VSX (NEW in v1.1.0)
- VSX block declaration
- inter-switch-link, keepalive, system-mac, role
- linkup-delay-timer, split-recovery
- vsx-sync, active-gateway (IP and MAC)

### ACLs & Security
- ACL declarations (`access-list ip|ipv6|mac`)
- Permit / deny entries with protocol, ports, wildcards
- Port-access policies (802.1X, MAC-auth) with full sub-commands
- Port-access roles
- AAA (RADIUS, TACACS+) server definitions
- User/password/secret/ciphertext
- Captive portal profiles (NEW in v1.1.0)
- User roles (NEW in v1.1.0)

### QoS
- Class-map and policy-map declarations
- DSCP/CoS/dot1p values (af11-af43, cs0-cs7, ef, be)
- Police, shape, queue, bandwidth actions
- Queue profiles and schedule profiles
- QoS trust mode
- CoPP (Control Plane Policing) (NEW in v1.1.0)

### DHCP (NEW in v1.1.0)
- DHCP server pool declarations
- Range, default-router, dns-server, lease, options
- DHCP relay
- DHCP server VRF binding

### Network Protection (NEW in v1.1.0)
- Loop-protect
- UDLD
- IPv6 ND / RA guard
- DHCPv6 guard

### Monitoring (NEW in v1.1.0)
- Mirror sessions (source, destination)
- Scheduler jobs and schedules

### System
- Hostname
- NTP, DNS, logging, SNMP (v1/v2c/v3)
- Banner blocks (motd, login, exec) with multi-line support
- IP helper-address
- HTTPS / REST API / SSH service
- Hardware and system resource keywords

### Values
- IPv4 addresses (with CIDR and dotted subnet masks)
- IPv6 addresses with prefix length
- MAC addresses (colon, dot, and dash notation)
- Physical port identifiers (`slot/port/subport`)
- VLAN ranges (`10,20,30-40`)
- OSPF area IDs in dotted notation
- Route Distinguisher / Route Target values (`65000:100`)
- Description text (scoped as string)

### Comments
- `!` line comments
- `#` line comments

### Folding
- Section folding on block declarations (interface, vlan, router, vsx, evpn, etc.) terminated by `!`

## File Association

The extension activates on:
- `.aoscx` files
- `.aoscxcfg` files
- Files whose first line matches common AOS-CX config patterns

To use with `.cfg` or `.txt` files, select **Aruba AOS-CX** from the language picker in VS Code (bottom right status bar).

## Installation

### From VSIX (recommended)
1. Download `aruba-cx-syntax-1.1.0.vsix`
2. In VS Code: `Extensions` → `...` → `Install from VSIX...`
3. Select the downloaded file

### From source
```bash
git clone https://github.com/SThomson29/aruba-cx-syntax
cd aruba-cx-syntax
npm install -g @vscode/vsce
vsce package
code --install-extension aruba-cx-syntax-1.1.0.vsix
```

## Development

Grammar file: `syntaxes/aruba-cx.tmLanguage.json`

To test grammar changes, open the extension source in VS Code and press `F5` to launch an Extension Development Host.

Use **Developer: Inspect Editor Tokens and Scopes** (`Ctrl+Shift+P`) to debug scope assignments on specific tokens.

## Changelog

### 1.1.0
- Added VXLAN / EVPN / NVO support (interface vxlan, evpn block, nvo, VNI, VTEP, arp/nd-suppression)
- Added VSX support (vsx block, inter-switch-link, keepalive, system-mac, role, split-recovery)
- Added VRF top-level declarations with RD/RT values
- Added DHCP server pool declarations and sub-commands
- Added CoPP (Control Plane Policing) support
- Added BFD (Bidirectional Forwarding Detection) keywords
- Added mirror session declarations
- Added user-role declarations
- Added scheduler job/schedule declarations
- Added captive-portal profile declarations
- Added loop-protect, UDLD keywords
- Added IPv6 ND / RA guard / DHCPv6 guard keywords
- Added banner multi-line block support (motd/login/exec)
- Added description text scoped as string
- Added Route Distinguisher / Route Target value highlighting (ASN:NN)
- Added management interface (`interface mgmt`) recognition
- Added dash-separated MAC address format
- Added section folding markers in language configuration
- Expanded port-access declaration to include role, vlan-access-tunnel-profile, onboarding-profile, client-profile
- Expanded SNMP keywords for v3 (user, group, view, auth/priv)
- Expanded system keywords (hardware, resource, fan, power-supply, redundancy)
- Expanded BGP keywords (l2vpn-evpn, route-reflector-client, send-community extended, bfd)
- Expanded constants (true/false/on/off, ospf/eigrp/igmp/mld protocols)
- Updated example config with comprehensive VXLAN/EVPN/VSX fabric scenario

### 1.0.0
- Initial release
- Full grammar for AOS-CX interface, routing, switching, QoS, security, and system commands
