# PLC Modbus
=========
## Brief
The modbus stack provides a wrapper from the modbus communication to standardized ROS messages. The modbus package is based on pymodbus and is also written in Python.

After a catkin_make the Python modbus classes are also available from the outside and can be easily integrated in other packages.

This stack was tested by interfacing with a Siemens PLC

* The package `modbus` is the basic python wrapper for <strong> modbus server and client for ROS </strong>
* The package `modbus_plc_siemens` inherits the modbus client base class and changes the register size.

Cient: Creates a Python modbus TCP client and runs several tests using the topic and Python interface. The modified client for the Siemens PLC and Insight camera use the same topics, but address different registers.
* Subscriber: modbus_wrapper/output (std_msgs/Int32MultiArray) 
  //Corresponds to the outputs of your PLC. Set a non zero value to activate an output. 
* Publisher: modbus_wrapper/input (std_msgs/Int32MultiArray) 
  //Corresponds to the inputs of the PLC. 

Server: Creates a Python modbus TCP server and runs several tests, if combined with the client. 
* Subscriber: modbus_server/read_from_registers (std_msgs/Int32MultiArray)
  //Corresponds to the readable modbus registers. 
* Publisher:  modbus_server/write_to_registers (std_msgs/Int32MultiArray)
  //Corresponds to the writeable modbus registers. 


## Functions
Define start register and number of registers that are going to read
* setReadingRegisters(self,start,num_registers)

Define start register and number of registers that are going to write
* setWritingRegisters(self,start,num_registers)

Directly write one register with specified value(If timeout is set, the register is set to 0 after this time)
* setOutput(address,value,timeout=0.0)

Get values of the read registers of the modbus use a subscriber on the topic: 
* rostopic echo /modbus_wrapper/input

Send something to the modbus use a publisher on the topic 
* /modbus_wrapper/output

For more detail, please read APIs in <strong> package modbus </strong> `modbus_wrapper_client` and `modbus_wrapper_server`


## Example Codes (Python)
Refer to `modbus_client_s7_1200.py` in package <strong> modbus_plc_simens </strong>

This pacakge is a bridge between a python modbus client and a Siemens PLC as modbus server.
This package includes:
* A project test to load in TIA Portal
* A ROS node to interface a Siemens PLC with a ROS environmen

To be completely tested this package needs a Siemens PLC S7-1200 configured with Siemens TIA Portal

### Quickstart
Download the TIA Portal project (in modbus_wrapper/modbus_plc_siemens/resources/[TIA_PORTAL] S7_1200_Modbus_wrapper) to your siemens PLC to enable the modbus server on the PLC.

Make sure you are able to ping the PLC from the workstation, where you execute your ROS node.

Start a modbus client that connects to a modbus server on PLC, running the programm of the resources directory. Replace the ip address with the address from your PLC. Try first if you are able to ping it.

```
$ rosrun modbus_plc_siemens modbus_client_s7_1200.py _ip:="192.168.1.1(depend on used PLC address)" _port:=502
```
