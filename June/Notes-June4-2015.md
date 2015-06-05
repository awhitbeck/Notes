
Research Notes - June 4, 2015
------------------------------------

### Updates to TreeMaker 

 - Frank has added some code to include leptons and charges of leptons into the main TreeMaker config file. 
 - Fixed bug which was causing a "Plugin not found" error.
 - Adding new JECs back into workflow by default.

### Checked synchronization with Jack

- still don't agree will jack, don't know why yet.

### LPC events committee
 - announced HATS for the summer
 - worked out schedule of 'Framework 101'
 - got a week for the precision mass measurement workshop
  - need to settle on the exact dates
  - need to submit a conference exception
  - need to review updated agenda from steven

### Checking gen-level $Z_{p_T}$ distributions 

<pre>
cd /uscms_data/d2/awhitbe1/workArea/RA2studies/commonFramework/newRepo_March8_2015/CMSSW_7_4_1/src/AWhitbeck/SuSySubstructure/test/ZtoInvisibleEst

python -i genLevelTest_pedroTree.py
</pre>
*I don't understand how to upload images! -- this is a major limitation for efficient note taking...*

I think that the low Pt stuff could be do to inefficiencies in lepton reconstruction.  I think to check this one will have to clean gen-level leptons from jets and then recompute things in the phase space of the analysis.

> Written with [StackEdit](https://stackedit.io/).