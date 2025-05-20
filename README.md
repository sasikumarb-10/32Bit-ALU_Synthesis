# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)
![Screenshot 2025-05-19 093528](https://github.com/user-attachments/assets/90567819-ca76-4d99-afce-c11775f71687)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

### Design Code

module ALU ( input [3:0] A, B, input [2:0] ALU_Sel, output reg [3:0] ALU_Out, output reg
CarryOut );
```
e
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
![Screenshot 2025-05-20 140433](https://github.com/user-attachments/assets/4bf8f5e9-1e46-4a97-a26c-c5a3be3d7ff5)

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc
![Screenshot 2025-05-20 140633](https://github.com/user-attachments/assets/c2b4b5d7-38f7-4a37-8a12-8432b0b26883)

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![Screenshot 2025-05-20 140808](https://github.com/user-attachments/assets/81be9cf5-52c1-4acd-990d-c8b790cb8313)

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![Screenshot 2025-05-20 113729](https://github.com/user-attachments/assets/c7d62436-3264-4962-a30f-5eaaa8ee0bb9)

#### Area report:
![Screenshot 2025-05-20 115232](https://github.com/user-attachments/assets/8db436ba-b2c3-4a9b-8e6a-e264210e42a5)

#### Power Report:
![Screenshot 2025-05-20 115324](https://github.com/user-attachments/assets/65cf84cc-009a-4c9a-a988-3da48d4d4e66)


#### Result: 
![Screenshot 2025-05-20 115153](https://github.com/user-attachments/assets/0b63b2cc-5b79-4aba-8c34-bf072853d0bd)

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
