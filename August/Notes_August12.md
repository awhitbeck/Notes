
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

<div>
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
</div>

notes from other trials...
-- For some reason this didn't work the although it has in the past.  I am not sure why though. Probably something in my proxy settings -- Indeed when I set the proxy port to 2013 and logged into cms904usr with -D 2013, everything worked -- Now the usual hyperdaq links are not there ... 

I am not sure why this is, but I was also have trouble connecting to the server.  It took a while for the peer-to-peer thing to initialize.  I am wondering if it just takes a while for everything to connect... indeed it took like 10 minutes for everything to start behaving. 

<a name="DissectingJetsMET">
## *Dissecting jets+MET* 

To do list :

1. Finish writing up a section in the paper on the variables and their distributions

2. Make 2D plots 

> Written with [StackEdit](https://stackedit.io/).