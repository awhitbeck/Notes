### Latest development code ###

Instructions from Kevin Pedro:

<pre>
cmsrel CMSSW_8_0_0_pre3
cd CMSSW_8_0_0_pre3/src
cmsenv
git cms-merge-topic kpedro88:Phase1-HF2
scram b -j 8
</pre>

Setup seems to work fine.  I am just going through the different package to try and understand how everything fits
together.  The relevant packages can be browsed on my laptop [here](file:///Users/awhitbe1/HFreco/). A simple 
tree that shows the package structure is [here](file:///Users/awhitbe1/HFreco/test.html).

For the packer/unpacker, I think all of the code is in EventFilter/HcalRawToDigi.

There seems to be code in both the src and plugins directories:

src:

| File Name  | Description   | Dependecies   |
| ---------- | ------------- | ------------- |
| AMC13Header.cc          | gets pointer to current AMC13 header??? | interface/AMC13Header.h | 
| HcalDataFrameFilter.cc  | implements a class which seems to simply check if data in digi collections are 'good' | interface/HcalDataFrameFilter.h | 
| HcalPacker.cc           | creates raw data from digi collections | interface/HcalPacker.h, interface/HcalHTRData.h, interface/HcalDCCHeader.h, interface/HcalGenericDetId.h, interface/MessageLogger.h, interface/FEDTrailer.h, interface/CRC16.h| 
| HcalUnpacker.cc| creates digi collections from raw data | interface/HcalUnpacker.h, interface/HcalDCCHeader.h, interface/HcalDTCHeader.h, interface/AMC13Header.h, interface/HcalHTRData.h, interface/HcalUHTRData.h, DataFormats/HcalDetId/interface/HcalOtherDetId.h, DataFormats/HcalDigi/interface/HcalQIESample.h, FWCore/MessageLogger/interface/MessageLogger.h, interface/HcalTTPUnpacker.h| 
| HcalDCCHeader.cc   |  | |      
| HcalFEDList.cc         | seems to just define a scheme for a range of FEDs based on calibration modules??? | DataFormats/FEDRawData/interface/FEDNumbering.h, EventFilter/HcalRawToDigi/interface/HcalDCCHeader.h, EventFilter/HcalRawToDigi/interface/HcalFEDList.h |  
| HcalTTPUnpacker.cc| | | 
| HcalDTCHeader.cc      | | |   
| HcalHTRData.cc          | | | 
| HcalUHTRData.cc| | | 

plugins:

| File Name  | Description   | Dependecies   |
| ---------- | ------------- | ------------- |
| HcalHistogramRawToDigi.cc |||         
| HcalLaserHBHEHFFilter2012.cc|||
| HcalCalibFEDSelector.cc        |||    
| HcalHistogramRawToDigi.h          ||| 
| HcalLaserHFFilter2012.cc|||
| HcalCalibTypeFilter.cc     |||        
| HcalLaserEventFiltProducer2012.cc  |||
| HcalRawToDigi.cc|||
| HcalDigiToRaw.cc   |||                
| HcalLaserEventFiltProducer2012.h   |||
| HcalRawToDigi.h|||
| HcalDigiToRaw.h   |||                 
| HcalLaserEventFilter2012.cc        |||
| modules.cc|||
| HcalEmptyEventFilter.cc            |||
| HcalLaserHBHEFilter2012.cc||| 


#### Side note ####

Its possible to construct content in html that can be toggle to appear and dissapear.  I am working on
some simple code to scan a CMSSW package and map out all of the classes they implement.  This is 
relevant for displaying the information in a user friendly way.

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

