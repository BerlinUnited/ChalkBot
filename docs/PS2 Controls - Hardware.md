# PS2 controls through Arduino - Hardware Side
Below is a detailed documentation of the hardware components used to enable PS2 controls of the ChalkBot. 

This information is subject to change, for example, Arduino Mega will eventually replaced by the lighter Arduino Nano, etc.

# The controller

![PS2 Controller](https://m.media-amazon.com/images/I/61X1rlukjdL._AC_SL1200_.jpg)

This project uses Blue Lake Performance Wireless PS2 Controller. The receiver component can connect to the target device through USB or classic PS2 pins.

## Controller connection to Arduino Mega
Jumper wires have been used to connect the pins on PS2 receiver to the Arduino Mega:

![Arduino Mapping](https://hackster.imgix.net/uploads/attachments/890339/untitled-2_CM3WtxTySI.jpg?auto=compress,format&w=1280&h=960&fit=max)

 The receiver is fully powered through Arduino Mega through the corresponding pin, but this will not be possible in the later stages of the project, since Arduino Nano is unable to power up the receiver.

Below is a visual breakdown of the receiver pins for the PS2 controller:

![PS2 Pins](https://hackster.imgix.net/uploads/attachments/890338/ps2_controller-2_zdnilnV0Ci.jpg?auto=compress,format&w=1280&h=960&fit=max)

## Arduino Mega connection to PC

Arduino Mega is connected to the PC through the USB port, which serves to power it up, as well as enable the serial input received by the Arduino to be read on the PC.


