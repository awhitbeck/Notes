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
<td> Gjets400 </td><td>2068061</td><td>273</td><td>0.132</td>
</tr>
<td> Gjets600 </td><td>2492376</td><td>94.5</td><td>0.0379</td>
</tr>
<tr>
<td> Zinv400 </td><td>935221</td><td>10.944</td><td>0.0117</td>
</tr>
<tr>
<td> DY400 </td><td>908937</td><td>6.761</td><td>0.00744</td>
</tr>
<tr>
<td> DY600 </td><td>3353595</td><td>471100</td><td>0.00335</td>
</tr>
<tr>
<td> QCDpt80 </td><td>3325105</td><td>2762530</td><td>830.8</td>
</tr>
<tr>
<td> QCDpt120 </td><td>3353595</td><td>471100</td><td>140.5</td>
</tr>
<tr>
<td> QCDpt170 </td><td>3364368</td><td>117276</td><td>34.9</td>
</tr>
<tr>
<td> QCDpt300 </td><td>2893108</td><td>7823</td><td>2.70</td>
</tr>
<tr>
<td> QCDpt470 </td><td>1936832</td><td>648.2</td><td>0.335</td>
</tr>
<tr>
<td> QCDpt600 </td><td>1865328</td><td>186.9</td><td>0.100</td>
</tr>
<tr>
<td> QCDpt800 </td><td>1858448</td><td>32.293</td><td>0.0174</td>
</tr>
<tr>
<td> QCDpt1000 </td><td>1482720</td><td>9.4183</td><td>0.00635</td>
</tr>
<tr>
<td> QCDpt1400 </td><td>195447</td><td>0.84265</td><td>0.00431</td>
</tr>
<tr>
<td> QCDpt1800 </td><td>193608</td><td>0.114943</td><td>0.000594</td>
</tr>
<tr>
<td> QCDpt2400 </td><td>194456</td><td>0.00682981</td><td>3.51e-5</td>
</tr>
<tr>
<td> QCDpt3200 </td><td>187184</td><td>0.000165445</td><td>8.84e-7</td>
</tr>
<tr>
<td> TTJets </td><td>11023664</td><td>815.96</td><td>0.0740</td>
</tr>
<tr>
<td> WJets400 </td><td>1828496</td><td>59.5</td><td>0.0325</td>
</tr>
<tr>
<td> WJets600 </td><td>1025364</td><td>22.8</td><td>0.0222</td>
</tr>

</table>

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