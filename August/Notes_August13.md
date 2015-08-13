Research Notes - August 13, 2015
------------------------------------
## *Summary*

Working on 2 main project today:

- [RA2/b](#RA2b)
- [HF commissioning](#HFcommissioning)
- [pheno paper](#DissectingJetsMET)

<a name="RA2b">
## *RA2/b*

1. Remake Zinv plots for the DPS
	+ make sure to add the jetID and filters!!!
	+ implement the photon classification branches into tree maker
	+ try to get the QCD contamination added to the photon plots 
	
2. Collect plots from others and upload them to SVN


Helping Sam with his updated trigger studies.  The HT turn on looks much better now.  Apparently, it can get even better if we use an or of the ele15_IsoVVVL trigger with b-tagging, according to Manuel.  It also became apparent that Sam's observation that the JetID has a big impact on the efficiency is not crazy because despite my assumption, jets that fail the jetID ***are*** removed from the goodJets collection!!!!! ugh...

Trying to implement the non-prompt photon tagging and hadronization photon tagging into the PhotonIDisoProducer.  Using this code as a guide:
https://github.com/awhitbeck/ZtoInvisibleEst/blob/master/photonUtils.py#L42-L80
The algorithm is intended to go as follows:
* for each gen-photon (pdgId==22) that is matched to the candidate photon (ΔR<0.2)
	* check if its parent is a pion (or similar meson) - add one to pion count
	* check if its parent is a charged particle (including a proton) - add one to prompt count
 
* if pion count > 0 && prompt count == 0 -> photon candidate is non-prompt
* else -> photon candidate is prompt
  

<a name="HFcommissioning">
## *HF frontend commissioning* 

To do list:

1. Work on analyzing data from AMC13 
	+ test Jay's scripts 
	+ get a simple dump to work
	+ get an analyzer that makes useful plots

<a name="DissectingJetsMET">
## *Dissecting jets+MET* 

To do list :

1. Finish writing up a section in the paper on the variables and their distributions

2. Make 2D plots 


> Written with [StackEdit](https://stackedit.io/).