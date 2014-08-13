GENERAL
net-snmpd-lvs-module is a dynamicaly loadable shared object to get the
configuration and some statistical information from the Linux kernel
with IP virtual server support (also known as Linux Virtual Server).

INSTALLATION
From http://www.linuxvirtualserver.org/software/ipvs.html download the
the correct version of ipvsadm, for kernel 2.6 use ipvsadm-1.24 or later,
for kernel 2.4 use ipvsadm-1.21. Extract ipvsadm-<version>.tar.gz, build
the library and copy the subtree 'libipvs' into the directory where this
README-file resides.
Check that the Linux kernel is available under /usr/src/linux.
Install net-snmp and its development headers and libraries.
Invoke 'make', this should build 'lvs.so'.
Copy LVS-MIB.txt and OC.txt to /usr/share/snmp/mibs/ 
Check that the new MIB is visible by invoking 
shell> snmptranslate -m LVS-MIB -On -IR lvsServiceEntry,
this should return .1.3.6.1.4.1.8225.4711.18.1
Copy lvs.so to /usr/lib/libnetsnmplvs.so and add the following line to 
/etc/snmp/snmpd.conf:
---------------------------------------
dlmod lvs /usr/lib/libnetsnmplvs.so
---------------------------------------
Restart your snmpd.
Try if everything works invoking:
shell> snmpwalk -c public -v 2c -m LVS-MIB localhost 1.3.6.1.4.1.8225.4711
LVS-MIB::lvsVersion.0 = STRING: "1.2.0"
LVS-MIB::lvsNumServices.0 = INTEGER: 2
LVS-MIB::lvsHashTableSize.0 = INTEGER: 4096
LVS-MIB::lvsTcpTimeOut.0 = INTEGER: 900
LVS-MIB::lvsTcpFinTimeOut.0 = INTEGER: 120
LVS-MIB::lvsUdpTimeOut.0 = INTEGER: 300
LVS-MIB::lvsDaemonState.0 = INTEGER: none(0)
...

In case you want to add additional snmp-values to your MIB:
Set export MIBS=ALL and create skeleton with 
shell> mib2c -c mib2c.interate.conf lvsRealTable
or 
shell> mib2c -c mib2c.interate.conf lvsServiceTable
this should create a file lvsRealTable.c and/or lvsServiceTable.c.
Use the generated code as a template for lvs.c and populate the missing parts.

CREDITS
The code for this module is based on ucd-snmpd-lvs written by Romeo Benzoni in
2002 and never modified since. As that code did not compile with the newer
net-snmp headers, I decided to rewrite the complete code. The only unchanged
parts from the ucd-snmpd-lvs project are LVS-MIB.txt and OC.txt.

AUTHOR
Jacob Rief <jacob.rief@tiscover.com>
Jan, 2nd 2006

LICENSE
This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

