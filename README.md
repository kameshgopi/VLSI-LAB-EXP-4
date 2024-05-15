# VLSI-LAB-EXP-4
SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

APPARATUS REQUIRED:
Vivado 2023.1

Procedure:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

**SR FLIPFLOP**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)

# VERILOG CODE

# SR Flip Flop
```
module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
OUTPUT WAVEFORM

# SR Flip Flop

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/490da3e1-1a57-475f-81eb-efd9f0417945)

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/1ec8aa9f-077c-42fb-a3e5-7c2261e8ec59)

**JK FLIPFLOP**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

# VERILOG CODE

# JK Flip Flop
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
OUTPUT WAVEFORM

# JK Flip flop

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/31ce26b8-a919-4e57-8fae-6a682bbc32b2)

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/2cc1bae8-b37c-42e2-80b9-65af395e1600)

**T FLIPFLOP**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

# VERILOG CODE

# T Flip Flop
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
OUTPUT WAVEFORM

# T Flip FLop

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/9cbfe9c5-3097-4891-ab4f-20e943abd62d)

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/e65a06d2-e5d9-46ec-9949-31bf09db501f)


**D FLIPFLOP**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

# VERILOG CODE

# D Flip Flop
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```

OUTPUT WAVEFORM

# D Flip Flop

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/3827d520-2d02-49f6-a673-aeb3849bfe78)

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/031293dd-0998-49e6-9ec1-ef7925b90772)



**COUNTER**


![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

# VERILOG CODE

# Ripple Carry Counter
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```

OUTPUT WAVEFORM

# RIPPLE CARRY COUNTER

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/fa262614-ddcd-452d-86b2-5010940e2325)

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/d4707ff6-b0f9-4606-ab6d-13e3134ac745)

# MOD 10 Counter
**VERILOG CODE**
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
OUTPUT WAVEFORM

# MOD-10 COUNTER

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/fecdf582-0098-46f0-be88-442bfef0526b)

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/2506a3ea-6f61-4596-a76e-5aee72c1ae10)

UP-DOWN COUNTER

**VERILOG CODE:**
~~~
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
~~~

OUTPUT WAVEFORM

# UP DOWN COUNTER

![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/2f103427-d2a4-4986-854b-4bff3784bec9)


![image](https://github.com/kameshgopi/VLSI-LAB-EXP-4/assets/164839944/35ef2783-6478-4b78-8ba4-2b29ec8dac4e)



RESULT:
Thus the simulation and implementation of sequential logic gates is done and verified.


