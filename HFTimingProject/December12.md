### Goals for HF timing studies with QIE10 ###

 0. Build a simple analysis framework [notes](#framework)
 1. Show plot of energy distribution for all events 
 2. Show plot of timing for all events versus run number to figure out exactly when the clock phase was changed (analysis should be split into three periods according to this)
 3. Show timing distribution of showers relative to timing distributions from PMT hits — derive cuts for isolating PMT hits
 4. Show rates versus energy
 5. Correlate early timing hits with topological cuts and possibly pre-triggers
 6. Try to extrapolate rates from single channel to entire detector
 7. Understand the impact on MET and forward jets
 8. Make recommendations for DQM for 2016

<a name="framework">

 - Need to first make a list of all runs that are relevant and put them into a cff.py file
 - Build an analyzer that can make a nice flat tree (maybe use the RA2/b TreeMaker package)
