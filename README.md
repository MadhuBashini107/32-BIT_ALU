# 32-BIT_ALU Simulation and Synthesis

## Aim:
Write a Verilog code for a 32-bit ALU supporting four logical and four arithmetic operations. Use case statements in behavioural modelling.
To verify functionality using the Test Bench, synthesize and analyse area and Power reports of a 32 Bit ALU design 

## Tool Required:
Functional Simulation: Incisive Simulator (ncvlog, nclaunch, ncsim)

Synthesise using Genus

## Design Information and Block Diagram:
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators.

<img width="668" height="344" alt="image" src="https://github.com/user-attachments/assets/1195efe3-e2dd-443c-8bf0-be1579c06533" />

#### Fig 1: Block Diagram of 32 Bit ALU

## Creating a Workspace:

Create a folder in your name (Note: Give folder name without any space) and create a new sub-Directory name it as Exp3 or alu_32bit for the Design and open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_32bit.v)

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

#### a)	To verify the Functionality using the Test Bench

## Source Code – Using Case Statement :
```verilog
module alu_32(input [31:0]a,
input [31:0]b,
input [2:0]op,
output reg [31:0]res);
always@(*)
begin
	case(op)
		3'b000: res = a+b;
		3'b001: res = a-b;
		3'b010: res = a&b;
		3'b011: res = a|b;
		3'b100: res = ~(a&b);
		3'b101: res = ~(a|b);
		3'b110: res = a^b;
		3'b111: res = a<<1;
		default: res = 32'd0;
	endcase
end
endmodule
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

## Creating a Test Bench:

Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_32bit_tb_case).

## Test Bench :
```verilog
module alu_32_tb;
reg [31:0]a;
reg [31:0]b;
reg [2:0]op;
wire [31:0]res;
alu_32 uut (a,b,op,res);
initial
begin
	a = 32'd10;#10;
	b = 32'd5;#10;
	op = 3'b000;#10;
	op = 3'b001;#10;
	op = 3'b010;#10;
	op = 3'b011;#10;
	op = 3'b100;#10;
	op = 3'b101;#10;
	op = 3'b110;#10;
	op = 3'b111;#10;
	$finish;
end
endmodule
	
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

## Functional Simulation:

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/777cdf12-86de-4392-8d71-97db6a4d4099" />


#### Fig 2: Invoke the Cadence Environment

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/04e9d78e-5985-4f49-9025-37e24e5b825d" />


#### Fig 3: Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option

<img width="1919" height="1079" alt="Screenshot 2026-02-24 110826" src="https://github.com/user-attachments/assets/1d5fc52f-e7a5-42b5-82af-e4c0a796b848" />

#### Fig 4:cds.lib file Creation
Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below
 
#### Fig 5: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.

<img width="1915" height="1075" alt="image" src="https://github.com/user-attachments/assets/c9e642bf-2566-4ca2-8206-c791eacb495d" />


#### Fig 6: Nclaunch Window

### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#### Steps for compilation:
1.	Create work/library directory (most of the latest simulation tools creates automatically)
   
2.	Map the work to library created (most of the latest simulation tools creates automatically)
   
3.	Run the compile command with compile options

i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code
Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

#### Fig 7: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

<img width="1912" height="1073" alt="image" src="https://github.com/user-attachments/assets/ecfdcb96-6519-4825-a5a1-23114b737f11" />


### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#### Steps for elaboration
– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.
<img width="1919" height="1072" alt="image" src="https://github.com/user-attachments/assets/0df5f9c6-1b5a-4e9f-bfca-aa1f8ebc0897" />


#### Fig 8: Elaboration Launch Option

### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options
<img width="1917" height="1079" alt="image" src="https://github.com/user-attachments/assets/fc295763-9b2f-4c5e-97e9-c1a9b0f268e4" />


#### Fig 9: Design Browser window for simulation

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/8d8009bc-9510-4150-8b88-440e919a54c3" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/0350b034-1f66-4e4b-be24-1b9ed68a8799" />

#### Fig 10: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/22464883-e7db-4da3-883e-bbab5a5777a9" />


### Performing Synthesis
The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

#### Fig 11: Synthesis RTL Schematic 
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5c62e756-febd-4da6-9442-1bf823ce41ac" />


#### Fig 12: Area report
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/b0e7953c-ef3b-4df8-a9ef-ed30c3a0ee71" />


#### Fig 13: Power Report
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/57216e40-db56-4082-8c2a-b1f3faea4bb5" />

## Result
The functionality of the 32-bit ALU was successfully verified using a test bench and simulated with the nclaunch tool. Additionally, the generic netlist of the 32-bit ALU was generated, and the corresponding area and power reports were analyzed and tabulated using Cadence Genus.
