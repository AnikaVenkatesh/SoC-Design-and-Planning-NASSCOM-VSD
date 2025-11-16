# Digital VLSI SoC Design and Planning
<img width="1486" height="725" alt="image" src="https://github.com/user-attachments/assets/0ee3ff78-0e4d-4258-bfc7-db8f6f3be8fe" /> 
A 2-week Digital VLSI SoC Design and Planning workshop conducted by VSD in collaboration with NASSCOM. The workshop focuses on the end-to-end ASIC design process, beginning with RTL and culminating in the GDS file, implemented through the OpenLane design flow.

## Topics Learnt
The RTL to GDSII flow represents the complete process of transforming a Register Transfer Level (RTL) description of a digital circuit into a fabrication-ready physical layout. This methodology includes steps such as synthesis, floorplanning, placement, routing, and final layout generation in GDSII format. Each stage ensures that the resulting integrated circuit faithfully meets the intended functionality, design constraints, and manufacturing specifications. This structured flow is fundamental to modern VLSI design, enabling efficient and reliable ASIC development.

## Introduction to IC Components
1. *Chip Package*: 
The component we usually see on any embedded board is not the actual silicon chip, but the package. The package acts as a protective enclosure for the silicon die, shields it from environmental damage, and provides mechanical stability. It also includes metal leads or balls (in BGA packages) that allow electrical connection between the silicon die and the PCB. Packaging ensures heat dissipation, ease of handling, and reliable integration of the chip onto systems.

2. *Silicon Die*:
Inside every package lies the silicon die, which is the actual manufactured semiconductor block. The die contains all functional circuits logic gates, memory blocks, I/O interfaces, and analog components. It is created through multiple photolithography and fabrication steps in the foundry. The die is extremely small and fragile, which is why it must be encapsulated inside a package.

3. *IO Pads*:
 All external signals entering or leaving the chip must pass through IO pads present on the die. These pads act as the interface between the chip’s internal logic and the outside world. They include ESD protection circuits, drivers, and receivers to ensure signal integrity and protect against voltage spikes. Pads form the boundary of the die and occupy a significant portion of chip periphery.

4. *Core*:
 The core is the central region of the die where all the digital logic is placed. This includes the combinational and sequential circuits, functional blocks, arithmetic units, controllers, memory interfaces, and other custom logic designed for the chip. The performance, area, and power efficiency of the entire chip largely depend on the design and optimization of the core.

5. *Die*:
 The core and the surrounding pad ring constitute the die, which is the fundamental unit manufactured in semiconductor fabrication. Dies are replicated across a silicon wafer, and each die functions as one complete chip after packaging. The die layout must follow strict design rules to ensure manufacturability, reliability, and yield.

6. *Foundry*:
A foundry is the fabrication facility where silicon dies are manufactured. It uses highly advanced equipment for photolithography, doping, etching, deposition, and CMP (Chemical-Mechanical Polishing). Each foundry (TSMC, Intel, GlobalFoundries, etc.) provides its own process design kit (PDK) and manufacturing rules. Foundry IPs are specialized building blocks—like SRAM, PLLs, IO cells—optimized for a specific technology node.

7. *Macros*:
Macros are pre-designed, reusable digital or analog blocks such as SRAMs, multipliers, FIFOs, or specialized logic. They are inserted as hard blocks within the core during the physical design flow. Macros help reduce design time and ensure silicon-proven reliability. Unlike foundry IPs, which are process-specific, macros are more generic digital blocks used repeatedly across designs.

## Introduction to RISC-V

-*Application software* refers to the programs written by users to perform specific tasks such as a stopwatch app, a browser, or productivity tools. These applications are written in high-level languages like C, C++, Java, or Python. When a user runs an application, the program itself does not interact directly with the hardware. Instead, it relies on lower-level system components to translate the high-level instructions into a form that the processor can understand. In VLSI terms, the application is the starting point of the entire execution pipeline.

-*System Software* acts as the intermediary layer that prepares application programs to run on actual hardware with *Operating System (OS)* handles fundamental operations such as input/output management, memory control, and basic system services often generating low-level function calls. And the *Compiler* takes high-level language functions provided by the OS or the user and converts them into ISA-specific assembly instructions. For RISC-V hardware, this means generating RISC-V assembly instructions. Finally, the *Assembler* then converts this assembly code into machine language (binary). This binary is fed directly into the hardware. Each instruction triggers a set of signal transitions in the digital logic, ensuring the processor performs exactly what the program intended.

-*Instruction Set Architecture (ISA)* defines the set of instructions a processor can execute. It acts as the formal interface between software and hardware. For RISC-V, the ISA is simple, modular, and open-source, making it widely used for research and chip design. When a C program is compiled, it is converted into RISC-V assembly instructions, which represent device-level operations such as arithmetic, memory access, branching, and control flow. These assembly instructions are then transformed into machine-level binary code, which is fed into the processor for execution.

-*RTL Implementation* is done when the ISA and machine code behavior is understood, we implement the processor architecture in RTL (Register Transfer Level) using Verilog, the PicoRV32 core is a lightweight RISC-V implementation written in Verilog. The RTL describes registers, datapaths, ALUs, control units, pipeline stages, and the overall micro-architecture. The RTL code reflects the exact behavior needed to execute RISC-V instructions. This RTL must then be transformed into a physical chip layout through the ASIC design flow.

-After RTL is verified functionally, it enters the physical design stage commonly called RTL to GDSII or Place-and-Route (PnR). This process converts the logical hardware representation into a manufacturable silicon layout.Tools like OpenLane perform synthesis, floorplanning, placement of standard cells, routing of wires, clock-tree synthesis, and final sign-off checks.

-The output is the GDSII file, which contains geometrical shapes representing transistors, metal layers, vias, and all physical information required by a semiconductor foundry to fabricate the chip.
