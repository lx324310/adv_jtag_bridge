#adv_jtag_bridge 
This is only the software of adv_jtag_bridge,the hardware of adv_jtag_bridge has include in SOC design,you can find in rtl dir.Here is some thing about adv_jtag_bridge install and use

#adv_jtag_bridge install 

1、preparing for install
  
  $sudo apt-get install -y pkg-config libusb-1.0-0-dev libtclcl1-dev libftdi-dev
  
2、Getting the Repo and config
  
  $cd ~/openrisc-tool
  
  $git clone https://github.com/lx324310/adv_jtag_bridge.git
  
  $cd adv_jtag_bridge
  
  $./autogen.sh
  
  $./configure
  
3、install 

  $make 
  
  $sudo make install
  
#adv_jtag_bridge use

1、generate jp-io-vpi.vpi or jp-io-vpi.so
simulator:iverilog
  
  $cd adv_jtag_bridge/sim_lib/icarus
  
  $make 
  
  $cp jp-io-vpi.so  /to soc path/bench/verilog/vpi
  
simulator:modelsim

  $cs adv_jtag_bridge/sim_lib/modelsim_linux_x86
  
  $vim Makefile     //change LINE8 Model=/modelsim install dir
  
  $make 
  
  $cp jp-io-vpi.so  /to soc path/bench/verilog/vpi
  
2、consume hardware build correctly when the soc system is run you can use the adv_jtag_bridge to connect with the soc 

  $adv_jtag_bridge <options> [cable] <cable options>
the options you can find in adv_jtag_bridge.pdf

Here is some example i have used 
1、sim
  
  $adv_jtag_bridge -x0 -l 0:4 -c 0x8 vpi
  
2、on xilinx ml501 board
  
  $adv_jtag_bridge -b ~/ml501_bsdl/ xpc_usb
  
3、on altare FPGA
  
  $adv_jtag_bridge -b /ep4c_bsdl/ ft245
then you will see JTAG connect in sim terminal

  


