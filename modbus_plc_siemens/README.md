# PLC Modbus
=========
## Example Codes (Python)
Refer to `modbus_client_s7_1200.py` in package <strong> modbus_plc_simens </strong>

### Brief
This pacakge is a bridge between a python modbus client and a Siemens PLC as modbus server.
This package includes:
* A project test to load in TIA Portal
* A ROS node to interface a Siemens PLC with a ROS environmen

To be completely tested this package needs a Siemens PLC S7-1200 configured with Siemens TIA Portal

### Quickstart
Download the TIA Portal project (in modbus_wrapper/modbus_plc_siemens/resources/[TIA_PORTAL] S7_1200_Modbus_wrapper) to your siemens PLC to enable the modbus server on the PLC.

Make sure you are able to ping the PLC from the workstation, where you execute your ROS node.

Start a modbus client that connects to a modbus server on PLC, running the programm of the resources directory.
Replace the ip address with the address from your PLC. Try first if you are able to ping it.

```
$ rosrun modbus_plc_siemens modbus_client_s7_1200.py _ip:="192.168.1.1(depend on used PLC address)" _port:=502
```

### Output
You should be able to see:
* The first 4 LED flash one by one (test write value to single register)
* Print out the data received from PLC registers if any (test receive values from defined reading register)  
* All the LED flash periodically (test send values to defined writing register)
 