Research Notes - August 8, 2015
------------------------------------
## *Summary*

Working on 1 main project today:

- [RA2/b](#RA2b) 
- [pheno paper](#DissectingJetsMET)
- [HF commissioning](#HFcommissioning)

<a name="RA2b">
## *RA2/b* 

To do list :

1. Make patch for whatever went wrong with the L2L3 residuals
2. Make new plots for the DPS ([notes](#ra2b-item2))
	+ update inputFiles in playingWithData repo
	+ compute weights
	+ compute lumis
3. update plots by Monday morning for the DPS
4. Edit RA2/b section of the DPS note... I think its in rough shape

###Notes:
<a name="ra2b-item1">
####item 1
<a name="ra2b-item2">
####item 2

working directory is here:
<pre>/uscms_data/d2/awhitbe1/workArea/RA2studies/commission2015/CMSSW_7_4_6_patch1/src/AWhitbeck/SuSySubstructure/test/playingWithData</pre>

Setting up inputFiles.py to load all of the spring15 MC and the latest data trees.  I am trying to test this, but for some reason I just get zero entries for everything.

<table>
<tr> 
<td> sample </td> <td> events analyzed </td> <td> x-sec [pb] </td> <td>weight [/fb^-1]</td>
</tr>
<tr> 
<td> Gjets400 </td><td>2068061</td><td>273</td><td id="Gjets400weight"></td>
</tr>
<td> Gjets600 </td><td>2492376</td><td>94.5</td><td id="Gjets600weight"></td>
</tr>

<tr> 
<td> </td><td> </td><td> </td><td> </td>
</tr>

</table>

<script src="http://code.jquery.com/jquery-1.4.2.min.js">

var Gjets400xsec=273.
var Gjets400eventsAnalyzed=2068061.
document.getElementById("Gjets400weight").innerHTML = 1000.*Gjets400xsec/Gjets400eventsAnalyzed
</script>
<a name="DissectingJetsMET">
## *Dissecting jets+MET* 

To do list :

1. Finish writing up a section in the paper on the variables and their distributions

2. Make 2D plots 

<a name="HFcommissioning">
## *HF frontend commissioning* 

To do list:

1. Thinks about availability of hardware for installing a crate into UXC
2. Verify that triggered readout works with the RCMS configuration files
	+ need to make sure that crate 50 gets added to the run configuration so that the DAQ is automatically configured
	+ figure out how to analyze the data 
	+ test ICI functionality
3. Test ngRBXmanager at 904
4. Get LV power software running at 904 for HF crates
	+ figure out where the ngCCMs are and get UMD guys to test them (and the backplanes maybe)
5. Figure out database issues for ePortage


> Written with [StackEdit](https://stackedit.io/).