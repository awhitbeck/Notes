Research Notes - August 10, 2015
------------------------------------
## *Summary*

Working on 1 main project today:

- [RA2/b](#RA2b) 

<a name="RA2b">
## *RA2/b* 

To do list :

1. Make patch for whatever went wrong with the L2L3 residuals
2. Edit RA2/b section of the DPS note [notes](#ra2b-item2)
	+ put new plots from commissioning [twiki](https://twiki.cern.ch/twiki/bin/view/CMS/RA2b13TeVCommissioning) into note
	+ get the relevant people to update their plots on the twiki
	+ edit the DPS

### NOTES:

<a name="RA2b-item1">
#### item 1:

+ Sam's plots are updated with the MET>190 cut?
+ Jack's plots have the full stats, but they are not with the new MHT3.0 variable
+ Got updated plots from Simon, but they don't yet include the event filters
+ No word about had tau, yet

<a name="RA2b-item2">
#### item 2:

Updating analysis note.  I need to be careful not to commit all of the editing I was working on before.  I should be able to just do and update though.  

Working directory:
<pre>/uscms_data/d2/awhitbe1/workArea/susy-DPS/notes</pre>

tdr style sourcing:
<pre>eval `./notes/tdr runtime -csh`</pre>

SVN update:
<pre>svn update SUS-15-001/</pre>

compiling latex:
<pre>tdr  --style=an b SUS-15-001</pre>

> Written with [StackEdit](https://stackedit.io/).