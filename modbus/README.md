# PLC Modbus
=========
## Brief
Cient: Creates a Python modbus TCP client and uses the topic and Python interface to communicate with plc server
Server(PLC) <---> Client(PC)
* Subscriber: modbus_wrapper/output (std_msgs/Int32MultiArray) 
  //Corresponds to the outputs of your PLC. Set a non zero value to activate an output. 
* Publisher: modbus_wrapper/input (std_msgs/Int32MultiArray) 
  //Corresponds to the inputs of the PLC. 

Server: Creates a Python modbus TCP server and communicates with plc client
Server(PC) <---> Client(PLC)
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

Get values of the read registers of the PLC server use a <strong> subscriber </strong> on the topic: 
* /modbus_wrapper/input

Send something to the PLC server use a <strong> publisher </strong> on the topic 
* /modbus_wrapper/output

Get values of the read registers of the PLC client use a <strong> subscriber </strong> on the topic: 
* /modbus_server/read_from_registers

Send something to the PLC client use a <strong> publisher </strong> on the topic 
* /modbus_server/write_to_registers

For more detail, please read APIs in <strong> package modbus </strong> `modbus_wrapper_client.py` and `modbus_wrapper_server.py`

### Quickstart
Start a modbus server or use an existing one. Replace the port with user-defined value (502 by default)
```
$ rosrun modbus_wrapper modbus_server.py _port:=502
```

Start the corresponding modbus client on the same or another computer. If started on another computer, replace the IP and port with the modbus server's values
```
$ rosrun modbus_wrapper modbus_client.py _ip:="localhost" _port:=502
```