# 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task

# Aim
To design and simulate a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment. 

# Apparatus Required
Vivado 2023.1
# Procedure
1. Launch Vivado 2023.1
Open Vivado and create a new project.
2. Design the Verilog Code
Write the Verilog code for the seven-segment display, defining the logic that maps a 4-bit binary input to the corresponding segments (a to g) of the display.
3. Create the Testbench
Write a testbench to simulate the seven-segment display behavior. The testbench should apply various 4-bit input values and monitor the corresponding output.
4. Create the Verilog Files
Create both the design module and the testbench in the Vivado project.
5. Run Simulation
Run the behavioral simulation to verify the output. 
6. Observe the Waveforms
Analyze the output waveforms in the simulation window, and verify that the correct segments light up for each digit.
7. Save and Document Results
Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Verilog Code

# 4 bit Ripple Adder using Task
```
`timescale 1ns/1ps 
module rca4(a,b,cin,sum,cout);
input [3:0] a,b;
input cin;
output reg [3:0] sum;
output reg cout;
reg [4:0] temp;
task ripple_add;
input [3:0] x,y;
input c_in;
output [3:0] s;
output c_out;
reg [4:0] t;
begin
t = x + y + c_in; 
s = t[3:0];
c_out = t[4];
end
endtask
always @(*) begin
ripple_add(a,b,cin,sum,cout);
end
endmodule

```

# Test Bench
```
module tb_rca4;
reg [3:0] a,b;
reg cin;
wire [3:0] sum;
wire cout;
rca4 uut(a,b,cin,sum,cout);
initial begin
$monitor("T=%0t | a=%b | b=%b | cin=%b | sum=%b | cout=%b",$time,a,b,cin,sum,cout);
a=4'b1010; b=4'b0101; cin=0;
#10;
a=4'b1111; b=4'b0001; cin=1;
#10;
a=4'b1001; b=4'b0110; cin=0;
#10;
a=4'b1110; b=4'b1111; cin=1;
#10;
end
endmodule

```

# Output Waveform


<img width="1920" height="1080" alt="Screenshot (105)" src="https://github.com/user-attachments/assets/2abb7a03-d73d-4299-a89d-b652de54c945" />



# 4 bit Ripple counter using Function
```

`timescale 1ns / 1ps

module ripple_counter_4bit(clk, rst, q);
input clk, rst;
output reg [3:0] q;

function [3:0] i;
input [3:0] data;
begin
i = data + 1;
end
endfunction

always @(posedge clk or posedge rst) begin
if (rst)
q <= 4'b0000;
else
q <= i(q);
end
endmodule
```

# Test Bench
```
module tb_ripple_counter_4bit;
reg clk, rst;
wire [3:0] q;
ripple_counter_4bit uut(clk, rst, q);
always #5 clk = ~clk;
initial begin
$monitor("T=%0t | rst=%b | q=%b (%0d)", $time, rst, q, q);
clk = 0;
rst = 1;  
#10 rst = 0; 
#100;
$finish;
end
endmodule
```


# Output Waveform 

<img width="1920" height="1080" alt="Screenshot (106)" src="https://github.com/user-attachments/assets/29d3364c-8075-433e-8823-ae1b80ee75dc" />




# Conclusion
In this experiment, a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task was successfully designed and simulated using Verilog HDL.
