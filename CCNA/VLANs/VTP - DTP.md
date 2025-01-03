**DTP Table**

|                       | Trunk | Dynamic Desirable | Access | Dynamic Auto |
| --------------------- | ----- | ----------------- | ------ | ------------ |
| **Trunk**             | Trunk | Trunk             | X      | Trunk        |
| **Dynamic** Desirable | Trunk | Trunk             | Access | Trunk        |
| **Access**            | X     | Access            | Access | Access       |
| **Dynamic** Auto      | Trunk | Trunk             | Access | Access       |

DTP - Dynamic Trunking Protocol

Recommended to **disable** DTP

VTP - VLAN Trunk Protocol

Recommended to **not** use VTP

3x Versions: 1 / 2  / 3

Switches are **Servers** by Default

Revision number is increased every time a VLAN is added/modified/deleted

Higher Revision Number wins

VTP Clients:
- cannot add/modify/delete VLANs
- do not store VLAN DB in NVRAM (except for v3)
- will advertise VTP info

VTP v1-2 only support Vlans 1-1005

Switch with null VTP domain will auto-join

VTP Transparent Mode:
- Own independent Vlan DB
- Will forward VTP updates in the same domain
- 