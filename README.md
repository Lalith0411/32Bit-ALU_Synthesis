# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)
```
module alu_32bit_case(y, a, b, f);
  input [31:0] a;
  input [31:0] b;
  input [2:0] f;
  output reg [31:0] y;

  always @(*) begin
    case(f)
      3'b000: y = a & b;       // AND
      3'b001: y = a | b;       // OR
      3'b010: y = ~(a & b);    // NAND
      3'b011: y = ~(a | b);    // NOR
      3'b100: y = a + b;       // ADD
      3'b101: y = a - b;       // SUB
      3'b110: y = a * b;       // MUL
      default: y = 32'bx;      // Undefined
    endcase
  end

endmodule

```
```
module test_alu_32bit_case;

  reg [31:0] a;
  reg [31:0] b;
  reg [2:0] f;
  wire [31:0] y;

  // Instantiate the ALU module
  alu_32bit_case uut (
    .y(y),
    .a(a),
    .b(b),
    .f(f)
  );

  initial begin
    // Test AND
    a = 32'hAAAAAAAA; b = 32'h55555555; f = 3'b000; #10;
    
    // Test OR
    a = 32'hAAAAAAAA; b = 32'h55555555; f = 3'b001; #10;

    // Test NAND
    a = 32'hFFFFFFFF; b = 32'h00000000; f = 3'b010; #10;

    // Test NOR
    a = 32'h00000000; b = 32'h00000000; f = 3'b011; #10;

    // Test ADD
    a = 32'd100; b = 32'd25; f = 3'b100; #10;

    // Test SUB
    a = 32'd100; b = 32'd25; f = 3'b101; #10;

    // Test MUL
    a = 32'd10; b = 32'd3; f = 3'b110; #10;

    // Test default
    f = 3'b111; #10;

    $finish;
  end

endmodule

```
```
read_libs /cadence/install/FOUNDRY-01/digital/90nm/dig/lib/slow.lib
read_hdl alu_32bit_.v
elaborate
syn_generic
report_area
syn_map
report_area
syn_opt
report_area 
report_area > alu_area.txt
report_power > alu_power.txt
report_timing > alu_timing.txt
report_ gates > alu_gates.rpt
write_hdl >alu_netlist.v
gui_show

```
### Step 2 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![Screenshot 2025-05-19 160110](https://github.com/user-attachments/assets/87d3070a-55dd-42af-ba4f-3244b9c05101)


#### Area report:
![Screenshot 2025-05-19 160321](https://github.com/user-attachments/assets/df3fbf11-c6e6-4bdb-a53b-b6f81dbfe4ad)


#### Power Report:
![Screenshot 2025-05-19 160333](https://github.com/user-attachments/assets/945f5135-ed16-4533-9711-79e3a64e5463)


#### Result: 

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
