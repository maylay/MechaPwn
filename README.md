# MechaPwn

Disclaimer: DO NOT USE A ON A REAL DTL/DEX; This sets the QA flag which forces the use of the retail keystore, this would break memory card compatibility.

Real DEX (non QA) flags have not been added to the public version of mechapwn for your own safety.


The authors hold no responsibility should you break/damage your Playstation 2 console using this software



This tool can be used to change the region and configuration flags from Dragon based mechacon consoles

This means Playstation 2 consoles from the SCPH-5000X systems all the way to the SCPH-90000X are supported
(with the exception of the DESR (PSX) consoles which are not supported at this time, a future update is planned to address this)

Older Playstation 2 units do NOT use a Dragon based mechacon and therefore are not supported, no support is planned for those in the future.


How does it work?


The Dragon Based mechacon store configuration flags and patches encrypted in their eeprom, the patch DES key was eventually bruteforced which allowed code execution
on those units and for the full keystore to be dumped.

Normally the patch area is write protected and cannot be written to at runtime except while using PMAP in TEST mode (this requires soldering) furthermore the configuration area can only be written to when it is empty.

This is done to prevent an attacker or anyone outside of Sony's own factory to overwrite mechacon configuration.

However an exploitable bug was found in the writeconfig function which allows to write arbitrary data to the patch area,

this allows to write a mechacon patch which disables the write protection on mechacon configuration bits and thus set specific regions and flags to mechacon.


This allows the following:

On SCPH-5000X and SCPH-7000x:

* Disable disc region checks (ps1 and ps2 discs from all region as well as masterdiscs mount with data accessible)

* Change the region the console reports as, as well as change the disc/kelf region that mechacon allows

* BOOT original PS2 discs from NTSC-J and NTSC-U regions directly from the OSD (NTSC-J units only)

* BOOT original PS2 discs all regions directly from the OSD (NTSC-U and ASIA (non NTSC-J) units only)

* BOOT original PS2 discs all regions as well as PS2 Masterdiscs from all region by skipping the logo check (for example by loading a disc using ulaunchelf)

* BOOT PS1 disc originals and backups from the console's original region (NTSC-J and PAL consoles)

* BOOT PS1 disc originals and backups from all regions (NTSC-U and ASIA (non NTSC-J) units only)



On SCPH-7500X and later models (also known as Deckard consoles)

* Disable disc region checks (ps1 and ps2 discs from all region as well as masterdiscs mount with data accessible)

* Change the IOP ROM region (the ROM sets a specific bank according to the mechacon region flags)

* Change the region the console reports as, as well as change the disc/kelf region that mechacon allows

* BOOT original PS2 discs all regions directly from the OSD

* BOOT original PS2 discs all regions as well as PS2 Masterdiscs from all region by skipping the logo check (for example by loading a disc using ulaunchelf)

* BOOT PS1 disc originals and backups from all regions


FAQ: 

Why do PAL/NTSC-J consoles do not play NTSC/PAL discs (on scph-70000 and earlier) ?

The IOP ROM on those consoles have enforced strict logo decryption checks both in the PS1 and PS2 BIOS which the NTSC-U (also used in ASIA consoles) BIOS does not have.


Why do consoles not run masterdiscs directly from the OSD? 

An additional protection exists on the DSP, which is different in retail and debug consoles, the debug one allows mechacon to store the masterdisc xor key in its registers, the retail one does not.
Bypassing the logo check bypasses this protection (this can be done using ule or a future cdvdman patch using a ps2 homebrew)


How to use: 

Run Mechapwn once to install the exploit patch/payload an initial backup of your mechacon eeprom will be made to the usb mass storage device (keep it safe!),then power off the console by disconnecting it from the mains when asked (mechacon is on even when the ps2 cpu is off, so you really need to disconnect the power chord!) 


Run Mechapwn again to choose which region you want 


Retail will just set the region flag and machine ID of your chosing (it is not advised to mix and match different machine ID types, for example setting an SCPH-75001 ID to an SCPH-50004 console.

Debug will let you set a QA Flagged DEX configuration/region with a DEX machine ID of your chosing, this allows mechacon to read discs from all regions as well as masterdiscs (the retail option does not).


Run Mechapwn one last time to restore the original patch set (and uninstall the exploit patch) from your mechacon backup (you will need to reinstall the exploit patch to change your region again).

