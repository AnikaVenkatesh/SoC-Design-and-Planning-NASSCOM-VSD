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

## Lab Implementations 

 *SECTION-1*

 1. To Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

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
Screenshots of the steps

<img width="1280" height="768" alt="Starting commands" src="https://github.com/user-attachments/assets/010c858a-0a48-47cc-85a0-1ca1eca80cf9" />

<img width="1280" height="768" alt="starting com2" src="https://github.com/user-attachments/assets/61cabe68-51cd-4919-9f3c-ac08359e7211" />

<img width="1280" height="768" alt="starting_com3" src="https://github.com/user-attachments/assets/a4753326-aa79-40be-ae22-9bc9552e3ecc" />

2. To calculate the flop ratio

<img width="1280" height="768" alt="folder creation" src="https://github.com/user-attachments/assets/68a2e8dc-dc93-436c-9b6a-d9602e6cd9f9" />

<img width="1280" height="768" alt="no of cells" src="https://github.com/user-attachments/assets/9179fbb4-d9b1-4a58-811e-ad1014a83526" />

<img width="1280" height="768" alt="no of dfft" src="https://github.com/user-attachments/assets/b82ac8a8-f30d-41f7-aca3-4fe25cdaee09" />

Calculation of Flop Ratio and DFF % from synthesis statistics report file

### Flop Ratio Calculation

The flop ratio is calculated using the total number of flip-flops divided by the total number of cells:

$$
\text{Flop Ratio} = \frac{1613}{14876} = 0.108429685
$$

The percentage of DFFs is obtained by multiplying the flop ratio by 100:

$$
\text{DFF Percentage} = 0.108429685 \times 100 = 10.84296854\%
$$

*SECTION-2*

1. To Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

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

Screenshots

<img width="1366" height="643" alt="run floorplan" src="https://github.com/user-attachments/assets/1cdf5cb6-c425-4c78-8c52-ba2916efdeed" />

<img width="1366" height="643" alt="run floorplan2" src="https://github.com/user-attachments/assets/fa1d3514-c5d8-4976-813a-1bb93cbb757f" />

2. To calulate diarea

<img width="1366" height="643" alt="Diarea" src="https://github.com/user-attachments/assets/cd08972a-8656-4e5d-912c-82fe3e0c07e6" />

1000 Unit Distance = 1 Micron

Die width (units)  = 660685
Die height (units) = 671405

Die width in microns  = 660685 / 1000 = 660.685 µm
Die height in microns = 671405 / 1000 = 671.405 µm

Die Area = 660.685 × 671.405 = 443587.212425 µm²

3. Load generated floorplan def in magic tool

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-11_09-50/results/floorplan/


magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```


Screenshots of floorplan def in magic:

<img width="1366" height="643" alt="explore fp1 centre" src="https://github.com/user-attachments/assets/ef589252-49c9-433f-b0cd-ae5d1cb138ba" />

Equidistant placement of ports:

<img width="1366" height="643" alt="explore fp2" src="https://github.com/user-attachments/assets/32d2fdba-3a6c-4376-acd0-f2f00e67db31" />

Port layer as set through config.tcl:

<img width="1366" height="643" alt="explore fp3 hori pin" src="https://github.com/user-attachments/assets/00557a42-ef2d-4c4e-83e5-22c6b584f8e5" />

<img width="1366" height="643" alt="explore fp4 vert pin" src="https://github.com/user-attachments/assets/cb4eec00-9d3c-4eb9-9209-e976f12f4843" />

Decap Cells and Tap Cells:

<img width="1366" height="643" alt="explore fp5 decap andtap" src="https://github.com/user-attachments/assets/32803817-29b5-48cb-a70d-edd373cb8f91" />

Diagonally Equidistant Tap cells:

<img width="1366" height="643" alt="explore fp6 diagnally distant tap" src="https://github.com/user-attachments/assets/41ef0cea-9ebe-4a41-aca7-2637a402e47c" />

Unplaced standard cells at the origin

<img width="1366" height="643" alt="explore fp7 std cell" src="https://github.com/user-attachments/assets/be036942-913c-41f6-9984-88bb210dbb9b" />

4. Run 'picorv32a' design congestion aware placement

```
run_placement
```
Screenshots of the command

<img width="1366" height="643" alt="run placement" src="https://github.com/user-attachments/assets/c84661f1-432f-4cc5-a7e4-09c9952c144c" />

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/14-11_16-02/results/placement/


magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```

floorplan def in magic at the centre


<img width="1366" height="643" alt="placement centre" src="https://github.com/user-attachments/assets/81c84912-0650-4420-b370-5240ffd974c7" />

Standard cells legally placed

<img width="1366" height="643" alt="placement legally placed" src="https://github.com/user-attachments/assets/32e00a75-2d79-4e08-8fef-499a3da81628" />

*SECTION-3*

1. To clone custom inverter standard cell design from github repository

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

2. To load the custom inverter layout in magic

<img width="1366" height="643" alt="inverter view" src="https://github.com/user-attachments/assets/82265d22-5edc-471a-8667-254d79e3b463" />

NMOS

<img width="1366" height="643" alt="nmos" src="https://github.com/user-attachments/assets/9873f568-6f3b-4455-ba54-409c20dc0aa6" />

PMOS

<img width="1366" height="643" alt="pmos" src="https://github.com/user-attachments/assets/62200890-2a65-4f7c-8631-022bb4dd3ad2" />

PMOS source connectivity to VPWR verified

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/890865e5-5d0c-4a9d-8753-6410018619ac" />

NMOS source connectivity to VSS VGND verified

<img width="1366" height="643" alt="nmos conn gnd" src="https://github.com/user-attachments/assets/df793064-96d2-418e-85ad-3bbc21c2534a" />

Output Y connected to PMOS and NMOS verified 

<img width="1366" height="643" alt="y conn" src="https://github.com/user-attachments/assets/6413ca94-98d5-4af8-b85f-27b113ca39a6" />

Deleting necessary layout to check for DRC error

<img width="1366" height="643" alt="deleting drc" src="https://github.com/user-attachments/assets/9adb4856-6906-42db-852f-ee6f4e9698bb" />

<img width="1366" height="643" alt="drc error" src="https://github.com/user-attachments/assets/0cdb9906-ca9a-4247-9a8d-2cf8768a4ad5" />

3. To spice extraction of inverter in magic.

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

4. Editing spice file prior to ngspice simulations

<img width="1366" height="643" alt="image" src="https://github.com/user-attachments/assets/b3e692fb-113e-4900-9fd3-f9312b53fb88" />

5. ngspice simulations

Commands

```
ngspice sky130_inv.spice

plot y vs time a
```

<img width="1366" height="643" alt="ngspice run1" src="https://github.com/user-attachments/assets/bc6e7ade-9600-48ab-9567-80768ec63179" />

<img width="1366" height="643" alt="ngspice plot command" src="https://github.com/user-attachments/assets/7d56f31b-232f-4ced-953b-c27bc1982575" />

<img width="1366" height="643" alt="ng plot full" src="https://github.com/user-attachments/assets/c78ff238-bc83-4f55-9c3a-a70ccb7b3d3c" />

Rise transition:

Output to rise 80%

<img width="1366" height="643" alt="rise 80" src="https://github.com/user-attachments/assets/11d212c4-e4e4-47ca-a69c-27826ea61e0f" />

<img width="1366" height="643" alt="rise 80 coordinate" src="https://github.com/user-attachments/assets/25e50487-3056-49af-84cb-1d8fa8c54992" />

Output to rise 20%

<img width="1366" height="643" alt="rise 20" src="https://github.com/user-attachments/assets/d87938c8-909f-42cd-971c-a2346b5f3d71" />

<img width="1366" height="643" alt="rise 20 coordinate" src="https://github.com/user-attachments/assets/6afdda21-b6b9-4994-b725-5f48e425f589" />

Rise Transition Time Calculation

Given:
- 20% of output = 6.18212 ns
- 80% of output = 6.24595 ns

Formula:
Rise Transition Time = Time at 80% − Time at 20%

Calculation:
Rise Transition Time = 6.24595 ns − 6.18212 ns
                      = 0.06383 ns
                      = 63.83 ps

Fall transition:

Output to fall 80%

<img width="1366" height="643" alt="fall 80" src="https://github.com/user-attachments/assets/b892221e-dd89-4729-ae5f-e96c543df5c4" />

<img width="1366" height="643" alt="fall 80 coordinate" src="https://github.com/user-attachments/assets/7822b57a-c254-4a2e-818d-c988e0400d68" />

Output to fall 20%

<img width="1366" height="643" alt="fall 20 plot" src="https://github.com/user-attachments/assets/14b1ff5b-3a78-4bfa-82d9-9f06e75bf1ed" />

<img width="1366" height="643" alt="fall 20 coordinate" src="https://github.com/user-attachments/assets/3203a017-1018-4730-874e-319e23e0bd9c" />

Fall Transition Time Calculation

Given:
- 80% of output = 8.05278 ns
- 20% of output = 8.09530 ns

Formula:
Fall Transition Time = Time at 20% − Time at 80%

Substitution:
Fall Transition Time = 8.09530 ns − 8.05278 ns

Result:
Fall Transition Time = 0.04252 ns = 42.52 ps


Rise Cell Delay:

50% Screenshots

<img width="1366" height="643" alt="rise cell delay" src="https://github.com/user-attachments/assets/3552bdae-99e6-463a-a333-1971037bdf53" />

<img width="1366" height="643" alt="rise cell del coordinate" src="https://github.com/user-attachments/assets/eda8e7d3-8543-4bc4-9998-3ec62da617cb" />

Rise Cell Delay Calculation

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

Fall Cell Delay:

<img width="1366" height="643" alt="fall cell delay plot" src="https://github.com/user-attachments/assets/2c655702-e5f0-435e-b9e6-62abf53b0b21" />

<img width="1366" height="643" alt="fall cell delay coordinate" src="https://github.com/user-attachments/assets/9b4ef248-ea3b-45dd-9dd5-f86dee7d8a9a" />

**Fall Cell Delay Calculation**

Fall Cell Delay = Time taken for output to fall to 50% − Time taken for input to rise to 50%

50% of 3.3 V = 1.65 V

Given:
- Output fall 50% crossing time = **1.20777 ns**
- Input rise 50% crossing time = **1.20503 ns**

Fall Cell Delay = 1.20777 ns − 1.20503 ns  
                 = **0.00274 ns**  
                 = **2.74 ps**




































































