Research Notes - August 8, 2015
------------------------------------

## *RA2/b*

To do list :

1. ~~make configuration files that have the rereco data and non-overlapping prompt data~~ [notes](#RA2/b-item1)
2. ~~track new .db file if the residual corrections become available in both repositories~~ [notes](#RA2/b-item2)
3. ~~Submit jobs to condor~~ [notes](#RA2/b-item3)
	+ ~~need to make sure that both prompt and reprocessed datasets are in looper with the right scenario~~
4. Announce the files once they are done
5. Make new plots for the DPS -- update plots by Monday morning for the DPS
6. Edit RA2/b section of the DPS note... I think its in rough shape

### NOTES: 
#### item 1 <a name="RA2/b-item1">

Working with SuSySubstructure branch 'synch_June26_2015'.  
Again I had this issue when I tried to updates from the remote, git complains:
<pre>git: 'Merge branch 'synch_June26_2015' of https://github.com/awhitbeck/SuSySubstructure into synch_June26_2015' is not a git command. See 'git --help'.</pre>
I don't get this, but I have been just doing a forced reset when I run into this problem.  There must be a better way to fix this though.  So, I fetched the latest and then did a hard reset: 
<pre>git fetch
git reset --hard origin/synch_June26_2015</pre>
Maybe the issue is actually that I keep doing this and all of the other branches are really messed up... Oh well.  For now it works. 

Adding reprocessed data files, see [here](https://cmsweb.cern.ch/das/request?view=list&limit=50&instance=prod%2Fglobal&input=dataset%3D%2F*%2FRun2015B-17Jul2015-v1%2FMINIAOD).  Unfortunately, the files names of the MINIAOD tier do not help, but the run list helps, e.g. [here](https://cmsweb.cern.ch/das/request?view=list&limit=50&instance=prod%2Fglobal&input=run+dataset%3D%2FSingleMuon%2FRun2015B-17Jul2015-v1%2FMINIAOD). 

I move Kevin's script into the SuSySubstructure repo.  There are now several copies of it in each of the relevant directories so config files can easily be updated.  All reprocessed files have been downloaded, I am not removing the relevant runs from the prompt files which overlap with the reprocessed files.  

<table>
<tr> 
	<td> PD </td> <td> last run in reprocessed dataset </td>
</tr>
<tr>
	<td> DoubleEG </td> <td> 251521 </td>
</tr>
<tr>
	<td> DoubleMuon </td> <td> 251559 </td>
</tr>
<tr>
	<td> EGamma </td> <td> 251250 </td>
</tr>
<tr>
	<td>HTMHT </td> <td> 251521 </td>
</tr>
<tr>
	<td> SingleElectron </td> <td> 251521 </td>
</tr>
<tr>
	<td> SingleMu </td> <td> 251160 </td>
</tr>
<tr>
	<td> SingleMuon </td> <td> 251559 </td>
</tr>
<tr>
	<td> SinglePhoton </td> <td> 251521 </td>
</tr>
</table>

Overlapping runs should now be cleaned up -- I need a way of double checking this, though. 

https://github.com/awhitbeck/SuSySubstructure/commit/02732d471ff4eba52c876f956695a207c200f2d5

#### item 2 <a name="RA2/b-item2">

Grabbed .db that Nhan forwarded from Alexx Perloff.  This is now committed to the repo:

https://github.com/awhitbeck/SuSySubstructure/commit/fa4b01fe599648830c8a1791f425a439bd8b7588

#### item 3 <a name="RA2/b-item3">

Adding all scenarios to the help field of the scenario option in condorSub/generateSubmission.py.  The full list should be:

 - Phys14
 - Spring15
 - 2015B
 - re2015B

These are now configured correctly, hopefully:

<pre>
if options.scenario == "Phys14":
    Global_Tag="PHYS14_25_V2"
    tagname="PAT"
    geninfo=True
    jsonfile=""
    jecfile=""
    residual=False
elif options.scenario == "Spring15":
    Global_Tag="MCRUN2_74_V9"
    tagname="PAT"
    geninfo=True
    jsonfile=""
    jecfile="Summer15_25nsV2_MC"
    residual=False
elif options.scenario == "2015B":
    Global_Tag="74X_dataRun2_Prompt_v1"
    tagname="RECO"
    geninfo=False
    jsonfile="Cert_246908-251883_13TeV_PromptReco_Collisions15_JSON_v2.txt"
    jecfile="Summer15_50nsV2_DATA"
    residual=True
elif options.scenario == "re2015B":
    Global_Tag="74X_dataRun2_Prompt_v1"
    tagname="PAT"
    geninfo=False
    jsonfile="Cert_246908-251883_13TeV_PromptReco_Collisions15_JSON_v2.txt"
    jecfile="Summer15_50nsV2_DATA"
    residual=True
</pre>

Organized the looper script a bit and added the reprocessed Run2015B datasets.  Now all committed to synch_June26_2015:

https://github.com/awhitbeck/SuSySubstructure/commit/ca03329fe4e09f79b631d2ae7a621b8e5a374cc2

File should show up in:
<pre>/eos/uscms/store/user/lpcsusyhad/SusyRA2Analysis2015/FinalProductionDPS</pre>
 
 jobs were submitted from:
 <pre>/uscms_data/d2/awhitbe1/workArea/RA2studies/commission2015/CMSSW_7_4_6_patch6/src/AWhitbeck/SuSySubstructure/test/FinalProductionDPS</pre>

***oops!!!!*** I forgot to update the TreeMaker package to the latest release...

okay, I updated to the latest release and compared against the latest pull request into CMSSW_7_2_X to be sure.  I also cleaned up my area and recompiled:
<pre>git pull # I don't think this did anything
git fetch --all
git branch
git pull origin # this didn't do anything
git pull origin CMSSW_7_2_X # I am not sure if this did anything
git checkout -b b_2015B_v2.0 2015B_v2.0 
cmsenv
scram b clean
scram b -j8</pre>

Now submitting...

## *Dissecting jets+MET*

To do list :

1. Finish writing up a section in the paper on the variables and their distributions

2. Make 2D plots 

### *HF frontend commissioning*

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