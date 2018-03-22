PLC modbus
=========
The modbus stack provides a wrapper from the modbus communication to standardized ROS messages. The modbus package is based on pymodbus and is also written in Python.

After a catkin_make the Python modbus classes are also available from the outside and can be easily integrated in other packages.

This stack was used in a quality inspection project with the Baxter robot interfacing with a Siemens PLC and a Cognex In-Sight camera. 

* The package modbus is the basic python wrapper for a modbus server and client for ROS
* The package modbus_plc_siemens inherits the modbus client base class and changes the register size.


## Functions
setReadingRegisters(self,start,num_registers)
setWritingRegisters(self,start,num_registers)

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


## Exampler Codes (Python)
Refer to `modbus_client_s7_1200.py` in package modbus_plc_simens
  $ rosrun modbus_wrapper modbus_client_s7_1200.py _ip:="192.168.1.1(depend on used PLC address)" _port:=502
