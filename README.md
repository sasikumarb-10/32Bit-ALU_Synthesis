# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)
![Screenshot 2025-05-19 093528](https://github.com/user-attachments/assets/d2601c34-c0a1-4300-a191-cab619c2886c)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

### Design Code:
module ALU ( input [3:0] A, B, input [2:0] ALU_Sel, output reg [3:0] ALU_Out, output reg
CarryOut );

```
always @(*) begin
 case (ALU_Sel)
 3'b000: {CarryOut, ALU_Out} = A + B;
 3'b001: {CarryOut, ALU_Out} = A - B;
 3'b010: ALU_Out = A & B;
 3'b011: ALU_Out = A | B;
 3'b100: ALU_Out = A ^ B;
 3'b101: ALU_Out = ~A;
 3'b110: ALU_Out = A << 1;
 3'b111: ALU_Out = A >> 1;
 default: ALU_Out = 4'b0000;
 endcase
end
endmodule
```
### TestBench:
module ALU_tb; reg [3:0] A, B; reg [2:0] ALU_Sel; wire [3:0] ALU_Out; wire CarryOut;
```
ALU uut (
 .A(A),
 .B(B),
 .ALU_Sel(ALU_Sel),
 .ALU_Out(ALU_Out),
 .CarryOut(CarryOut)
);
initial begin
 A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
 A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
 A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
 A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
 A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
 $finish;
end
endmodule
```
### Step 2 : Performing Synthesis

The Liberty files are present in the library path,
![Screenshot 2025-05-20 142337](https://github.com/user-attachments/assets/f0848c86-25cc-402a-99ea-dc8b9d7b237d)

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh
◦ source /cadence/install/cshrc
![Screenshot 2025-05-20 140633](https://github.com/user-attachments/assets/1b260bf0-124f-4a8d-b2e6-988c60c91935)

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![Screenshot 2025-05-20 140808](https://github.com/user-attachments/assets/6aa3ff06-aaab-423c-b044-24f2e19b697e)

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![Screenshot 2025-05-20 113729](https://github.com/user-attachments/assets/f24e7b62-4ec5-4a59-8e74-5e01c78d8a59)

#### Area report:
![Screenshot 2025-05-20 115232](https://github.com/user-attachments/assets/240ae63e-c887-4b97-8f50-9ae4dc3fa6e6)

#### Power Report:
![Screenshot 2025-05-20 115324](https://github.com/user-attachments/assets/9ffe230b-d038-4b0a-89a5-5321b62c597c)

#### Result: 
![Screenshot 2025-05-20 115153](https://github.com/user-attachments/assets/be3346af-ff3e-4ddc-8220-0002bc7c3019)

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
