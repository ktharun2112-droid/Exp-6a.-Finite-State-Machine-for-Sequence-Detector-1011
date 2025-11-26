# Exp-6a.-Finite-State-Machine-for-Sequence-Detector-1011
# Aim 
To design and simulate a Finite-State-Machine-for-Sequence-Detector-1011 using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment. 

# Apparatus Required 

Vivado 2023.1 

# Procedure

Launch Vivado 2023.1 Open Vivado and create a new project.
Design the Verilog Code Write the Verilog code for the RAM,ROM,FIFO
Create the Testbench Write a testbench to simulate the memory behavior. The testbench should apply various and monitor the corresponding output.
Create the Verilog Files Create both the design module and the testbench in the Vivado project.
Run Simulation Run the behavioral simulation to verify the output.
Observe the Waveforms Analyze the output waveforms in the simulation window, and verify that the correct read and write operation.
Save and Document Results Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.
# Code
# Mealy 1011
// Verilog code

// Test bench

// output Waveform
# Moore 1011
```
`timescale 1ns / 1ps
module MOORE(clk,reset,in,out);
 input clk;
 input reset;
 input in; 
 output reg out; 
 
 parameter S0 = 3'b000, 
 S1 = 3'b001, 
 S2 = 3'b010, 
 S3 = 3'b011,
 S4 = 3'b100; 
 reg [2:0] current_state, next_state;
always @(posedge clk or posedge reset) 
 begin
 if (reset)
 current_state <= S0;
 else
 current_state <= next_state;
 end
always @(*) 
begin
 case (current_state)
 S0: if (in) 
 next_state <= S1; 
 else 
 next_state <= S0;
 S1: begin
 if (in)
 next_state <= S1;
 else
 next_state <= S2;
 end
 S2: begin
 if (in)
 next_state <= S3;
 else
 next_state <= S0;
 end
 S3: begin
 if (in)
 next_state <= S4;
 else
 next_state <= S2;
 end
S4: begin
 if (in)
 next_state <= S1;
 else
 next_state <= S0; 
 end
 default: next_state <= S0;
 endcase
 end
always @(*) 
 begin
 case (current_state)
 S4: out = 1'b1;
 default: out = 1'b0;
 endcase
 end
endmodule
```
// Test bench
```
module tb_MOORESEQUENCE;
 reg clk, reset, in;
 wire out;
 MOORE uut (clk,reset,in,out);
 initial 
 begin
 clk = 0;
 forever #5 clk = ~clk;
 end
 initial 
 begin
 reset = 1;
 in = 0;
 #12 reset = 0;
 in = 1; #10;
 in = 0; #10; 
 in = 1; #10; 
 in = 1; #10;
  
 in = 1; #10;
 in = 1; #10;
 in = 0; #10;
 in = 0; #10;
 #20 $finish;
 end
endmodule
```
// output Waveform

<img width="1919" height="1079" alt="Screenshot 2025-11-11 205127" src="https://github.com/user-attachments/assets/b1c4ebe3-9f61-4504-bc52-ec23ba0b79c8" />




Conclusion
The Mealy and Moore state machine for sequence 1011 was designed and successfully simulated using Verilog HDL. The testbench verified both the write and read functionalities by simulating the sequence operations and observing the output waveforms.
