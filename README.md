# A simple guide to completely fix sleep/wake issues on hackintosh laptops

I have tried this with my laptop and works fine. I do not have any idea about desktop users. So they can give it a try and let me know if it works

---

### Preparations
So to start with we need to remove any of the past patches like :-

- Any ssdt used (for eg. ssdt-GPRW,ssdt-UPRW etc.)

- Any config.plist patch used (for eg. GPRW to XPRW Patch , UPRW to XPRW Patch or any similar patches)

- Usb kexts (for eg. USBInjectAll.kext, USBMap.kext)

- Any usb renames in config.plist (for eg. EHC2 to EH02, XHC1 to SHCI or any similar)


---

## Grab your DSDT.aml

So now you will need a fresh copy of your DSDT.aml. There are a plenty of guides specifing how to dumb it and fix issues with it , so I consider you already know by now what we are doing here

---

## Tunning your DSDT.aml

- Now open your DSDT.aml in maciasl and pre-apply any necessary fixes

- Now inside Your Maciasl search for a method called ```_PRW```. It should look like this:
```js
    Method (_PRW, 0, NotSerialized)  // _PRW: Power Resources for Wake
            {
                Return (GPRW (0x6D, 0x04))
            }
```
- Note that this method should only return the power resource value as ```(0x09, 0x04)```
If it returns anything other than this you need to change it here aswell as in all the method calls listed by the name ```_PRW```.

![Alt text](https://github.com/grvsh02/A-guide-to-completely-fix-sleep-wake-issues-on-hackintosh-laptops/blob/main/Screenshots/maciasl.png)

- Also your return function might be different from mine. It's either of GPRW,UPRW or LANC.

- After the necessary changes all the ```_PRW``` should look like this :
```js
    Method (_PRW, 0, NotSerialized)  // _PRW: Power Resources for Wake
            {
                Return (GPRW (0x09, 0x04))
            }
``` 

- With this done you can save your DSDT.aml to your efi folder and add it to your config.plist.

#### Some other settings

Now we need to change some settings in our system preferences. These are totally optional and can depend on your system. For me these settings worked the best.

![alt text](https://github.com/grvsh02/A-guide-to-completely-fix-sleep-wake-issues-on-hackintosh-laptops/blob/main/Screenshots/onbattery.png)

![alt text](https://github.com/grvsh02/A-guide-to-completely-fix-sleep-wake-issues-on-hackintosh-laptops/blob/main/Screenshots/onpower.png)


#### If any one wants to come up with a ssdt or a config.plist patch for this can report back.
