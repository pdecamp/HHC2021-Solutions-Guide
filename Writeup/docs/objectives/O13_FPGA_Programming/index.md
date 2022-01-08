# Objective 13) FPGA Programming

!!! summary "*Difficulty*: :fontawesome-solid-tree:{: style="color: red;"}:fontawesome-solid-tree:{: style="color: red;"}:fontawesome-solid-tree:{: style="color: red;"}:fontawesome-solid-tree:{: style="color: red;"}:fontawesome-solid-tree:{: style="color: grey;"}"
    Write your first FPGA program to make a doll sing. You might get some suggestions from Grody Goiterson, near Jack's elevator.

!!! note
    This objective unlocks after reaching the roof of Frost Tower


## Hints and Resources

??? hint "Hints provided after helping Grody Goiterson and completing the <a href="../../challenges/T13_Frostavator">Frostavator</a> Terminal Challenge"
    **FPGA for Fun**<br>
    There are <a href="https://www.fpga4fun.com/MusicBox.html">FPGA enthusiast sites</a>.<br>
    <br>
    **FPGA Talk**<br>
    Prof. Qwerty Petabyte is giving <a href="https://www.youtube.com/watch?v=GFdG1PJ4QjA">a lesson</a> about Field Programmable Gate Arrays (FPGAs).<br>


??? hint "Other Resources"
    **Introduction Hint for Rounding Numbers**<br>
    If $rtoi(real_no * 10) - ($rtoi(real_no) * 10) > 4, add 1<br>


## Solution

Open the FPGA Programming terminal on the roof of Frost Tower and program it so all tests pass and you are able to program the device.

### The Code

There may be a more elegant way to do this but the following code will, at least in every test I ran, result in exact matches for any target frequency and will successfully complete the challenge.  See below for an explanation of the math.

``` java linenums="1"
// Note: For this lab, we will be working with QRP Corporation's CQC-11 FPGA.
// The CQC-11 operates with a 125MHz clock.
// Your design for a tone generator must support the following 
// inputs/outputs:
// (NOTE: DO NOT CHANGE THE NAMES. OUR AUTOMATED GRADING TOOL
// REQUIRES THE USE OF THESE NAMES!)
// input clk - this will be connected to the 125MHz system clock
// input rst - this will be connected to the system board's reset bus
// input freq - a 32 bit integer indicating the required frequency
//              (0 - 9999.99Hz) formatted as follows:
//              32'hf1206 or 32'd987654 = 9876.54Hz
// output wave_out - a square wave output of the desired frequency
// you can create whatever other variables you need, but remember
// to initialize them to something!

`timescale 1ns/1ns
module tone_generator (
    input clk,
    input rst,
    input [31:0] freq,
    output wave_out
);
    // ---- DO NOT CHANGE THE CODE ABOVE THIS LINE ---- 
    // ---- IT IS NECESSARY FOR AUTOMATED ANALYSIS ----
    // TODO: Add your code below. 

    reg [31:0] counter;
    real counter_target;
    reg wo;
    assign wave_out = wo;
    
    always @(posedge clk or posedge rst)
    begin

        // To set the valude of counter_target correctly we need to first determine if the
        // computed value needs to be rounded up by one.
        // Note that the numeric constants must be represented as decimal numbers
        // otherwise integer math will be used and no 'rounding up' will occur.

        if ($rtoi(((125000000.0 / freq) * 50.0) * 10) - ($rtoi((125000000.0 / freq) * 50.0) * 10) > 4)
            begin
                counter_target <= ((125000000.0 / freq) * 50.0) + 1;
            end
        else
            begin
                counter_target <= (125000000.0 / freq) * 50.0;
            end

        // Now that counter_target is set, we can start counting clock ticks waiting
        // for our next transition

        if (rst==1)
            begin
                counter <=0;
            end
        else
            begin
                if (counter >= counter_target)
                    begin 

                        // Each time the square wave tranistions we reset the counter to 2 (not 1).
                        // This is because (I think) we are already executing the first tick of the cycle.
                    
                        counter <= 2;
                        wo <= wo ^ 1;
                    end
                else
                    counter <= counter + 1;
            end
    end
endmodule
```

### The Frequency Math

Our clock is running at 125MHz, so 125,000,000 clock ticks = 1 second

The number of clock ticks that pass during each cycle of a given frequency (say for example, 500Hz) is equal to 125,000,000 divided by that number.<br>
`(125,000,000 / 500) = 250,000`

But a square wave cycle represents both the high and low portions of the wave, so the number of clock ticks between each transition is half that.<br>
`((125,000,000 / 500) / 2) = 125,000`

The target frequency supplied to our code is an integer value with the last 2 digits representing the fractional portion.  So a frequency of 500Hz will be seen by the code as the number 50000, so we have to multiply the previous result by 100.<br>
`(((125,000,000 / 50000) / 2) * 100) = 125,000`

Simplifying our final calculation gives us the following formula for how many clock ticks pass before each high / low transition.<br>
`((125,000,000 / freq) * 50)`


## Completion

!!! success "Answer"
    Successfully programming the device from the FPGA terminal completes the challenge and gives you the FPGA item, which can be plugged into the Speak and Spell next to Crunchy

