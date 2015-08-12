Research Notes - August 11, 2015
------------------------------------
## *Summary*

Working on 3 main project today:

- [RA2/b](#RA2b) 
- [pheno paper](#DissectingJetsMET)
- [HF commissioning](#HFcommissioning)

<a name="RA2b">
## *RA2/b* 

To do list :

1. Make patch for whatever went wrong with the L2L3 residuals
2. Understand what is going on with the Drell-Yan control regions [notes](#DebuggingDYCR)

### Notes:

<a name="DubuggingDYCR">
#### item 2

Checked filters, there is nothing obviously wrong with them:

https://www.evernote.com/shard/s310/nl/44292113/fac599ff-58f5-4053-83ae-21b6e79f3c47/

However, there is a very strange effect related to the number of events seen in the 17Jul2015 dataset and the PromptReco dataset.  There are 10k events with a good Z cand. in the former and 20k in the latter!  This doesn't make sense because I think the Prompt REC is 35/pb.   Check the luminosities for the different datasets separately. 

**prompt reco lumis:**

json/lumiSummary_DoubleEG.json
nLS=1768 Integrated Lumi: delivered=  35.354 (/pb) recorded=  34.438 (/pb)

json/lumiSummary_DoubleMuon.json
nLS=1767 Integrated Lumi: delivered=  35.329 (/pb) recorded=  34.414 (/pb)

json/lumiSummary_HTMHT.json
nLS=1767 Integrated Lumi: delivered=  35.329 (/pb) recorded=  34.414 (/pb)

json/lumiSummary_SingleElectron.json
nLS=1767 Integrated Lumi: delivered=  35.333 (/pb) recorded=  34.435 (/pb)

json/lumiSummary_SingleMuon.json
nLS=1767 Integrated Lumi: delivered=  35.329 (/pb) recorded=  34.414 (/pb)

json/lumiSummary_SinglePhoton.json
nLS=1768 Integrated Lumi: delivered=  35.354 (/pb) recorded=  34.438 (/pb)

**17Jul2015 lumis:**

json/lumiSummary_DoubleEG.json
nLS=1851 Integrated Lumi: delivered=  19.005 (/pb) recorded=  18.747 (/pb)

json/lumiSummary_DoubleMuon.json
nLS=1850 Integrated Lumi: delivered=  18.998 (/pb) recorded=  18.747 (/pb)

json/lumiSummary_HTMHT.json
nLS=1851 Integrated Lumi: delivered=  19.005 (/pb) recorded=  18.747 (/pb)

json/lumiSummary_SingleElectron.json
nLS=1770 Integrated Lumi: delivered=  17.621 (/pb) recorded=  17.390 (/pb)

json/lumiSummary_SingleMuon.json
nLS=1851 Integrated Lumi: delivered=  19.005 (/pb) recorded=  18.747 (/pb)

json/lumiSummary_SinglePhoton.json
nLS=1851 Integrated Lumi: delivered=  19.005 (/pb) recorded=  18.747 (/pb)

**ugh!!!!!** I just realized that when I grabbed the latest run from DAS, it wasn't actually showing me the latest run :(  It was only showing me 10/15 runs. 

This means that there really is ~35+18/pb worth of data in the combined data set, so the data is ~30% high.  Updated table with last reprocessed run:

<table>
<tr> 
	<td> PD </td> <td> last run in reprocessed dataset </td>
</tr>
<tr>
	<td> DoubleEG </td> <td>251562 </td>
</tr>
<tr>
	<td> DoubleMuon </td> <td> 251562 </td>
</tr>
<tr>
	<td> EGamma </td> <td> 251250 </td>
</tr>
<tr>
	<td>HTMHT </td> <td> 251562 </td>
</tr>
<tr>
	<td>MET </td> <td> 251562 </td>
</tr>
<tr>
	<td> SingleElectron </td> <td> 251562 </td>
</tr>
<tr>
	<td> SingleMu </td> <td> 251160 </td>
</tr>
<tr>
	<td> SingleMuon </td> <td> 251562 </td>
</tr>
<tr>
	<td> SinglePhoton </td> <td> 251562 </td>
</tr>
</table>

After rerunning the prompt reco jobs, the data-MC agreement looks better.  Still the photon plots are off.  I have to check whether add QCD to this plot will fix things or not.  I also noticed that some of the datasets didn't have the 20/pb that I was expecting which is really strange because when there were overlaps, I found that the lumi was exactly what I expected for all PDs.  This needs to be investigated.  So, there still could be some data, MC disagreement in the drell-yan plots since I only saw 7-12/pb for the doubleEG and doulbe Muon datasets.

For the plotting scripts, I also added ttbar to the drell-yan histograms.  This dramatically improved the agreement.  

[see here](http://whitbeck.web.cern.ch/whitbeck/RA2b/Run2015B/FinalProductionDPS/?match=)

In general, I need to work on my scripts so that the are more maintainable and scalable.  Things are quite messy right now.  

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