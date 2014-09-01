Energy Measurement Library
==========================
The Energy Measurement Library provides a simple API to extract energy
consumption data from hardware power counters. It is designed to simplify energy
consumption experimentation by presenting a unified interface for different
kinds of hardware.

The following devices are currently supported:
	* Intel CPUs starting from Sandy Bridge
	(through the Running Average Power Limit interface)

	* Recent Nvidia Tesla and Quadro GPUs
	(through NVIDIA Management Library)

	* Intel Xeon Phi MICs
	(through the Intel Manycore Platform Software Stack (3.x+), from the host device)

EML automatically discovers necessary libraries and available devices at runtime.

Documentation
-------------
Doxygen-generated documentation can be found at:

https://hpc-ull.github.io/eml

License
-------
EML is released under the GPLv2 license.

Contact
-------
Universidad de La Laguna, High Performance Computing group <cap@pcg.ull.es>

http://cap.pcg.ull.es
