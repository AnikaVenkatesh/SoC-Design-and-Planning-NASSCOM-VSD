# **Digital VLSI SoC Design and Planning**
<img width="1486" height="725" alt="image" src="https://github.com/user-attachments/assets/0ee3ff78-0e4d-4258-bfc7-db8f6f3be8fe" /> 
A 2-week Digital VLSI SoC Design and Planning workshop conducted by VSD in collaboration with NASSCOM. The workshop focuses on the end-to-end ASIC design process, beginning with RTL and culminating in the GDS file, implemented through the OpenLane design flow.

## **Topics Learnt**
The RTL to GDSII flow represents the complete process of transforming a Register Transfer Level (RTL) description of a digital circuit into a fabrication-ready physical layout. This methodology includes steps such as synthesis, floorplanning, placement, routing, and final layout generation in GDSII format. Each stage ensures that the resulting integrated circuit faithfully meets the intended functionality, design constraints, and manufacturing specifications. This structured flow is fundamental to modern VLSI design, enabling efficient and reliable ASIC development.

<img width="810" height="444" alt="Screenshot 2025-11-17 001128" src="https://github.com/user-attachments/assets/2399c7b3-4848-4392-abfd-781ddeacfbd7" />


## Introduction to IC Components
1. **Chip Package**: 
The component we usually see on any embedded board is not the actual silicon chip, but the package. The package acts as a protective enclosure for the silicon die, shields it from environmental damage, and provides mechanical stability. It also includes metal leads or balls (in BGA packages) that allow electrical connection between the silicon die and the PCB. Packaging ensures heat dissipation, ease of handling, and reliable integration of the chip onto systems.

<img width="815" height="537" alt="Screenshot 2025-11-17 001309" src="https://github.com/user-attachments/assets/22424e32-c01a-4ee3-862a-8d85274a3b3d" />


3. **Silicon Die**:
Inside every package lies the silicon die, which is the actual manufactured semiconductor block. The die contains all functional circuits logic gates, memory blocks, I/O interfaces, and analog components. It is created through multiple photolithography and fabrication steps in the foundry. The die is extremely small and fragile, which is why it must be encapsulated inside a package.

<img width="816" height="558" alt="image" src="https://github.com/user-attachments/assets/b80f6d4e-926d-49af-964e-6107d69c7565" />


5. **IO Pads**:
 All external signals entering or leaving the chip must pass through IO pads present on the die. These pads act as the interface between the chip’s internal logic and the outside world. They include ESD protection circuits, drivers, and receivers to ensure signal integrity and protect against voltage spikes. Pads form the boundary of the die and occupy a significant portion of chip periphery.

6. **Core**:
 The core is the central region of the die where all the digital logic is placed. This includes the combinational and sequential circuits, functional blocks, arithmetic units, controllers, memory interfaces, and other custom logic designed for the chip. The performance, area, and power efficiency of the entire chip largely depend on the design and optimization of the core.

7. **Die**:
 The core and the surrounding pad ring constitute the die, which is the fundamental unit manufactured in semiconductor fabrication. Dies are replicated across a silicon wafer, and each die functions as one complete chip after packaging. The die layout must follow strict design rules to ensure manufacturability, reliability, and yield.

8. **Foundry**:
A foundry is the fabrication facility where silicon dies are manufactured. It uses highly advanced equipment for photolithography, doping, etching, deposition, and CMP (Chemical-Mechanical Polishing). Each foundry (TSMC, Intel, GlobalFoundries, etc.) provides its own process design kit (PDK) and manufacturing rules. Foundry IPs are specialized building blocks—like SRAM, PLLs, IO cells—optimized for a specific technology node.

<img width="1035" height="586" alt="image" src="https://github.com/user-attachments/assets/ed218de0-aaed-4167-8111-41efa1ae251d" />


10. **Macros**:
Macros are pre-designed, reusable digital or analog blocks such as SRAMs, multipliers, FIFOs, or specialized logic. They are inserted as hard blocks within the core during the physical design flow. Macros help reduce design time and ensure silicon-proven reliability. Unlike foundry IPs, which are process-specific, macros are more generic digital blocks used repeatedly across designs.

## Introduction to RISC-V

-**Application software** refers to the programs written by users to perform specific tasks such as a stopwatch app, a browser, or productivity tools. These applications are written in high-level languages like C, C++, Java, or Python. When a user runs an application, the program itself does not interact directly with the hardware. Instead, it relies on lower-level system components to translate the high-level instructions into a form that the processor can understand. In VLSI terms, the application is the starting point of the entire execution pipeline.

<img width="1043" height="600" alt="image" src="https://github.com/user-attachments/assets/ffc89f0f-a818-4e6e-9f89-a846927c1f6f" />


-**System Software** acts as the intermediary layer that prepares application programs to run on actual hardware with *Operating System (OS)* handles fundamental operations such as input/output management, memory control, and basic system services often generating low-level function calls. And the *Compiler* takes high-level language functions provided by the OS or the user and converts them into ISA-specific assembly instructions. For RISC-V hardware, this means generating RISC-V assembly instructions. Finally, the *Assembler* then converts this assembly code into machine language (binary). This binary is fed directly into the hardware. Each instruction triggers a set of signal transitions in the digital logic, ensuring the processor performs exactly what the program intended.

-**Instruction Set Architecture (ISA)** defines the set of instructions a processor can execute. It acts as the formal interface between software and hardware. For RISC-V, the ISA is simple, modular, and open-source, making it widely used for research and chip design. When a C program is compiled, it is converted into RISC-V assembly instructions, which represent device-level operations such as arithmetic, memory access, branching, and control flow. These assembly instructions are then transformed into machine-level binary code, which is fed into the processor for execution.

<img width="937" height="560" alt="Screenshot 2025-11-17 003459" src="https://github.com/user-attachments/assets/5072ab27-0122-429e-9d14-60b13b370b23" />


-**RTL Implementation** is done when the ISA and machine code behavior is understood, we implement the processor architecture in RTL (Register Transfer Level) using Verilog, the PicoRV32 core is a lightweight RISC-V implementation written in Verilog. The RTL describes registers, datapaths, ALUs, control units, pipeline stages, and the overall micro-architecture. The RTL code reflects the exact behavior needed to execute RISC-V instructions. This RTL must then be transformed into a physical chip layout through the ASIC design flow.

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


1. **RTL Designs:** It describes the digital logic behavior of a design using Verilog or VHDL. In open-source ASIC workflows, RTL is the starting point from which all downstream processes are derived, including synthesis and physical design. Platforms like librecores.org, opencores.org, and GitHub provide widely available open-source RTL blocks such as RISC-V cores.  
2. **EDA Tools: Electronic Design Automation (EDA):** Tools automate each stage of the chip design flow—from synthesis and floorplanning to routing and sign-off. Open-source tools such as Yosys, OpenROAD, Magic, Netgen, and OpenLANE provide a complete toolchain capable of taking RTL all the way to GDSII. These tools collectively perform logic synthesis, placement, routing, timing analysis, DRC, LVS, and final verification.  
3. **PDK Data:** A Process Design Kit (PDK) contains all technology-specific information required for chip fabrication, such as device models, design rules, layer information, and standard cell libraries. Historically, PDKs were distributed under NDAs, restricting public access. The SkyWater-Google collaboration enabled the first open-source 130nm PDK, making fully open ASIC design flows possible.

**OpenLANE – Open-Source ASIC Implementation Flow**

<img width="819" height="584" alt="Screenshot 2025-11-17 020613" src="https://github.com/user-attachments/assets/b9ff4c2d-88d3-4bfa-976e-c32ac38890a0" />



 1. **Synthesis**

<img width="1070" height="574" alt="Screenshot 2025-11-17 020921" src="https://github.com/user-attachments/assets/e94da2c7-9d03-4c33-aca4-8115e8732751" />


Synthesis converts the RTL description into a gate-level netlist composed of standard cells from the target PDK. The resulting netlist preserves the original RTL functionality but expresses it in terms of physical logic gates. Standard cells include multiple models—electrical (liberty), behavioral (HDL), and layout views (LEF/GDS) that support different EDA processes.

2. **Floorplanning and Power Planning**

<img width="1068" height="563" alt="Screenshot 2025-11-17 021014" src="https://github.com/user-attachments/assets/a0a615d2-4808-442b-aa48-24d1ed7d7316" />

<img width="1070" height="556" alt="Screenshot 2025-11-17 021058" src="https://github.com/user-attachments/assets/9a85f887-cce9-42be-adb0-3054b7079b1a" />

<img width="1070" height="572" alt="Screenshot 2025-11-17 021127" src="https://github.com/user-attachments/assets/f32ca9b2-6bec-4fee-9938-5f18be15eec5" />



Floorplanning arranges all major blocks on the chip die and defines locations for I/O pads, macros, and routing channels. Macro and chip-level dimensions, pin placements, and row structures are defined during this stage. Power planning introduces power rings and straps to ensure stable VDD and VSS distribution across the chip.

3. **Placement**

<img width="1070" height="556" alt="Screenshot 2025-11-17 021149" src="https://github.com/user-attachments/assets/b6be5044-5e8a-4bfc-95fc-981a8fee9df2" />

<img width="1071" height="567" alt="Screenshot 2025-11-17 021210" src="https://github.com/user-attachments/assets/32ec3921-bac0-4650-b424-9b00e8827511" />


Standard cells from the synthesized netlist are placed into predefined rows aligned with the manufacturing grid. Placement aims to minimize wirelength and reduce routing congestion while adhering to timing constraints. The output is a physically-arranged but not yet connected version of the design.

4. **Clock Tree Synthesis (CTS)**

<img width="1072" height="568" alt="Screenshot 2025-11-17 023908" src="https://github.com/user-attachments/assets/3ce84a44-edcb-44f4-aaf8-1737c940b3a6" />

Clock Tree Synthesis is the step where a dedicated clock distribution network is created to deliver the clock signal to all sequential elements—mainly flip-flops—within the design. The goal is to minimize skew so that all elements receive the clock edge as uniformly as possible, even though perfect zero skew is practically impossible. Typically, structured tree topologies such as H-trees or X-trees are used to achieve low-skew, balanced propagation paths.

5. **Routing**

<img width="1072" height="581" alt="Screenshot 2025-11-17 023932" src="https://github.com/user-attachments/assets/a5e0aab1-f372-493a-bf8d-1ce54a1e501b" />

Routing connects all placed standard cells by drawing metal interconnects using the available routing layers in the technology (Sky130 uses LI + Metal1–Metal5). The tool assigns horizontal and vertical tracks across multiple layers, inserting vias wherever the routing needs to switch between layers. This stage finalizes the physical wiring so that every net in the gate-level netlist is electrically connected according to the design rules.

6. **Sign-Off**

<img width="1067" height="552" alt="Screenshot 2025-11-17 024035" src="https://github.com/user-attachments/assets/ae682264-2491-433d-a80f-b63d09ee46b3" />

Sign-off verifies that the design is ready for fabrication by performing a series of critical checks. Physical verification includes Design Rule Checking (DRC) to ensure the layout obeys all process constraints and Layout-vs-Schematic (LVS) to confirm the layout matches the logical netlist. Timing verification is done through Static Timing Analysis (STA) to ensure all timing paths meet setup and hold requirements before generating the final GDSII file.

## Lab Implementations- *SECTION-1*

 **1. To Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.**

 Steps to invoke OpenLANE flow 

```bash
cd Desktop/work/tools/openlane_working_dir/openlane

docker

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a

run_synthesis

exit

exit
```
**Screenshots of the steps**

<img width="1280" height="768" alt="Starting commands" src="https://github.com/user-attachments/assets/010c858a-0a48-47cc-85a0-1ca1eca80cf9" />

<img width="1280" height="768" alt="starting com2" src="https://github.com/user-attachments/assets/61cabe68-51cd-4919-9f3c-ac08359e7211" />

<img width="1280" height="768" alt="starting_com3" src="https://github.com/user-attachments/assets/a4753326-aa79-40be-ae22-9bc9552e3ecc" />

**2. To calculate the flop ratio**

<img width="1280" height="768" alt="folder creation" src="https://github.com/user-attachments/assets/68a2e8dc-dc93-436c-9b6a-d9602e6cd9f9" />

<img width="1280" height="768" alt="no of cells" src="https://github.com/user-attachments/assets/9179fbb4-d9b1-4a58-811e-ad1014a83526" />

<img width="1280" height="768" alt="no of dfft" src="https://github.com/user-attachments/assets/b82ac8a8-f30d-41f7-aca3-4fe25cdaee09" />


**## Flop Ratio Calculation**

The flop ratio is calculated using the total number of flip-flops divided by the total number of cells:

$$
\text{Flop Ratio} = \frac{1613}{14876} = 0.108429685
$$

The percentage of DFFs is obtained by multiplying the flop ratio by 100:

$$
\text{DFF Percentage} = 0.108429685 \times 100 = 10.84296854\%
$$

## Lab Implementations-*SECTION-2*

**1. To Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.**

Steps to invoke OpenLANE flow 

```bash
cd Desktop/work/tools/openlane_working_dir/openlane

docker

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a

run_synthesis

run_floorplan


```

**Screenshots**

<img width="1366" height="643" alt="run floorplan" src="https://github.com/user-attachments/assets/1cdf5cb6-c425-4c78-8c52-ba2916efdeed" />

<img width="1366" height="643" alt="run floorplan2" src="https://github.com/user-attachments/assets/fa1d3514-c5d8-4976-813a-1bb93cbb757f" />

**2. To calulate diarea**

<img width="1366" height="643" alt="Diarea" src="https://github.com/user-attachments/assets/cd08972a-8656-4e5d-912c-82fe3e0c07e6" />

1000 Unit Distance = 1 Micron

Die width (units)  = 660685
Die height (units) = 671405

Die width in microns  = 660685 / 1000 = 660.685 µm
Die height in microns = 671405 / 1000 = 671.405 µm

Die Area = 660.685 × 671.405 = 443587.212425 µm²

**3. Load generated floorplan def in magic tool**

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-11_09-50/results/floorplan/


magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```


**Screenshots of floorplan def in magic:**

<img width="1366" height="643" alt="explore fp1 centre" src="https://github.com/user-attachments/assets/ef589252-49c9-433f-b0cd-ae5d1cb138ba" />

**Equidistant placement of ports:**

<img width="1366" height="643" alt="explore fp2" src="https://github.com/user-attachments/assets/32d2fdba-3a6c-4376-acd0-f2f00e67db31" />

**Port layer as set through config.tcl:**

<img width="1366" height="643" alt="explore fp3 hori pin" src="https://github.com/user-attachments/assets/00557a42-ef2d-4c4e-83e5-22c6b584f8e5" />

<img width="1366" height="643" alt="explore fp4 vert pin" src="https://github.com/user-attachments/assets/cb4eec00-9d3c-4eb9-9209-e976f12f4843" />

**Decap Cells and Tap Cells:**

<img width="1366" height="643" alt="explore fp5 decap andtap" src="https://github.com/user-attachments/assets/32803817-29b5-48cb-a70d-edd373cb8f91" />

**Diagonally Equidistant Tap cells:**

<img width="1366" height="643" alt="explore fp6 diagnally distant tap" src="https://github.com/user-attachments/assets/41ef0cea-9ebe-4a41-aca7-2637a402e47c" />

**Unplaced standard cells at the origin**

<img width="1366" height="643" alt="explore fp7 std cell" src="https://github.com/user-attachments/assets/be036942-913c-41f6-9984-88bb210dbb9b" />

**4. Run 'picorv32a' design congestion aware placement**

```
run_placement
```
**Screenshots of the command**

<img width="1366" height="643" alt="run placement" src="https://github.com/user-attachments/assets/c84661f1-432f-4cc5-a7e4-09c9952c144c" />

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-11_16-02/results/placement/


magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```

**floorplan def in magic at the centre**


<img width="1366" height="643" alt="placement centre" src="https://github.com/user-attachments/assets/81c84912-0650-4420-b370-5240ffd974c7" />

**Standard cells legally placed**

<img width="1366" height="643" alt="placement legally placed" src="https://github.com/user-attachments/assets/32e00a75-2d79-4e08-8fef-499a3da81628" />

## Lab Implementations-*SECTION-3*

**1. To clone custom inverter standard cell design from github repository**

```
cd Desktop/work/tools/openlane_working_dir/openlane

git clone https://github.com/nickson-jose/vsdstdcelldesign

cd vsdstdcelldesign

cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

ls

magic -T sky130A.tech sky130_inv.mag &
```
<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/cdb165e6-917c-4f9b-b7d6-a1d637be2df5" />

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/1e14d359-a213-483f-8236-99fb8a9a6dd8" />

**2. To load the custom inverter layout in magic**

<img width="1366" height="643" alt="inverter view" src="https://github.com/user-attachments/assets/82265d22-5edc-471a-8667-254d79e3b463" />

**NMOS**

<img width="1366" height="643" alt="nmos" src="https://github.com/user-attachments/assets/9873f568-6f3b-4455-ba54-409c20dc0aa6" />

**PMOS**

<img width="1366" height="643" alt="pmos" src="https://github.com/user-attachments/assets/62200890-2a65-4f7c-8631-022bb4dd3ad2" />

**PMOS source connectivity to VPWR verified**

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/890865e5-5d0c-4a9d-8753-6410018619ac" />

**NMOS source connectivity to VSS VGND verified**

<img width="1366" height="643" alt="nmos conn gnd" src="https://github.com/user-attachments/assets/df793064-96d2-418e-85ad-3bbc21c2534a" />

**Output Y connected to PMOS and NMOS verified** 

<img width="1366" height="643" alt="y conn" src="https://github.com/user-attachments/assets/6413ca94-98d5-4af8-b85f-27b113ca39a6" />

**Deleting necessary layout to check for DRC error**

<img width="1366" height="643" alt="deleting drc" src="https://github.com/user-attachments/assets/9adb4856-6906-42db-852f-ee6f4e9698bb" />

<img width="1366" height="643" alt="drc error" src="https://github.com/user-attachments/assets/0cdb9906-ca9a-4247-9a8d-2cf8768a4ad5" />

**3. To spice extraction of inverter in magic.**

Commands for tkcon window of magic

```
pwd

extract all

ext2spice cthresh 0 rthresh 0

ext2spice
```


<img width="1366" height="643" alt="spice created" src="https://github.com/user-attachments/assets/b8d89f88-1b2a-45a5-9c35-81ab88a311d4" />

<img width="1366" height="643" alt="spice cr2" src="https://github.com/user-attachments/assets/71607ba8-5e89-4059-a649-acd16991e3df" />

<img width="1366" height="643" alt="sice file created" src="https://github.com/user-attachments/assets/24d99f8c-efbc-461a-8d23-028459470304" />

**4. Editing spice file prior to ngspice simulations**

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/b3e692fb-113e-4900-9fd3-f9312b53fb88" />

**5. ngspice simulations**

Commands

```
ngspice sky130_inv.spice

plot y vs time a
```

<img width="1366" height="643" alt="ngspice run1" src="https://github.com/user-attachments/assets/bc6e7ade-9600-48ab-9567-80768ec63179" />

<img width="1366" height="643" alt="ngspice plot command" src="https://github.com/user-attachments/assets/7d56f31b-232f-4ced-953b-c27bc1982575" />

<img width="1366" height="643" alt="ng plot full" src="https://github.com/user-attachments/assets/c78ff238-bc83-4f55-9c3a-a70ccb7b3d3c" />

**Rise transition:**

**Output to rise 80%**

<img width="1366" height="643" alt="rise 80" src="https://github.com/user-attachments/assets/11d212c4-e4e4-47ca-a69c-27826ea61e0f" />

<img width="1366" height="643" alt="rise 80 coordinate" src="https://github.com/user-attachments/assets/25e50487-3056-49af-84cb-1d8fa8c54992" />

**Output to rise 20%**

<img width="1366" height="643" alt="rise 20" src="https://github.com/user-attachments/assets/d87938c8-909f-42cd-971c-a2346b5f3d71" />

<img width="1366" height="643" alt="rise 20 coordinate" src="https://github.com/user-attachments/assets/6afdda21-b6b9-4994-b725-5f48e425f589" />

**Rise Transition Time Calculation**

Given:
- 20% of output = 6.18212 ns
- 80% of output = 6.24595 ns

Formula:
Rise Transition Time = Time at 80% − Time at 20%

Calculation:
Rise Transition Time = 6.24595 ns − 6.18212 ns
                      = 0.06383 ns
                      = 63.83 ps

**Fall transition:**

**Output to fall 80%**

<img width="1366" height="643" alt="fall 80" src="https://github.com/user-attachments/assets/b892221e-dd89-4729-ae5f-e96c543df5c4" />

<img width="1366" height="643" alt="fall 80 coordinate" src="https://github.com/user-attachments/assets/7822b57a-c254-4a2e-818d-c988e0400d68" />

**Output to fall 20%**

<img width="1366" height="643" alt="fall 20 plot" src="https://github.com/user-attachments/assets/14b1ff5b-3a78-4bfa-82d9-9f06e75bf1ed" />

<img width="1366" height="643" alt="fall 20 coordinate" src="https://github.com/user-attachments/assets/3203a017-1018-4730-874e-319e23e0bd9c" />

**Fall Transition Time Calculation**

Given:
- 80% of output = 8.05278 ns
- 20% of output = 8.09530 ns

Formula:
Fall Transition Time = Time at 20% − Time at 80%

Substitution:
Fall Transition Time = 8.09530 ns − 8.05278 ns

Result:
Fall Transition Time = 0.04252 ns = 42.52 ps


**Rise Cell Delay:**

**50% Screenshots**

<img width="1366" height="643" alt="rise cell delay" src="https://github.com/user-attachments/assets/3552bdae-99e6-463a-a333-1971037bdf53" />

<img width="1366" height="643" alt="rise cell del coordinate" src="https://github.com/user-attachments/assets/eda8e7d3-8543-4bc4-9998-3ec62da617cb" />

**Rise Cell Delay Calculation**

Rise Cell Delay is defined as:

Rise Cell Delay = Time taken for output to rise to 50%  
                   − Time taken for input to fall to 50%

50% of 3.3 V = 1.65 V

Given:
- Output at 50% = 6.21116 ns
- Input at 50%  = 6.15 ns

Calculation:
Rise Cell Delay = 6.21116 ns − 6.15 ns  
                 = 0.06116 ns  
                 = 61.16 ps

**Fall Cell Delay:**

<img width="1366" height="643" alt="fall cell delay plot" src="https://github.com/user-attachments/assets/2c655702-e5f0-435e-b9e6-62abf53b0b21" />

<img width="1366" height="643" alt="fall cell delay coordinate" src="https://github.com/user-attachments/assets/9b4ef248-ea3b-45dd-9dd5-f86dee7d8a9a" />

**Fall Cell Delay Calculation**

Fall Cell Delay = Time taken for output to fall to 50% − Time taken for input to rise to 50%

50% of 3.3 V = 1.65 V

Given:
- Output fall 50% crossing time = 1.20777 ns
- Input rise 50% crossing time = 1.20503 ns

Fall Cell Delay = 1.20777 ns − 1.20503 ns  
                 = 0.00274 ns  
                 = 2.74 ps

**6. To find problem in the DRC section of the old magic tech file and fix them.**


Link to Sky130 Periphery rules: https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html

Commands:
```
cd

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

tar xfz drc_tests.tgz

cd drc_tests

ls -al

gvim .magicrc

magic -d XR &
```

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/ec9adc1b-58c3-4885-8a81-f6271a5d784b" />

<img width="1366" height="643" alt="to veiw kywater com2" src="https://github.com/user-attachments/assets/dfc999f2-3da1-4450-9f78-16806bc052b5" />



**.magicrc file**

<img width="1366" height="643" alt="magicrc file" src="https://github.com/user-attachments/assets/1bfae76b-75b1-43f9-9e94-bbc5c37f1951" />


**Incorrect implementation of poly.9 rule:**

<img width="1366" height="643" alt="poly9 rule doc" src="https://github.com/user-attachments/assets/9224699f-314f-4194-a14a-6727cda96575" />

**Incorrected poly.9**

<img width="1366" height="643" alt="poly9 violation" src="https://github.com/user-attachments/assets/8e8d66fa-9fb4-471d-94cc-d4eaa5987c40" />

**New commands inserted in sky130A.tech file to update drc**

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/888e6562-a8cb-4952-9f46-792be34ba920" />

<img width="1366" height="643" alt="poly9 text edit2" src="https://github.com/user-attachments/assets/e8127c25-7b5f-4b67-bcef-01d62128663f" />

**Rule Implemented**

<img width="1366" height="643" alt="corected poly9 rule" src="https://github.com/user-attachments/assets/9f521bc7-938e-4262-877c-fbebcd567def" />


**Incorrectly implemented difftap.2:**

**difftap.2 rule**

<img width="1366" height="643" alt="diff rule doc" src="https://github.com/user-attachments/assets/78e35945-bce2-453a-b09d-c4ccbda3a1d4" />

**Incorrect implementation difftap.2**

<img width="1366" height="643" alt="diff incorrect snap" src="https://github.com/user-attachments/assets/ae65ed1b-d7fc-46e1-88cb-3a75b8612d20" />

**New commands inserted in sky130A.tech file to update drc**

<img width="1366" height="643" alt="diff text edited" src="https://github.com/user-attachments/assets/7d6551e3-2acb-47dd-b26f-0e354443776f" />

**Corrected difftap.2 rule**

<img width="1366" height="643" alt="corrected diff rule" src="https://github.com/user-attachments/assets/02594e0b-55a9-4c77-ac31-98f1f57d0ff7" />


**Incorrectly implemented nwell.4:**

**nwell.4 rule**

<img width="1366" height="643" alt="nwell 4 rule" src="https://github.com/user-attachments/assets/b84ee228-ef99-470d-aa2a-021c14be0c69" />

**screenshot of incorrectly implemented**

<img width="1366" height="643" alt="nwell incorrect snap" src="https://github.com/user-attachments/assets/55c5266f-83bf-4214-acd8-6ad4f6219b81" />

**New commands inserted in sky130A.tech file to update drc**

<img width="1366" height="643" alt="nwell text edited" src="https://github.com/user-attachments/assets/c1cc383f-1ff4-4b72-af4f-b35271dd0857" />

<img width="1366" height="643" alt="nwell text edited 2" src="https://github.com/user-attachments/assets/c911e97e-84b1-468d-ad81-eb3d7946cec2" />

**Corrected nwell.4**

<img width="1366" height="643" alt="corrected nwell rule" src="https://github.com/user-attachments/assets/a0403cf2-67a9-4511-96ba-7d3ff90b3c8e" />


## Lab Implementations-*SECTION-4*

**1. To fix up small DRC errors**

**Screenshot of tracks.info of sky130_fd_sc_hd**

<img width="1366" height="643" alt="tracks info of sky130a" src="https://github.com/user-attachments/assets/c7973d74-b1f0-4ab3-acd4-2cfa1389fa58" />

**tkcon window command**

```
help grid

grid 0.46um 0.34um 0.23um 0.17um
```
<img width="1366" height="643" alt="command run for grid" src="https://github.com/user-attachments/assets/58a7de6a-c37e-4f57-a787-76ba8a4467ec" />

**Condition 1 verified:**

<img width="1366" height="643" alt="condition1 grid" src="https://github.com/user-attachments/assets/264e815c-91f6-4d52-8fcf-519a3016bd6e" />

**Condition 2 verified:**

<img width="356" height="632" alt="Horizontal pitch" src="https://github.com/user-attachments/assets/4c5df2ff-4398-4d46-aadb-9f81daebfe41" />

<img width="846" height="329" alt="horizontal pitch com" src="https://github.com/user-attachments/assets/0fa803a8-ba60-431d-8a12-a2c21bad3aa7" />

**Condition 3 verified:**

<img width="1071" height="603" alt="condition 3 verified" src="https://github.com/user-attachments/assets/91cc8168-7a09-4dd6-a245-61d3c357bf91" />

**2. Save the finalized layout**

```
save sky130_vsdinv.mag

magic -T sky130A.tech sky130_vsdinv.mag &

```
<img width="1366" height="643" alt="newly saved layout" src="https://github.com/user-attachments/assets/9003e5b8-3cc8-46c2-bc98-1f8a345a84de" />

**3. Create lef file**

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/b1a81ab6-588a-4db4-b66c-14f0ced3bbb0" />

**4. Copy the newly generated lef to 'picorv32a' directory**

```
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

<img width="1366" height="643" alt="lef copy commands" src="https://github.com/user-attachments/assets/4fdd1c51-aaf6-45dc-9b5d-544af9617bf6" />

**5. Edit config.tcl**

```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

<img width="1366" height="643" alt="lef file edited pico" src="https://github.com/user-attachments/assets/0f8b2b2f-d88d-4646-a13c-abf094a7ab64" />

**Run Openlane**

<img width="1366" height="643" alt="run command after 1hr" src="https://github.com/user-attachments/assets/f9e5c09c-6c5e-4d94-9fad-bc0ea4b95150" />

<img width="1366" height="643" alt="run com after 1 hr 2" src="https://github.com/user-attachments/assets/78eee086-76c1-49e0-9124-e7f8e2465c8c" />

<img width="1366" height="643" alt="run com after 1 hr 3" src="https://github.com/user-attachments/assets/d3218de9-2e86-4f4d-be03-19a0ea10656b" />

**6. Introduction of custom inverter cell**

<img width="1366" height="643" alt="time delay run after" src="https://github.com/user-attachments/assets/d7bbe8ff-cc5e-4431-824d-e2598e9d84fb" />

<img width="1366" height="643" alt="area after run" src="https://github.com/user-attachments/assets/db532e97-02a2-4f7a-8c32-b0cb087553bd" />

```
prep -design picorv32a -tag 16-11_12-42 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

echo $::env(SYNTH_STRATEGY)

set ::env(SYNTH_STRATEGY) "DELAY 3"

echo $::env(SYNTH_BUFFERING)

echo $::env(SYNTH_SIZING)

set ::env(SYNTH_SIZING) 1

echo $::env(SYNTH_DRIVING_CELL)

run_synthesis
```

**Increase in area and worst negative slack is reduced to zero**

<img width="1366" height="643" alt="new chip area after run" src="https://github.com/user-attachments/assets/57e6bf82-941d-49e0-9f1d-8cc7ce0af1e3" />

<img width="1366" height="643" alt="new chip time after run" src="https://github.com/user-attachments/assets/0e0cfbc0-e69d-428b-af4c-4787b6a41d1c" />

**7. After custom inverter acceptance run floorplan and placement**

``` run_floorplan```

<img width="1366" height="643" alt="flow failed" src="https://github.com/user-attachments/assets/851fddb2-c4ff-4d5f-a599-88247054bc35" />

Due to an unexpected error change the ```run_floorplan``` command 

```
init_floorplan
place_io
tap_decap_or
```

<img width="1366" height="643" alt="new com for floorplan" src="https://github.com/user-attachments/assets/fae40a14-e98a-42bc-8f69-3d84e28f6b5f" />

<img width="1366" height="643" alt="new com floor2" src="https://github.com/user-attachments/assets/0bf8be41-4a3b-4fd8-8fb9-44191a92aa8a" />

```run_placement```

<img width="1366" height="643" alt="com for placement" src="https://github.com/user-attachments/assets/2eabbe0f-658a-46f2-9c3d-d62fb8e67e34" />

<img width="1366" height="643" alt="run com for placement" src="https://github.com/user-attachments/assets/b97b21e5-c1bc-479d-af73-e33ca104084c" />

<img width="1366" height="643" alt="placement def in magic" src="https://github.com/user-attachments/assets/12d30afd-b4e1-4d71-bacc-12d57905824e" />

<img width="1366" height="643" alt="cell in placement" src="https://github.com/user-attachments/assets/b9353e3c-7b06-404d-a47d-a930a53a3d18" />

<img width="1366" height="643" alt="cell in placement 2" src="https://github.com/user-attachments/assets/b1f55295-154d-4317-a561-56cfee1e369f" />

**8. Do Post-Synthesis timing analysis with OpenSTA tool.**

Newly created `pre_sta.conf` in `openlane` directory 

<img width="1366" height="643" alt="pre sta conf" src="https://github.com/user-attachments/assets/972e67ba-620b-4898-86e7-bcca4ef2744b" />

Newly Created `my_base.sdc` in `openlane/designs/picorv32a/src` directory 

<img width="1366" height="643" alt="mybase1" src="https://github.com/user-attachments/assets/d86cf248-002e-4ee6-8ff7-71b6e6536033" />

<img width="1366" height="643" alt="my base2" src="https://github.com/user-attachments/assets/400551aa-9dca-46b6-bcd4-5111565b65fa" />

```
cd Desktop/work/tools/openlane_working_dir/openlane

sta pre_sta.conf
```

<img width="1366" height="643" alt="sta run1" src="https://github.com/user-attachments/assets/9672c9a6-6283-450d-b69d-35d61742fc13" />

<img width="1366" height="643" alt="sta run2" src="https://github.com/user-attachments/assets/c72ba0ec-eaa3-46b9-9313-d67f501ef6f3" />

<img width="1366" height="643" alt="sta run3" src="https://github.com/user-attachments/assets/4b8631e4-b3c0-4156-ac9a-a10efe60c37f" />

**Commands to include new lef and perform synthesis**

```
prep -design picorv32a -tag 16-11_16-06 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

set ::env(SYNTH_SIZING) 1

set ::env(SYNTH_MAX_FANOUT) 4

echo $::env(SYNTH_DRIVING_CELL)

run_synthesis
```

<img width="1366" height="643" alt="sta new lef" src="https://github.com/user-attachments/assets/fd96b772-57b5-4ba9-a766-beff9c3c727c" />

<img width="1366" height="643" alt="sta new lef run1" src="https://github.com/user-attachments/assets/d8e785c2-b146-4e23-8c24-ece2ca152243" />

<img width="1366" height="643" alt="sta new lef run2" src="https://github.com/user-attachments/assets/f1d4ea3c-deee-4cc8-a6a8-6f2ef614bec6" />

<img width="1366" height="643" alt="sta new lef run3" src="https://github.com/user-attachments/assets/e3cfaa31-e6a0-454d-a20b-33db7aef34db" />

**9. Make timing ECO fixes to remove all violations.**

**OR gate of drive strength 2 is driving 4 fanouts**

<img width="1366" height="643" alt="sta run 4th cts" src="https://github.com/user-attachments/assets/29a20ed1-5bc4-49c1-8934-13a9fcdfbc42" />

```
report_net -connections _11672_

help replace_cell

replace_cell _14510_ sky130_fd_sc_hd__or3_4

report_checks -fields {net cap slew input_pins} -digits 4
```

<img width="1366" height="643" alt="sta run new com cts" src="https://github.com/user-attachments/assets/32e5c6c3-6302-41e8-898b-a4b619f5d44f" />

<img width="1366" height="643" alt="sta run com new2" src="https://github.com/user-attachments/assets/bb7b7d5a-b0dd-4499-8175-cee6cc51ee5f" />

<img width="1366" height="643" alt="sta new com cts3" src="https://github.com/user-attachments/assets/22a74818-dbf4-4f0f-bbb0-850e7657c501" />

**OR gate of drive strength 2 is driving 4 fanouts**

<img width="1366" height="643" alt="sta or2 high" src="https://github.com/user-attachments/assets/c906ccda-78ed-47d0-a30e-90652ab1bda1" />

```
report_net -connections _11675_

replace_cell _14514_ sky130_fd_sc_hd__or3_4

report_checks -fields {net cap slew input_pins} -digits 4
```

**Slack reduced**

<img width="1366" height="643" alt="sta slec red 3rd com" src="https://github.com/user-attachments/assets/7ecb282b-f844-4a6b-8139-8aa39cf3ff87" />

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/e2c83287-aaa6-4a2a-9d5b-97d08a7b77ac" />

Commands to verify instance `_14506_` is replaced with `sky130_fd_sc_hd__or4_4`

```
report_checks -from _29043_ -to _30440_ -through _14506_
```
<img width="1366" height="643" alt="replaced instance" src="https://github.com/user-attachments/assets/e3177ef1-ad28-4607-aefe-d978deb63d73" />

**10. Replace the old netlist with the new netlist generated after timing ECO fix**

Command to make copy of netlist
```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-11_16-06/results/synthesis/

ls

cp picorv32a.synthesis.v picorv32a.synthesis_old.v

ls
```


<img width="1366" height="643" alt="fixed eco new netlist com" src="https://github.com/user-attachments/assets/b6e772aa-040d-47a8-b52b-913a7bbf1c62" />

```
help write_verilog

write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-11_16-06/results/synthesis/picorv32a.synthesis.v

exit
```

 **To check if instance *_14506_* is replaced with *sky130_fd_sc_hd__or4_4***

 
<img width="915" height="500" alt="image" src="https://github.com/user-attachments/assets/0c853756-f9c0-4a12-a8ef-a3b63881ab48" />

Command to load the design

```
prep -design picorv32a -tag 16-11_16-06 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

set ::env(SYNTH_STRATEGY) "DELAY 3"

set ::env(SYNTH_SIZING) 1

run_synthesis

init_floorplan
place_io
tap_decap_or

run_placement

unset ::env(LIB_CTS)

run_cts
```

<img width="911" height="503" alt="image" src="https://github.com/user-attachments/assets/c5897805-5088-4c9a-9cfe-4692be4a179b" />

<img width="910" height="498" alt="image" src="https://github.com/user-attachments/assets/3652155a-5dc3-479a-8c77-ba51c490e6b7" />



## Lab Implementations-*SECTION-5*

**1. Perform generation of Power Distribution Network (PDN)**


```
cd Desktop/work/tools/openlane_working_dir/openlane

docker

./flow.tcl -interactive

package require openlane 0.9

prep -design picorv32a

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

set ::env(SYNTH_STRATEGY) "DELAY 3"

set ::env(SYNTH_SIZING) 1

run_synthesis

init_floorplan
place_io
tap_decap_or

run_placement

unset ::env(LIB_CTS)

run_cts

gen_pdn 

```

<img width="1366" height="643" alt="cts run success" src="https://github.com/user-attachments/assets/99edc695-61cd-450f-9005-41655396b56b" />

<img width="1366" height="643" alt="pdn run success" src="https://github.com/user-attachments/assets/d21ef803-e925-4fd6-a352-8d39343f12bc" />

<img width="1366" height="643" alt="pdn in magic" src="https://github.com/user-attachments/assets/ed6ab2bd-6ac8-486e-98fe-704e3c12e5b3" />

<img width="1366" height="643" alt="pdn in magic 2" src="https://github.com/user-attachments/assets/8ba5a256-ed9c-4691-a42e-096e34562e30" />

**2. Perfrom detailed routing using TritonRoute**

```
echo $::env(CURRENT_DEF)

echo $::env(ROUTING_STRATEGY)

run_routing
```

<img width="1366" height="643" alt="routing complete" src="https://github.com/user-attachments/assets/a27e1872-fc23-4d1d-9715-744a270bd0bd" />

**Screenshot of routed def**

<img width="1366" height="643" alt="routed def1" src="https://github.com/user-attachments/assets/98a5209f-c6c0-4736-905d-e2299695ef6d" />

<img width="1366" height="643" alt="routed def2" src="https://github.com/user-attachments/assets/a1bf0006-1a60-40f3-b02f-612b727103db" />

<img width="1366" height="643" alt="routed def3" src="https://github.com/user-attachments/assets/602bf4b9-aebd-415e-8874-6648ead36a67" />

**3. Post-Route parasitic extraction using SPEF extractor.**

```
cd Desktop/work/tools/SPEF_EXTRACTOR

python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-11_16-06/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/16-11_16-06/results/routing/picorv32a.def
```

**4. Post-Route OpenSTA timing analysis**

```
openroad

read_lef /openLANE_flow/designs/picorv32a/runs/16-11_16-06/tmp/merged.lef

read_def /openLANE_flow/designs/picorv32a/runs/16-11_16-06/results/routing/picorv32a.def

write_db pico_route.db

read_db pico_route.db

read_verilog /openLANE_flow/designs/picorv32a/runs/16-11_16-06/results/synthesis/picorv32a.synthesis_preroute.v

read_liberty $::env(LIB_SYNTH_COMPLETE)

link_design picorv32a

read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

set_propagated_clock [all_clocks]

read_spef /openLANE_flow/designs/picorv32a/runs/16-11_16-06/results/routing/picorv32a.spef

report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

exit
```

<img width="1366" height="643" alt="postroute 1" src="https://github.com/user-attachments/assets/85a2e681-e449-404c-bc01-2c919f6a7eb5" />

<img width="1366" height="643" alt="postroute 2" src="https://github.com/user-attachments/assets/ba09736b-a69c-40e2-a1c9-f2945c26a957" />

<img width="1366" height="643" alt="postroute 3" src="https://github.com/user-attachments/assets/a0a494e3-603c-481a-99f2-0f1ee1915690" />

<img width="1366" height="643" alt="postroute 4" src="https://github.com/user-attachments/assets/5fcd5ffc-2277-4ca4-a8e0-79b73f1cf550" />




















































































































































