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

2) Additional connection support for the FT1.2 protocol (serial communications)

  * serialcom-jni.zip, an optional way of serial port access using the Java Native Interface (JNI)
  * calimero-rxtx jar archive, an optional way of serial port access using RXTX, or any compatible library

3) A collection of Calimero tools to access KNX networks from the terminal

4) The Calimero KNXnet/IP server, an extensible KNXnet/IP server implementation, having no client-side connection limit (like 1 or 4 connections with some hardware). The server can be run out-of-the-box and also supports KNXnet/IP client access for other interfaces, e.g., an FT1.2 interface.

5) Calimero KNX device, a library to easily implement your own KNX device in Java

6) properties.xml contains the KNX property definitions, used with APIs that access KNX properties

7) A graphical user interface to access KNX networks, based on the Standard Widget Toolkit (SWT) as used by the Eclipse IDE

8) XSLT stylesheets for converting ETS 4 project files for use with Calimero


Hatch Calimero
==============

Extract the content of this archive into a directory of your choice.


Learn to Fly
============

Additional documentation is also available via

* a quick guide with examples at https://calimero-project.github.io/
* the README.md files (Markdown formatted) in the various `*-sources.jar` files

Open a terminal and change to the directory with the extracted distribution files.
Ensure a Java interpreter is available by executing

	java 

on the terminal. The minimum required JRE is Java ME CDC Foundation Profile based on Java version 1.4 (note, that future Calimero releases will require Java 8).
The command

	java -jar calimero-core-x.jar

should print some information about the library. That information can also be queried directly in software through methods of the class `tuwien.auto.calimero.Settings`.

In the following examples we use the Calimero tools, replace _x_ with your Calimero version. Note, that on Windows the separator for class path entries (`-cp`) is `;`, on Linux/OSX `:` is used.
All of the Calimero tools offer a `-help` option, which prints a list of supported command line options.

To discover KNXnet/IP routers

	java -cp "calimero-core-x.jar;calimero-tools-x.jar" tuwien.auto.calimero.tools.Discover -s
	
or, relying on the information from the jar Manifest, one can also just type

	java -jar calimero-tools-x.jar discover

To print a list of all supported tool commands (similiar to `discover` that we've just used), simply type
	
	java -jar calimero-tools-x.jar


Asking for the KNXnet/IP self-description of the server using its IP address	

	java -jar calimero-tools-x.jar describe 192.168.10.12

To query the IP configuration of a KNXnet/IP server using its IP address

	java -jar calimero-tools-x.jar ipconfig 192.168.10.12

To busmonitor a KNX network using a KNXnet/IP server

	java -jar calimero-tools-x.jar monitor 192.168.10.10

And so on ...

### KNXnet/IP server

To run the server out-of-the-box, start it in a terminal supplying the `server-config.xml` configuration file customized to your setup. For details, refer to the corresponding server README and the configuration template `server-config.xml`.

### KNX Device
Calimero KNX device provides the network stack to run your own Java-based KNX device. An example of a 2-state push-button actuator over KNX IP is shown in the GitHub introduction repository ([PushButtonActuator.java](https://github.com/calimero-project/introduction/blob/master/examples/java8/PushButtonActuator.java)).

Network Interfaces (KNXnet/IP)
------------------------------
When using KNXnet/IP, make sure that your network interfaces are configured and firewalls do not block KNXnet/IP traffic. 
Take care when using IPv6 addresses, Network Address Translation (NAT), or multiple network interfaces. Each of those things might be a problematic factor if something does not work as expected.

* If you experience problems with IPv6, passing `-Djava.net.preferIPv4Stack=true` as VM argument helps. It does exactly what it says: prefer the IPv4 network stack over IPv6.
* Calimero KNXnet/IP allows you to specify the outgoing network interface, and use NAT-aware communication where necessary (see the corresponding command line options or JavaDoc).


FT1.2 Connection Protocol
-------------------------
The FT1.2 protocol requires access to a serial port communication resource.
Therefore, to use a FT1.2 connection, Calimero supports three ways of access to a serial port, with availability checked in the following order:

1. Java ME (Micro-Edition) CDC serial connection. This connection type will not be available at all on "bigger" environments like Java SE. Even on a ME CDC platform, a serial connection implementation might not be provided.
  
2. Calimero built-in support using JNI and the serialcom library. The C++ source code is provided for Windows and Unix / OS X platforms. Compiled .dll libraries for Windows and .so for Linux are available (see the corresponding READMEs for system and compiler versions). The sources should compile on any compliant Windows 32/64 platform as well as common Linux platforms. The simplest way to ensure the Java runtime detects the serial library is to put it into the current working directory. The better way is to use the dedicated Java library lookup path, e.g., on Microsoft Windows, \<java-home\>\bin.
  
3. Use of RXTX (or any compatible) library, if such library is available and configured, i.e., accessible via the class path so the Java class loader finds it. The calimero-rxtx jar archive, being the Calimero adapter to access the RXTX library, has to be on the Java class path, too.

If any of the connection prerequisites is not met, i.e., you do not have a Java ME environment, you do not want to use additional native (JNI) code, or you do not have a RXTX library, that way of accessing the serial port is skipped by Calimero, *without* any other limitation of functionality. 
In other words, to use FT1.2, you have to ensure at least one way of connection support for serial communication.

Note: The former Sun extension libraries for Java SE to access serial ports are *not* checked.




Have fun exploring and using Calimero!
