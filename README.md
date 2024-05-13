![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/0ee7331e-ecae-445e-9b53-8313685ecc7b)# VLSI-LAB-EXP-4
SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.2.

APPARATUS REQUIRED:

Vivado 2023.2

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


  
PROCEDURE:
Open Vivado: Launch Xilinx Vivado software on your computer.

Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

VERILOG CODE:

FLIP FLOP:

SR FLIP FLOP:

PROGRAM:
```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```
OUTPUT

![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/49085f3f-14bd-4da2-8d2b-2b450eeb2fd2)

JK FLIP FLOP:

PROGRAM:
```
module jkff(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```

OUTPUT:

![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/ec615bb5-3888-46ee-82e8-d8cdb1a43ac0)

T FLIP FLOP:

PROGRAM:
```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```

OUTPUT:

![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/37375d1d-74fa-44e1-b337-e39c8c92d3c2)

D FLIP FLOP:

PROGRAM:
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```

OUTPUT:

![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/6eadd308-6d77-408f-a675-da134e41945b)

COUNTER:

UPDOWN COUNTER:

PROGRAM:

```
module updowncounter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always @(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if (updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```

OUTPUT:

![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/4f3dc1b5-07e0-4338-9411-58f23794545b)

MOD10 COUNTER:

PROGRAM:
```
module mod10counter(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always @(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```
OUTPUT:

![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/605e3578-0ac3-471f-92a1-83ed90021693)

RIPPLE COUNTER:

PROGRAM:
```
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule

module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule

module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf1(q[0],clk,rst);
tff tf3(q[2],q[1],rst);
tff tf4(q[3],q[2],rst);
endmodule
```

OUTPUT:

![image](https://github.com/Mohanasankaran/VLSI-LAB-EXP-4/assets/161284142/8aca9414-a24a-4f83-8892-2eeb9a1de777)



RESULT:
Hence SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.2 is simulated and synthesised.


