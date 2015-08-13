
Research Notes - August 12, 2015
------------------------------------
## *Summary*

Working on 1 main project today:

- [HF commissioning](#HFcommissioning)
- [pheno paper](#DissectingJetsMET)

<a name="HFcommissioning">
## *HF frontend commissioning* 

To do list:

1. Think about availability of hardware for installing a crate into UXC
2. ~~Verify that triggered readout works with the RCMS configuration files~~ [notes](#triggeredReadout)
	+ need to make sure that crate 50 gets added to the run configuration so that the DAQ is automatically configured
	+ figure out how to analyze the data 
	+ test ICI functionality
3. Test ngRBXmanager at 904
4. Get LV power software running at 904 for HF crates
	+ figure out where the ngCCMs are and get UMD guys to test them (and the backplanes maybe)
5. Figure out database issues for ePortage

### Notes:

<a name="triggeredReadout">
#### Item 2 - triggered readout

<hr>
**Starting a standalone xdaq session for HF test stand in 904**

Log into hcal904daq01 (Eplr4S|1v) with, i think, port forwarding: 
<pre>ssh -Y whitbeck@cms904usr -L 40010:localhost:40010
ssh -Y hcal904daq02 -L 40010:localhost:40010</pre>
Then go to src/12_4_6/src/12_4_6/hcal/hcalUpgrade/test/ and run standalone-setup.pl and run-standalone.sh.  This starts the xdaq server. 
In the perl setup up script be sure to give this connection file:
<pre>/nfshome0/whitbeck/src/12_4_6/src/12_4_6/hcal/hcalUpgrade/test/amc13_904_config.xml</pre>

The xdaq server can then be accessed by going to http://127.0.0.1:40010

If everything works - 

Click on the hcalSupervisor -> control panel -> setup -> start 
<hr>
**Instructions for using RCMS at 904**
Checking that these changes have taken effect in the RCMS gui.  To open the RCMS gui, one should first tunnel into the cms904 network:
<pre>ssh -Y whitbeck@cms904usr -D 2013</pre>

One should then point their Firefox browser to:

http://cms904rc-hcal.cms904:16000/rcms/gui

To enable this there are some settings that one might have to change.  Go to settings - preferences - advanced - network - settings…  Switch to manual proxy  configuration set the SOCKS Host to localHost and the port you chose when you set up the tunnel (in this case 2013).  Select 'SOCKS v5' and 'remote DNS’, and click okay.  The RCMS gui will prompt you for a username and password, this will be hcalpro for both.  

One can now browse the available configuration from the ‘Configuration Chooser’ page.  
First check that there are no current configurations being used by going to the 'Running Configurations’ page.  If nothing is attached you can then choose a configuration from the ‘Configuration Chooser’ page.  Once chosen, click ‘create’.  Click initialize.  If you got an error, log can be check by doing: 
<pre>ssh cms904rc-hcal
Handsaw.pl /var/log/rcms/hcalpro/Logs_hcalpro.xml|less -R</pre>
Then you can click start!
<hr>

notes from other trials...
-- For some reason this didn't work the although it has in the past.  I am not sure why though. Probably something in my proxy settings -- Indeed when I set the proxy port to 2013 and logged into cms904usr with -D 2013, everything worked -- Now the usual hyperdaq links are not there ... 

I am not sure why this is, but I was also have trouble connecting to the server.  It took a while for the peer-to-peer thing to initialize.  I am wondering if it just takes a while for everything to connect... indeed it took like 10 minutes for everything to start behaving. 

I was successfully able to setup and start a run using the run configuration that I created last week ( /hcalpro/904Int/VME_uTCA30_QIE10_CI) *and* start and stop a run with the standalone xdaq tools.  The run was successful and I was able to get an output file.  However, now I need to get help from Jay on how to analyze this data! I have copied the file to:
<pre>lxplus.cern.ch:workPublic/HTB_000101.root</pre>

<hr>

**ngRBXmanager Setup**

do not source the hcal_teststand_scripts!!  

<pre>/nfshome0/whitbeck/hcalngRBX/test</pre>
* start a xdaq application to run the ngRBXmanager:
<pre>bash run-test.sh</pre>
* Go to this webpage (either with a tunnel or directly from cms904usr):
http://hcal904daq01.cms904:40010/
* Go to HCal Supervisor and initialize
* Go to ngRBXmanager hyperdaq page

-- to check that the configuration

working with Seth today, we found that there were two main problems:

* there were two supervisors being configured 
* there were two applications that had the same ID

Now everthying works!  I was successfully able to take a run in the usual way.  

> Written with [StackEdit](https://stackedit.io/).