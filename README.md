# Digital VLSI SoC Design and Planning
<img width="1486" height="725" alt="image" src="https://github.com/user-attachments/assets/0ee3ff78-0e4d-4258-bfc7-db8f6f3be8fe" /> 
A 2-week Digital VLSI SoC Design and Planning workshop conducted by VSD in collaboration with NASSCOM. The workshop focuses on the end-to-end ASIC design process, beginning with RTL and culminating in the GDS file, implemented through the OpenLane design flow.

## Topics Learnt
The RTL to GDSII flow represents the complete process of transforming a Register Transfer Level (RTL) description of a digital circuit into a fabrication-ready physical layout. This methodology includes steps such as synthesis, floorplanning, placement, routing, and final layout generation in GDSII format. Each stage ensures that the resulting integrated circuit faithfully meets the intended functionality, design constraints, and manufacturing specifications. This structured flow is fundamental to modern VLSI design, enabling efficient and reliable ASIC development.

<img width="810" height="444" alt="Screenshot 2025-11-17 001128" src="https://github.com/user-attachments/assets/2399c7b3-4848-4392-abfd-781ddeacfbd7" />


## Introduction to IC Components
1. *Chip Package*: 
The component we usually see on any embedded board is not the actual silicon chip, but the package. The package acts as a protective enclosure for the silicon die, shields it from environmental damage, and provides mechanical stability. It also includes metal leads or balls (in BGA packages) that allow electrical connection between the silicon die and the PCB. Packaging ensures heat dissipation, ease of handling, and reliable integration of the chip onto systems.

<img width="815" height="537" alt="Screenshot 2025-11-17 001309" src="https://github.com/user-attachments/assets/22424e32-c01a-4ee3-862a-8d85274a3b3d" />


3. *Silicon Die*:
Inside every package lies the silicon die, which is the actual manufactured semiconductor block. The die contains all functional circuits logic gates, memory blocks, I/O interfaces, and analog components. It is created through multiple photolithography and fabrication steps in the foundry. The die is extremely small and fragile, which is why it must be encapsulated inside a package.

<img width="816" height="558" alt="image" src="https://github.com/user-attachments/assets/b80f6d4e-926d-49af-964e-6107d69c7565" />


5. *IO Pads*:
 All external signals entering or leaving the chip must pass through IO pads present on the die. These pads act as the interface between the chip’s internal logic and the outside world. They include ESD protection circuits, drivers, and receivers to ensure signal integrity and protect against voltage spikes. Pads form the boundary of the die and occupy a significant portion of chip periphery.

6. *Core*:
 The core is the central region of the die where all the digital logic is placed. This includes the combinational and sequential circuits, functional blocks, arithmetic units, controllers, memory interfaces, and other custom logic designed for the chip. The performance, area, and power efficiency of the entire chip largely depend on the design and optimization of the core.

7. *Die*:
 The core and the surrounding pad ring constitute the die, which is the fundamental unit manufactured in semiconductor fabrication. Dies are replicated across a silicon wafer, and each die functions as one complete chip after packaging. The die layout must follow strict design rules to ensure manufacturability, reliability, and yield.

8. *Foundry*:
A foundry is the fabrication facility where silicon dies are manufactured. It uses highly advanced equipment for photolithography, doping, etching, deposition, and CMP (Chemical-Mechanical Polishing). Each foundry (TSMC, Intel, GlobalFoundries, etc.) provides its own process design kit (PDK) and manufacturing rules. Foundry IPs are specialized building blocks—like SRAM, PLLs, IO cells—optimized for a specific technology node.

<img width="1035" height="586" alt="image" src="https://github.com/user-attachments/assets/ed218de0-aaed-4167-8111-41efa1ae251d" />


10. *Macros*:
Macros are pre-designed, reusable digital or analog blocks such as SRAMs, multipliers, FIFOs, or specialized logic. They are inserted as hard blocks within the core during the physical design flow. Macros help reduce design time and ensure silicon-proven reliability. Unlike foundry IPs, which are process-specific, macros are more generic digital blocks used repeatedly across designs.

## Introduction to RISC-V

-*Application software* refers to the programs written by users to perform specific tasks such as a stopwatch app, a browser, or productivity tools. These applications are written in high-level languages like C, C++, Java, or Python. When a user runs an application, the program itself does not interact directly with the hardware. Instead, it relies on lower-level system components to translate the high-level instructions into a form that the processor can understand. In VLSI terms, the application is the starting point of the entire execution pipeline.

<img width="1043" height="600" alt="image" src="https://github.com/user-attachments/assets/ffc89f0f-a818-4e6e-9f89-a846927c1f6f" />


-*System Software* acts as the intermediary layer that prepares application programs to run on actual hardware with *Operating System (OS)* handles fundamental operations such as input/output management, memory control, and basic system services often generating low-level function calls. And the *Compiler* takes high-level language functions provided by the OS or the user and converts them into ISA-specific assembly instructions. For RISC-V hardware, this means generating RISC-V assembly instructions. Finally, the *Assembler* then converts this assembly code into machine language (binary). This binary is fed directly into the hardware. Each instruction triggers a set of signal transitions in the digital logic, ensuring the processor performs exactly what the program intended.

-*Instruction Set Architecture (ISA)* defines the set of instructions a processor can execute. It acts as the formal interface between software and hardware. For RISC-V, the ISA is simple, modular, and open-source, making it widely used for research and chip design. When a C program is compiled, it is converted into RISC-V assembly instructions, which represent device-level operations such as arithmetic, memory access, branching, and control flow. These assembly instructions are then transformed into machine-level binary code, which is fed into the processor for execution.

<img width="937" height="560" alt="Screenshot 2025-11-17 003459" src="https://github.com/user-attachments/assets/5072ab27-0122-429e-9d14-60b13b370b23" />


-*RTL Implementation* is done when the ISA and machine code behavior is understood, we implement the processor architecture in RTL (Register Transfer Level) using Verilog, the PicoRV32 core is a lightweight RISC-V implementation written in Verilog. The RTL describes registers, datapaths, ALUs, control units, pipeline stages, and the overall micro-architecture. The RTL code reflects the exact behavior needed to execute RISC-V instructions. This RTL must then be transformed into a physical chip layout through the ASIC design flow.

<img width="1035" height="599" alt="image" src="https://github.com/user-attachments/assets/dd9fcc5a-ae33-4fbd-af4e-b79371ddbd9d" />


-After RTL is verified functionally, it enters the physical design stage commonly called RTL to GDSII or Place-and-Route (PnR). This process converts the logical hardware representation into a manufacturable silicon layout.Tools like OpenLane perform synthesis, floorplanning, placement of standard cells, routing of wires, clock-tree synthesis, and final sign-off checks.

-The output is the GDSII file, which contains geometrical shapes representing transistors, metal layers, vias, and all physical information required by a semiconductor foundry to fabricate the chip.

<img width="1007" height="588" alt="image" src="https://github.com/user-attachments/assets/1f79a4bb-b1bc-4f05-b657-1ceb0aca2437" />

The three major parts of this course are:

1. RISC-V ISA – Understanding the instruction set architecture that defines how software instructions interact with hardware.

2. RTL and Synthesis of the RISC-V CPU Core (picorv32) – Converting the ISA specification into Verilog RTL and synthesizing it into a gate-level netlist.

3. Physical Design Implementation of picorv32 – Transforming the synthesized netlist into an actual chip layout using the RTL-to-GDSII flow.

## Open-Source ASIC Implementation

To design an open-source digital ASIC, several key components are required:

<img width="1072" height="581" alt="Screenshot 2025-11-17 020732" src="https://github.com/user-attachments/assets/7675c816-3cfb-48f4-9f83-17b525e05628" />


1. RTL Designs: It describes the digital logic behavior of a design using Verilog or VHDL. In open-source ASIC workflows, RTL is the starting point from which all downstream processes are derived, including synthesis and physical design. Platforms like librecores.org, opencores.org, and GitHub provide widely available open-source RTL blocks such as RISC-V cores.  
2. EDA Tools: Electronic Design Automation (EDA) tools automate each stage of the chip design flow—from synthesis and floorplanning to routing and sign-off. Open-source tools such as Yosys, OpenROAD, Magic, Netgen, and OpenLANE provide a complete toolchain capable of taking RTL all the way to GDSII. These tools collectively perform logic synthesis, placement, routing, timing analysis, DRC, LVS, and final verification.  
3. PDK Data: A Process Design Kit (PDK) contains all technology-specific information required for chip fabrication, such as device models, design rules, layer information, and standard cell libraries. Historically, PDKs were distributed under NDAs, restricting public access. The SkyWater-Google collaboration enabled the first open-source 130nm PDK, making fully open ASIC design flows possible.

*OpenLANE – Open-Source ASIC Implementation Flow*

<img width="819" height="584" alt="Screenshot 2025-11-17 020613" src="https://github.com/user-attachments/assets/b9ff4c2d-88d3-4bfa-976e-c32ac38890a0" />



 1. Synthesis

<img width="1070" height="574" alt="Screenshot 2025-11-17 020921" src="https://github.com/user-attachments/assets/e94da2c7-9d03-4c33-aca4-8115e8732751" />


Synthesis converts the RTL description into a gate-level netlist composed of standard cells from the target PDK. The resulting netlist preserves the original RTL functionality but expresses it in terms of physical logic gates. Standard cells include multiple models—electrical (liberty), behavioral (HDL), and layout views (LEF/GDS) that support different EDA processes.

2. Floorplanning and Power Planning

<img width="1068" height="563" alt="Screenshot 2025-11-17 021014" src="https://github.com/user-attachments/assets/a0a615d2-4808-442b-aa48-24d1ed7d7316" />

<img width="1070" height="556" alt="Screenshot 2025-11-17 021058" src="https://github.com/user-attachments/assets/9a85f887-cce9-42be-adb0-3054b7079b1a" />

<img width="1070" height="572" alt="Screenshot 2025-11-17 021127" src="https://github.com/user-attachments/assets/f32ca9b2-6bec-4fee-9938-5f18be15eec5" />



Floorplanning arranges all major blocks on the chip die and defines locations for I/O pads, macros, and routing channels. Macro and chip-level dimensions, pin placements, and row structures are defined during this stage. Power planning introduces power rings and straps to ensure stable VDD and VSS distribution across the chip.

3. Placement

<img width="1070" height="556" alt="Screenshot 2025-11-17 021149" src="https://github.com/user-attachments/assets/b6be5044-5e8a-4bfc-95fc-981a8fee9df2" />

<img width="1071" height="567" alt="Screenshot 2025-11-17 021210" src="https://github.com/user-attachments/assets/32ec3921-bac0-4650-b424-9b00e8827511" />


Standard cells from the synthesized netlist are placed into predefined rows aligned with the manufacturing grid. Placement aims to minimize wirelength and reduce routing congestion while adhering to timing constraints. The output is a physically-arranged but not yet connected version of the design.

4. Clock Tree Synthesis (CTS)

<img width="1072" height="568" alt="Screenshot 2025-11-17 023908" src="https://github.com/user-attachments/assets/3ce84a44-edcb-44f4-aaf8-1737c940b3a6" />

Clock Tree Synthesis is the step where a dedicated clock distribution network is created to deliver the clock signal to all sequential elements—mainly flip-flops—within the design. The goal is to minimize skew so that all elements receive the clock edge as uniformly as possible, even though perfect zero skew is practically impossible. Typically, structured tree topologies such as H-trees or X-trees are used to achieve low-skew, balanced propagation paths.

5. Routing

<img width="1072" height="581" alt="Screenshot 2025-11-17 023932" src="https://github.com/user-attachments/assets/a5e0aab1-f372-493a-bf8d-1ce54a1e501b" />

Routing connects all placed standard cells by drawing metal interconnects using the available routing layers in the technology (Sky130 uses LI + Metal1–Metal5). The tool assigns horizontal and vertical tracks across multiple layers, inserting vias wherever the routing needs to switch between layers. This stage finalizes the physical wiring so that every net in the gate-level netlist is electrically connected according to the design rules.

6. Sign-Off

<img width="1067" height="552" alt="Screenshot 2025-11-17 024035" src="https://github.com/user-attachments/assets/ae682264-2491-433d-a80f-b63d09ee46b3" />

Sign-off verifies that the design is ready for fabrication by performing a series of critical checks. Physical verification includes Design Rule Checking (DRC) to ensure the layout obeys all process constraints and Layout-vs-Schematic (LVS) to confirm the layout matches the logical netlist. Timing verification is done through Static Timing Analysis (STA) to ensure all timing paths meet setup and hold requirements before generating the final GDSII file.

