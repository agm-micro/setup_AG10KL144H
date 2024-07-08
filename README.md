# AG10KL144H FPGA project setup wizard

## 1, Setup Quartus II
  We recommend to use Quartus II 18.0 Prime Standard for the project.
  
  https://www.intel.com/content/www/us/en/software-kit/667160/intel-quartus-prime-standard-edition-design-software-version-18-0-for-windows.html

## 2, Create / User a Quartus project:
  Create a new project with device `EP4CE10E22C8`, 
  Use entry file
  ```
  module top(
	input clk,
	input resetn,
	output reg [3:0] LED
);
initial begin
	LED = 4'b0000;
end


always @ (posedge clk or negedge resetn) begin
  if (!resetn) begin
    LED <= 4'b0011;
  end begin
    LED <= 4'b1100;
  end
end
endmodule 
  ```
Assign Clock, Reset and LED pins.

## 2, Create / User a Supra project:
  You will see `af_quartus.tcl` file included in the project.
  
## 3, Add tcl script to Quartus project:
  Quartus, Tools -> run Tcl Scripts, Add to porjects, load the `af_quartus.tcl` and run.
  Compilation the project

## 4, Migrate Quartus project on Supra:
  Open the Supra project you created on step 2.
  Clock Tools -> Migrate, choose migrate from directory as Quartus project folder
  Select device `AG10KL144H`, click Next, Next then Finish, wait to finish.

  Supra will generate prg files:
  xx_sram.prj is for Blaster to load to RAM, xx_master.prj is for Blaster to load to flash.

  Tool -> Download to load the program to AGM FPGA.
  
  
