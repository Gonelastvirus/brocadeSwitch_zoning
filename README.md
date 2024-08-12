# brocadeSwitch_zoning
 As an example let’s assume the following values,<br><br>
Switch Port 1 – HBA1 - 10:00:ff:05:1e:4b:d5:30 <br><br>
Switch Port 2 – HBA2 - 10:00:ff:05:80:00:48:a5 <br><br>
Switch Port 12 - Storage Array port1 - 50:01:10:80:00:ad:33:e8<br><br>
Switch Port 13 - Storage Array port2 - 50:02:10:80:00:ac:f5:54<br><br>
<P><b>In the next step we are going to zone HBA1 with Storage Array port 1 and HBA2 with Storage Array port2.</b></P>
<br><br>
Step 1: Let’s assign an alias for each WWPN Following is the syntax,<br><br><br>
switch:admin> alicreate “HostPort1”, “10:00:ff:05:1e:4b:d5:30″<br><br>
switch:admin> alicreate “HostPort2”, “10:00:ff:05:80:00:48:a5″ <br><br>
switch:admin> alicreate “StoragePort1”, “50:01:10:80:00:ad:33:e8″<br><br>
switch:admin> alicreate “StoragePort2”, “50:02:10:80:00:ac:f5:54″ <br></P>
<p>To verify run command, 
alishow “HostPort1” and so on.<br><br>
Step 2: Now we are going to create two zones with two aliases in them (1 host port and 1 storage port)<br><br>
switch:admin> zonecreate “zone1”, “HostPort1; StoragePort1”<br><br>
switch:admin> zonecreate “zone2”, “HostPort2; StoragePort2”<br><br>
To verify run command, <br><br>
zoneshow “zone1” and so on.<br></p>
<p>
Step 3: Next step is to create a configuration which will hold the zones that we just created. The following command creates a configuration named “AppServer” and then adds both zones to it.<br>
switch:admin> cfgcreate "AppServer", "zone1;zone2"<br><br>
Final Step: Now that we have created a configuration we must enable it for it to act, following syntax enables AppServer configuration. At any given time there can be only one active configuration. But in switch database, there can be multiple.<br>
switch:admin> cfgenable "AppServer"<br><br>
Note: Names for Alias, Zones, Zone configuration is case-sensitive, it must begin with a letter and can be followed by any number of letters, numbers, and underscore characters.<br></p>
