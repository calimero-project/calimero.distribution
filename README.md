Calimero Project
================

The Calimero Project provides a collection of libraries and tools for 
KNX network access and management.
The name Calimero origins from an inside joke: Calimero is not a falcon, referring to the Windows DCOM KNX Falcon driver library.

* Current development versions on Github: <https://github.com/calimero-project/>
* Distributions on SourceForge: <http://sourceforge.net/projects/calimero/>
* Calimero group identifier for artifacts in Maven: com.github.calimero


What's in the Egg
=================

1) The Calimero-core library, providing access protocols, network links, and higher-layer process communication and management APIs

2) Additional connection support for serial communication:

  * serialcom-jni.zip, an optional way of serial port access using the Java Native Interface (JNI)
  * calimero-rxtx jar archive, an optional way of serial port access using RXTX, or any compatible library

3) A collection of Calimero tools to access KNX networks from the terminal

4) The Calimero KNXnet/IP server, an extensible KNXnet/IP server implementation. The server does not have a client-side connection limit (like 1 or 4 connections with many other hardware) and can be run out-of-the-box, also supporting KNXnet/IP client access for other interfaces/protocols, e.g., TP-UART, USB, FT1.2.

5) The Calimero KNX device, a library to implement your own KNX device in Java

6) The Calimero GUI, a graphical user interface to access KNX networks, based on the Standard Widget Toolkit (SWT)

7) properties.xml contains the KNX property definitions, used with APIs that access KNX properties

8) XSLT stylesheets for converting ETS project files for use with Calimero


Hatch Calimero
==============

Extract the content of this archive into a directory of your choice.


Learn to Fly
============

Open a terminal and change to the directory with the extracted distribution files.
Ensure a Java interpreter is available by executing

	java 

on the terminal. The minimum required Java runtime environment is Java 8. The command

	java -jar calimero-core-2.4.jar

should print some information about the library. That information can also be queried directly in software through methods of the class `tuwien.auto.calimero.Settings`.

Note, that on Windows the separator for classpath entries (`-cp`) is `;`, Linux/MacOS uses `:`.
All of the Calimero tools offer a `--help` option, which prints a list of supported command line options.

To discover KNXnet/IP routers

	java -cp "calimero-core-2.4.jar;calimero-tools-2.4.jar" tuwien.auto.calimero.tools.Discover -s
	
or, relying on the information from the jar Manifest, one can also just type

	java -jar calimero-tools-2.4.jar discover

To print a list of all supported tool commands (similiar to `discover` that we've just used), simply type
	
	java -jar calimero-tools-2.4.jar


Asking for the KNXnet/IP self-description of a KNXnet/IP server using its IP address	

	java -jar calimero-tools-2.4.jar describe 192.168.10.12

To query the IP configuration of a KNXnet/IP server using its IP address

	java -jar calimero-tools-2.4.jar ipconfig 192.168.10.12

To busmonitor a KNX network using a KNXnet/IP server

	java -jar calimero-tools-2.4.jar monitor 192.168.10.10

And so on ...

### Graphical User Interface

Launch the graphical user interface using

	java -jar calimero-gui-2.2.jar

On MacOS, use
	
	java -XstartOnFirstThread -jar calimero-gui-2.2.jar

### KNXnet/IP server

To run the server out-of-the-box, start it in a terminal supplying the `server-config.xml` configuration file customized to your setup:

	java -cp "./*" tuwien.auto.calimero.server.Launcher server-config.xml 

 Make sure to adjust the configuration template `server-config.xml` to your setup!

### KNX Device
Calimero KNX device provides the network stack to run your own Java-based KNX device. An example of a 2-state push-button device over KNX IP is shown in the GitHub introduction repository ([PushButtonDevice.java](https://github.com/calimero-project/introduction/blob/master/src/main/java/PushButtonDevice.java)).

Network Interfaces with KNXnet/IP
---------------------------------
When using KNXnet/IP, make sure that your network interfaces are configured and firewalls do not block KNXnet/IP traffic. 
Take care when using IPv6 addresses, Network Address Translation (NAT), or multiple network interfaces. Each of those things might be a problematic factor if something does not work as expected.

* If you experience problems with IPv6, passing `-Djava.net.preferIPv4Stack=true` as VM argument helps. It does exactly what it says: prefer the IPv4 network stack over IPv6.
* Calimero KNXnet/IP allows you to specify the outgoing network interface, and the use of NAT-aware communication where necessary (see the corresponding command line options or JavaDoc).


FT1.2 and TP-UART Connections
-------------------------
The FT1.2 protocol and TP-UART require access to a serial port communication resource.
Calimero supports two ways of access to a serial port, with availability checked in the following order:
  
1. Calimero built-in support using JNI and the serialcom library. The C++ source code is provided for Windows and Unix/MacOS platforms. Compiled .dll libraries for Windows and .so for Linux are available (see the corresponding READMEs for system and compiler versions). The sources should compile on any compliant Windows 32/64 platform as well as common Linux platforms. The simplest way to ensure the Java runtime detects the serial library is to put it into the current working directory. The better way is to use the dedicated Java library lookup path, e.g., on Microsoft Windows, \<java-home\>\bin.
  
2. Use of RXTX (or any compatible) library, if such library is available and configured, i.e., accessible via the class path so the Java class loader finds it. The calimero-rxtx jar archive, being the Calimero adapter to access the RXTX library, has to be on the Java class path, too.

If any of the connection prerequisites is not met, i.e., you do not have a Java ME environment, you do not want to use additional native (JNI) code, or you do not have a RXTX library, that way of accessing the serial port is skipped by Calimero. 
In other words, you have to ensure at least one way of connection support for serial communication.



Have fun exploring and using Calimero!
