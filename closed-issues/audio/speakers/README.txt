Problem: The volume of the inbuilt speakers were not being able to changed. The volume would either be 0% or 100%. I had noticed that changing the master volume did nothing, but changing the 
PCM in alsamixer did infact change the volume level and maintained the sound quality. Therefore the following remaps the keyboard butons to change the PCM settings rather than the master
volume.


Software Installed:
	1. Pulseaudio (pavucontrol)

Changes Made:
	1. In /usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common:
	ADD:
	
	[Element Master]
	switch = mute
	volume = ignore

	ABOVE
	
	[Element PCM]
	switch = mute
	volume = merge
	override-map.1 = all
	override-map.2 = all-left,all-right
