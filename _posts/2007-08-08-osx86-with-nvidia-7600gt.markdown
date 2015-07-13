---
layout: post
title: OSx86 with nVidia 7600gt
tags:
- Mac
- OSx86
---
This is quick and dirty how-to to get Quartz Extreme and Core Image at full resolution working on OSx86 (with OSX 10.4.8) a nVidia 7600gt 256MB card.

Follow the simple insructions below and you can’t go wrong:

- Install OSx86 with the optional `Natit` package
- Once booted find your card identifier by adding the `DeviceID` and `VendorID` together to get a string (mine is `0x02e110de`)
- Edit the corresponding `<string>` tag for the `IOPCIMatch` key in these four packages
  - `/System/Library/Extensions/Geforce.kext`
  - `/System/Library/Extensions/NVDANV40Hal.kext`
  - `/System/Library/Extensions/NVDANV30Hal.kext`
  - `/System/Library/Extensions/NVDAResman.kext`

If the file is like this:

```
<key>IOPCIMatch</key
<string>0x00000000&0x0000ffff</string>
```

Replace it with this:

```
<key>IOPCIMatch</key
<string>0x02e010de&0x0000ffff</string>
```

If the key has a number of values in the string tag, just add `0x02e010de&0x0000ffff` to the start of the list.

- You now need to flush the kext cache so run:    
`sudo rm /System/Library/Extensions`
- Now reboot and enjoy the goodness of Mac OSx86 :)

I cannot claim the credit for this, I got it from [a post by sinjon on the osxx86 forum](http://www.osxx86.info/vbulletin/showthread.php?t=1514)
