# Machine and robot hardware

[Back to the index](README.md)

## Workstations

Ten identical workstations, built for this lab. Every machine carries the same specification and
the same disk image, which is why a user moving between stations finds the same software in the
same places.

| Item | Specification |
|---|---|
| Motherboard | MSI MAG X870 TOMAHAWK WIFI |
| CPU | AMD Ryzen 9 9900X |
| GPU | NVIDIA RTX 5080, Blackwell, compute capability `sm_120` |
| Memory | 32 GB DDR5-6000 CL30 |
| Storage | Crucial T705 PCIe Gen 5 NVMe |
| Network | Onboard Realtek RTL8126 to the campus network |

## Stations

Hostnames follow the pattern `<name>-isl-ssurobotics-<numeral>`, and the station number is the
numeral in the hostname.

| Hostname | Station | Room |
|---|---|---|
| `brandon-isl-ssurobotics-i` | I | 2008 |
| `tyler-isl-ssurobotics-ii` | II | 2008 |
| `alex-isl-ssurobotics-iii` | III | 2008 |
| `xor-isl-ssurobotics-iv` | IV | 2008 |
| `ryan-isl-ssurobotics-v` | V | 2008 |
| `antonio-isl-ssurobotics-vi` | VI | 2008 |
| `sage-isl-ssurobotics-vii` | VII | 2008 |
| `hyper-isl-ssurobotics-viii` | VIII | 2008 |
| `blake-isl-ssurobotics-ix` | IX | 2007 |
| `esli-isl-ssurobotics-x` | X | 2007 |

Stations I through VIII are in Salazar 2008, and IX and X are in 2007.

An older group of ISL machines, named `<name>-isl-legacy-<numeral>`, remains in service for
general lab use. Those do not carry the robotics image described in
[Software](software.md).

## Manipulators

### Trossen WidowX AI

Five six-axis manipulators with a spherical wrist, a reach of 0.769 m, and a rated payload of
1.5 kg. These are the arms used for the six-axis kinematics and velocity control work.

The WidowX AI is commanded over **Ethernet** rather than USB, through the `trossen_arm` Python
driver, with no ROS layer involved. Each arm is connected directly to its workstation over a
private point-to-point link on a USB-Ethernet adapter, and is not on the campus network.

| | Address |
|---|---|
| Arm controller | `192.168.1.2/24` |
| Workstation, on the adapter | `192.168.1.1/24`, no gateway and no DNS |
| Campus network | the onboard interface, unaffected |

The driver version installed on the machines is matched to the firmware on the arm controllers.
This pairing is deliberate and is described in [Software](software.md).

### Interbotix RX150

Five-axis manipulators with a reach of approximately 450 mm, used for the introductory kinematics
work. Unlike the WidowX AI, the RX150 connects over USB and is commanded through the Interbotix
ROS 2 packages.

Each session requires the arm, its own 12 V supply, a USB to micro USB cable, and a clamp for
fixing the base to the table. All four are returned to storage at the end of a session.

> **Clamp the base before applying power.** An unclamped manipulator will move across the work
> surface under its own reaction torques. Clear the full reach of the arm before commanding any
> motion, and keep the power disconnect within reach.

## Cameras

| Camera | Interface | Notes |
|---|---|---|
| Intel RealSense D435 | USB | Depth and infrared. Python bindings through `pyrealsense2` |
| Luxonis OAK-D W | USB | Depth with on-camera inference. Python bindings through `depthai` |

Both cameras work without administrative privileges, as the required device rules are already
installed on every machine.
