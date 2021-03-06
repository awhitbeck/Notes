Research Notes - August 8, 2015
------------------------------------
## *Summary*

Working on 3 main projects today:

- [RA2/b](#RA2b) -- Most of this work had to do with finalizing all of the necessary updates to the analysis code so that the, hopefully, final version of the ntuples could be produced.  

<a name="RA2b">
## *RA2/b* 

To do list :

1. ~~make configuration files that have the rereco data and non-overlapping prompt data~~ [notes](#RA2b-item1)
2. ~~track new .db file if the residual corrections become available in both repositories~~ [notes](#RA2b-item2)
3. ~~Submit jobs to condor~~ [notes](#RA2b-item3)
	+ ~~need to make sure that both prompt and reprocessed datasets are in looper with the right scenario~~
4. ~~Announce the files once they are done~~

### NOTES:

<a name="RA2b-item1"> 
#### item 1 

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

Overlapping runs should now be cleaned up; I need a way of double checking this, though. 


<a name="RA2b-item2"> 
#### item 2 

Grabbed .db that Nhan forwarded from Alexx Perloff.  This is now committed to the repo.

<a name="RA2b-item3"> 
#### item 3 

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

Jobs failed first submission.  It turns out there was key merge in Kevin's instructions for the MET correction that I missed.  I set up a fresh working area here:
<pre>/uscms_data/d2/awhitbe1/workArea/RA2studies/commission2015/CMSSW_7_4_6_patch1/src/</pre>
Then checked out and compiled all of the code:
<pre>cmsrel CMSSW_7_4_6_patch1
cd CMSSW_7_4_6_patch1/src
cmsenv

git cms-merge-topic -u cms-met:METCorUnc74X
git clone https://github.com/TreeMaker/TreeMaker.git -b CMSSW_7_2_X
cd TreeMaker
git checkout -b b_2015B_v2.0 2015B_v2.0
cd ..
mv TreeMaker/* .

git clone git@github.com:awhitbeck/SuSySubstructure.git -b synch_June26_2015 AWhitbeck/SuSySubstructure
cd AWhitbeck/SuSySubstructure
./retrieveFastJetTools.sh
cd ../../
scram b -j 8</pre>
   
I then tested the PHYS14production.py config file on MC, which uncovered a problem with a module being loaded that does exist; this was removed and the changes were pushed back into github. 

commit is [here](https://github.com/awhitbeck/SuSySubstructure/commit/42bbf9ed2e44d0a34e3e2fb460613ff00d028342)

I also tested the configuration file locally on data, this revealed a problem with the L2L3 residual corrections in the file that Nhan and Alexx forwarded me:

<pre>----- Begin Fatal Exception 08-Aug-2015 07:48:29 CDT-----------------------
An exception of category 'InvalidRequest' occurred while
   [0] Processing run: 251252 lumi: 67 event: 40810229
   [1] Running path 'WriteTree'
   [2] Calling event method for module LeptonProducer/'LeptonsNew'
   [3] Calling produce method for unscheduled module PATMETSlimmer/'slimmedMETsNoHF'
   [4] Calling produce method for unscheduled module CorrectedPATMETProducer/'patPFMetT1NoHF'
   [5] Calling produce method for unscheduled module PATPFJetMETcorrInputProducer/'patPFMetT1T2CorrNoHF'
Exception Message:
The JEC level L2L3Residual does not exist !!
Available levels = { Uncorrected, L1FastJet, L2Relative, L3Absolute }.
----- End Fatal Exception -------------------------------------------------</pre>

I have already email Nhan and Alexx about this.  For now I am submitting jobs with no residual corrections.


> Written with [StackEdit](https://stackedit.io/).