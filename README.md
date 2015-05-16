Calimero Project
================

The Calimero Project provides a collection of libraries and tools for 
KNX network access and management.
The name Calimero origins from an inside joke: Calimero is not a falcon, referring to the Windows DCOM KNX Falcon driver library.

This distribution contains the Calimero project files, distinguished based on the name ending:

* "-bin" contains only the binaries and Java archives
* "-sources" contains the source code and configuration files
* "-doc" contains the JavaDoc documentation
* "-all" contains binaries, sources, and documentation

Distributions are available on SourceForge: http://sourceforge.net/projects/calimero/

The current development versions are hosted on Github: https://github.com/calimero-project/

Calimero is available as several Maven artifacts in the Maven repositories. The group identifier for the artifacts is "com.github.calimero".


What's in the Egg
=================

1) The Calimero-core library

2) A collection of Calimero tools to access KNX networks from the terminal

3) Additional connection logic for the FT1.2 protocol (serial communications)

  * serialcom-jni.zip, an optional way of serial port access using JNI
  * calimero-rxtx jar archive, an optional way of serial port access using the RXTX library

4) properties.xml contains the KNX property definitions, and is used with APIs that access KNX properties

5) A graphical user interface for the Calimero tools

6) XSLT stylesheets for converting ETS 4 project files to Calimero format


Hatch Calimero
==============

Extract the content of this archive into a directory of your choice.


Learn to Fly
============

A quick guide with examples is also available here: https://calimero-project.github.io/

Open a terminal and change to the directory with the extracted distribution files.
Ensure a Java interpreter is available by executing

	java 

on the terminal. The minimum required JRE is Java ME CDC Foundation Profile based on Java version 1.4.

In the following examples using the Calimero tools, replace _x_ with your Calimero version. The command

	java -jar calimero-core-x.jar

should print some information about the library. That information can also be queried directly in software through methods of the class `tuwien.auto.calimero.Settings`.

To discover KNXnet/IP routers

	java -cp "calimero-core-x.jar;calimero-tools-x.jar" tuwien.auto.calimero.tools.Discover -s
	
or, relying on the information from the jar Manifest

	java -jar calimero-tools-x.jar discover

Asking for the KNXnet/IP self-description of the server using its IP address	

	java -jar calimero-tools-x.jar describe 192.168.10.12

To query the IP configuration of a KNXnet/IP server using its IP address

	java -jar calimero-tools-x.jar ipconfig 192.168.10.12

Network Interfaces (KNXnet/IP)
------------------------------
When using KNXnet/IP, make sure that your network interfaces are configured and firewalls do not block KNXnet/IP traffic. 
Take care when using IPv6 addresses, Network Address Translation (NAT), or multiple network interfaces. Each of those things might be a problematic factor if something does not work as expected.


FT1.2 Connection Protocol
-------------------------
The FT1.2 protocol requires access to a serial port communication resource.
Therefore, to use the FT1.2. connection, Calimero supports 3 ways of access to a serial port, with availability checked by the library in the order listed:

 1) Java ME (Micro-Edition) CDC serial connection. This connection type will not be available on "bigger" environments like Java SE at all. Even on a ME CDC platform, a serial connection implementation might not be provided.

 2) Calimero built-in support using JNI and the serialcom library. The C++ source code is provided for Windows and Unix / OS X platforms. Compiled .dll libraries for Windows and .so for Linux are available (see the corresponding READMEs for system and compiler versions). The sources should compile on any compliant Windows 32/64 platform as well as common Linux platforms. The simplest way to ensure the Java runtime detects the serial library is to put it into the current working directory. The better way is to use the dedicated Java library lookup path, e.g. on Microsoft Windows, <java-home>\bin.

 3) Use of the RXTX library, if RXTX is available and configured (i.e., RXTX is on the class path, so the Java class loader finds it). The calimero-rxtx jar archive has to be on the Java class path, being the Calimero adapter to access the RXTX library.

If any of the connection prerequisites is not met, i.e., you do not have a Java ME environment, you do not want to use additional native (JNI) code, or you do not have a RXTX library, that way of connection will just not work (is skipped by Calimero), *without* any other limitation of functionality. 
To put it the other way round: to use FT1.2, you have to ensure at least one way of connection support for serial communication.

Note: The former Sun extension libraries for Java SE to access serial ports are *not* checked for in Calimero. Use RXTX instead.




Have fun exploring and using Calimero!
