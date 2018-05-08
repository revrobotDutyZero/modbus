# PLC Modbus
=========
## Overview
The modbus stack provides a wrapper from the modbus communication to standardized ROS messages. The modbus package is based on pymodbus and is also written in Python.

After a catkin_make the Python modbus classes are also available from the outside and can be easily integrated in other packages.

This stack was tested by interfacing with a Siemens PLC

* The package `modbus` is the basic python wrapper for <strong> modbus server and client for ROS </strong>
* The package `modbus_plc_siemens` inherits the modbus client base class and changes the register size.

Install all dependencies from packages or from sources:
	* sudo apt-get install python-pymodbus
	* sudo apt-get install python-pyasn1 python-twisted-conch