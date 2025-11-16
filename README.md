# Clock Divider (Divide-by-10)
# Aim:
To design, implement, and simulate a clock divider circuit that divides the input clock frequency by 10, using Verilog HDL and to verify its behavior using a Testbench.
# Software / Tools Used:
 Verilog HDL

Any HDL Simulator (Modelsim, QuestaSim, Vivado, iverilog, etc.)

GTKWave (optional for viewing waveforms)
# Module Description:
1. Clock Divider Module

Counts input clock cycles and toggles the output clock after the specified count.

2. Testbench Module

Generates input clock and reset, instantiates the DUT, and simulates its behavior.
# Verilog Code:

```verilog
module clock_divider_10(
    input  wire clk,
    input  wire rst,
    output reg  clk_out
);

    integer counter = 0;

    always @(posedge clk or posedge rst) begin
        if (rst) begin
            counter <= 0;
            clk_out <= 0;
        end
        else begin
            if (counter == 4) begin   // DIVISOR/2 - 1 = 4
                clk_out <= ~clk_out;
                counter <= 0;
            end
            else begin
                counter <= counter + 1;
            end
        end
    end

endmodule
```
# Test Bench:
```verilog
`timescale 1ns/1ps

module tb_clock_divider_10;

    reg clk;
    reg rst;
    wire clk_out;

    // Instantiate DUT
    clock_divider_10 uut (
        .clk(clk),
        .rst(rst),
        .clk_out(clk_out)
    );

    // Generate input clock (100 MHz)
    always #5 clk = ~clk;

    initial begin
        // Initial states
        clk = 0;
        rst = 1;

        // Apply reset
        #20 rst = 0;

        // Run simulation
        #500;
        $stop;
    end

endmodule
```
# Simulation Output:

<img width="1920" height="1200" alt="Screenshot 2025-11-16 192729" src="https://github.com/user-attachments/assets/7666c754-3c82-4173-a1e8-27d9163f122d" />

---
# Conclusion:
A functional divide-by-10 clock divider was designed using Verilog HDL and verified using simulation. This project demonstrates digital clock control, counter-based frequency division, and the importance of testbenches for verification.
