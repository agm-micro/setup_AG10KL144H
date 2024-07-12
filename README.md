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
  end
  else begin
    LED <= 4'b1100;
  end
end
endmodule 
  ```
Do compilation and assign clock, reset and LED pins. By now, all the above steps are just standard Altera Cyclone-4 development flow.

## 2, Create a Supra project:
  Open Supra, File -> New project
  
## 2, Migrate to Supra project from Quartus project:
  Open Supra, Tools -> Migrate,
  Select device `AG10KL144H`, click `Next`,
  On this step, `af-quartus.tcl` is now generated on your Supra project.
  ![image](https://github.com/user-attachments/assets/88d2d9c7-07bb-4366-a093-3a3ac9f14b69)
  Leave this step here, jump to Quartus and open the Quartus prject your created on `step1`.
  Quartus, Tools -> run Tcl Scripts, Add to Projects, load the `af_quartus.tcl` and run.
  Do compilation.

## 4, Convert project on Supra:
  Now go back to Supra's page shown in the image, click `Next` then `Finish`, 
  Supra will generate `prg` files:
  `xx_sram.prj` is for Blaster to load to RAM, `xx_master.prj` is for Blaster to load to flash.

## Synchronize new changes from Quartus to Supra.
  Everytime your Quartus project has been modified and finished the compilation sucessfully, use Supra -> Tools -> Compile.
  Click `Run`, it will synchronize the Quartus program to AGM `prj` firmware automatically.
  
  
