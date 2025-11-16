# Digital VLSI SoC Design and Planning
<img width="1486" height="725" alt="image" src="https://github.com/user-attachments/assets/0ee3ff78-0e4d-4258-bfc7-db8f6f3be8fe" /> 
A 2-week Digital VLSI SoC Design and Planning workshop conducted by VSD in collaboration with NASSCOM. The workshop focuses on the end-to-end ASIC design process, beginning with RTL and culminating in the GDS file, implemented through the OpenLane design flow.

## Topics Learnt
The RTL to GDSII flow represents the complete process of transforming a Register Transfer Level (RTL) description of a digital circuit into a fabrication-ready physical layout. This methodology includes steps such as synthesis, floorplanning, placement, routing, and final layout generation in GDSII format. Each stage ensures that the resulting integrated circuit faithfully meets the intended functionality, design constraints, and manufacturing specifications. This structured flow is fundamental to modern VLSI design, enabling efficient and reliable ASIC development.

## Introduction to IC Components
1. *Chip Package* 
The component we usually see on any embedded board is not the actual silicon chip, but the package. The package acts as a protective enclosure for the silicon die, shields it from environmental damage, and provides mechanical stability. It also includes metal leads or balls (in BGA packages) that allow electrical connection between the silicon die and the PCB. Packaging ensures heat dissipation, ease of handling, and reliable integration of the chip onto systems.

2. *Silicon Die*
Inside every package lies the silicon die, which is the actual manufactured semiconductor block. The die contains all functional circuits logic gates, memory blocks, I/O interfaces, and analog components. It is created through multiple photolithography and fabrication steps in the foundry. The die is extremely small and fragile, which is why it must be encapsulated inside a package.
