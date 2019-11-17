# Speakers

## Issue:

The volume of the inbuilt speakers were not being able to changed. The volume would either be 0% or 100%. 

## Solution Overview:

I had noticed that changing the master volume did nothing, but changing the 
**PCM** in `alsamixer` did in fact change the volume level and maintained the sound quality. Therefore the following remaps the keyboard buttons to change the **PCM** settings rather than the master
volume.

## Solution

1. Install Pulseaudio (Pavucontrol)

2. Uncomment and change the following lines in `/etc/pulse/daemon.conf`:

   ```
   enable-lfe-remixing = yes
   lfe-crossover-freq = 250
   ```

3. Add the following code block in `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common`:

   ```
   [Element Master]
   switch = mute
   volume = ignore
   ```

   above the following block. (Do not change this block)

   ```
   [Element PCM]
   switch = mute
   volume = merge
   override-map.1 = all
   override-map.2 = all-left,all-right
   ```





## Discussion

Although there are other solutions such changing the Audio profile in `pavucontrol` to Analog 2.1 + Stereo, I found that those solutions severely degrade audio quality whereas this one does not (if it does, it is not noticeable). 