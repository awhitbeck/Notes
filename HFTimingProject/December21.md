### Latest development code ###

Instructions from Kevin Pedro:

<pre>
cmsrel CMSSW_8_0_0_pre3
cd CMSSW_8_0_0_pre3/src
cmsenv
git cms-merge-topic kpedro88:Phase1-HF2
scram b -j 8
</pre>

Setup seems to work fine.  I am just going through the different package to try and understand how everything fits together:

CalibCalorimetry  
CommonTools    
DataFormats     
HLTriggerOffline  
RecoLocalMuon     
SimG4Core      
Validation
CalibFormats      
CondTools      
EventFilter [notes](#EventFilter)     
IORawData         
RecoMET           
SimGeneral
Calibration       
DQM            
Geometry        
RecoJets          
RecoTBCalo        
SimTracker
CalibMuon         
Configuration  
FastSimulation  
L1Trigger         
RecoParticleFlow  
SimMuon
CaloOnlineTools   
DQMOffline     
HLTrigger       
RecoLocalCalo     
SimCalorimetry    
TrackingTools

<a name="EventFilter">

	<script type="text/javascript">
	
    	function showElement(id){
       	// get a reference to your element, or it's container
       	var myElement = document.getElementById(id);
       	myElement.style.display = '';
       	}

	    function hideElement(id){
	       var myElement = document.getElementById(id);
	       myElement.style.display = 'none';
   		}

	</script>

    <a href="#" onclick="showElement('imageId')" >show</a>
    <a href="#" onclick="hideElement('imageId')" >hide</a>
	<div id="imageId">
		this is a test paragraph
	</div>

