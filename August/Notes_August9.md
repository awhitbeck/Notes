Research Notes - August 9, 2015
------------------------------------
## *Summary*

Working on 1 main project today:

- [RA2/b](#RA2b) 

largely trying to reproduce my plots showing the CR region distributions and the Zgamma ratios.  I spent a lot of time trying to organize all of my scripts so that they would easily run.  In the end it worked pretty well except this strange issue I had with condor and my inputFiles.py code, see [here](#condorInputFilesIssue).  In the end, I found a work around, but it requires more manual work.

<a name="RA2b">
## *RA2/b* 

To do list :

1. Make patch for whatever went wrong with the L2L3 residuals
2. ~~Make new plots for the DPS~~ ([notes](#ra2b-item2))
	+ ~~update inputFiles in playingWithData repo~~
	+ ~~compute weights~~
	+ ~~compute lumis~~
3. ~~update plots by Monday morning for the DPS~~
	+ ~~review scripts to make sure that nothing should have changed~~
	+ ~~submit jobs for all backgrounds~~
4. Edit RA2/b section of the DPS note
	+ put new plots from commissioning [twiki](https://twiki.cern.ch/twiki/bin/view/CMS/RA2b13TeVCommissioning) into note


###Notes:
<a name="ra2b-item1">
####item 1
<a name="ra2b-item2">
####item 2

working directory is here:
<pre>/uscms_data/d2/awhitbe1/workArea/RA2studies/commission2015/CMSSW_7_4_6_patch1/src/AWhitbeck/SuSySubstructure/test/playingWithData</pre>

Setting up inputFiles.py to load all of the spring15 MC and the latest data trees.  I am trying to test this, but for some reason I just get zero entries for everything.  This fixed itself once I renewed my voms certificate.  Below is an attempt to calculate the weights, however, there seems to be a huge inefficiency in the job success...

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
<td> Zinv600 </td><td>1014139</td><td>4.203</td><td>0.00414</td>
</tr>
<tr>
<td> DY400 </td><td>908937</td><td>6.761</td><td>0.00744</td>
</tr>
<tr>
<td> DY600 </td><td>811006</td><td>2.718</td><td>0.00335</td>
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

As a sanity check, this plot shows that the MC weights seems to be fine:

<<<<  add plot >>>> 

The lumi calculation showed that al of the PDs were 35/pb, but this only included the prompt files.  I edited the script to loop over both the July 17th reprocessing and the prompt files.  Now the integrated luminosities are all consistent with what the json file quotes:

<table>
<tr>
<td>Primary dataset</td><td>Integrated luminosity delivered [/pb]</td><td>Integrated luminosity recorded [/pb]</td>
</tr>
<tr>
<td>DoubleEG</td><td>41.024</td><td>40.028</td>
</tr>
<tr>
<td>DoubleMuon</td><td>40.992</td><td>40.002</td>
</tr>
<tr>
<td>HTMHT</td><td>40.999</td><td>40.003</td>
</tr>
<tr>
<td>SingleElectron</td><td>40.989</td><td>40.021</td>
</tr>
<tr>
<td>SingleMuon</td><td>40.999</td><td>40.003</td>
</tr>
<tr>
<td>SinglePhoton</td><td>41.024</td><td>40.028</td>
</tr>
</table>

I submitted jobs to reproduce the DY-CR plots, γ-CR plots, and the photon N-1 plots.  the relevant code is here:

https://github.com/awhitbeck/playingWithData/blob/master/plotDrellYanCRkinematics_batch.py
https://github.com/awhitbeck/playingWithData/blob/master/plotPhotonCRkinematics_batch.py
https://github.com/awhitbeck/playingWithData/blob/master/plotNminusOnePhoton_batch.py

script to submit jobs:

https://github.com/awhitbeck/playingWithData/blob/master/submitPhotonCRjobs.py
https://github.com/awhitbeck/playingWithData/blob/master/submitNminusOnePhotonJobs.py
https://github.com/awhitbeck/playingWithData/blob/master/submitDrellYanCRjobs.py

Plots are very strange.  I am still applying the same MHT cuts and I find that the MC yield goes up, even though the integrated luminosity went down, and the data yield goes down.  Maybe there were conspiring problems that just gave good agreement :(

Okay, I am trying to better understand what changed.  Fortunately, I can reproduce the MHT and HT calculation to within numerical precision:
<pre>PreSelection->Scan("HT:Sum$(ak4Jets.Pt()*(abs(ak4Jets.Eta())<2.5)*(ak4Jets.Pt()>30.)):MHT:sqrt(Sum$(ak4Jets.Px()*(abs(ak4Jets.Eta())<3.0)*(ak4Jets.Pt()>30.))*Sum$(ak4Jets.Px()*(abs(ak4Jets.Eta())<3.0)*(ak4Jets.Pt()>30.))+Sum$(ak4Jets.Py()*(abs(ak4Jets.Eta())<3.0)*(ak4Jets.Pt()>30.))*Sum$(ak4Jets.Py()*(abs(ak4Jets.Eta())<3.0)*(ak4Jets.Pt()>30.))):ak4Jets.Pt():ak4Jets.Eta():abs(ak4Jets.Eta())")</pre>

Similarly, I can directly compare MHT5.0 to MHT3.0.  The scatter plot for GJets events shows that there is very very high correlation between these two variables.  Basically, there are very few events which have pT>30. GeV jet in the HF.  Okay, now I see that there wasn't really any wrong with the tree themselves, as far as I can tell.  However, I was not analyzing all of the data due to a mistake in my submission scripts.  

<a name="condorInputFilesIssue">
While try to run over both the prompt and reprocessed data, I ran into a very strange problem with my jobs.  If I added the 17Jul2015 files to inputFiles.py, **none** of my sampleInfo objects would be able to find the target files in eos!!! I have no idea why this would be.  After several hours of trying to debug this, I simply changed to way the tchains are loaded -- I now pass a .txt file to the work nodes that has all of the file names and just use that instead of ls'ing the target directory on eos.  This work around is a very poor substitute for the way things used to work!

Now, I was able to make decent data MC comparisons, although they still don't look nearly as good as the last version:

[Drell-Yan CR](http://whitbeck.web.cern.ch/whitbeck/RA2b/Run2015B/FinalProductionDPS/?match=drellYanCR)

[γ CR](http://whitbeck.web.cern.ch/whitbeck/RA2b/Run2015B/FinalProductionDPS/?match=photonCR)

[R Z/γ](http://whitbeck.web.cern.ch/whitbeck/RA2b/Run2015B/FinalProductionDPS/?match=Zgamma)

**NOTE:** I just realized that I don't think the Drell-Yan CR plots have a trigger applied.  I am not sure what this implies.   I think for the high-pt events that I am interested in, there will be no bias from the trigger turn-on in data. 



> Written with [StackEdit](https://stackedit.io/).