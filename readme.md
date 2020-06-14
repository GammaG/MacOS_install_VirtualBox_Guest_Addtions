**Setup the VM**

https://github.com/GammaG/macos-virtualbox

**Recovery Mode**

*Enter recovery mode*

While beeing inside MacOS enter in terminal

    sudo nvram "recovery-boot-mode=unused"
    sudo reboot

This sets a firmware variable in nvram indicating that you want to start in Recovery mode on the next boot, and then reboots the machine.

*Reboot into system*

When done in Recovery mode, run the following from the Terminal in Recovery mode:

    nvram -d recovery-boot-mode

This deletes the firmware variable so that the next boot is a normal boot.
If Recovery boot fails and you cannot progress, you could also remove the firmware variable by holding down the keys Command, Option, P, and R during boot. This resets the nvram and thus the firmware variable.

**Disable Kernel Protection**

*Deactive SIP*

In Recovery Mode Terminal

    csrutil disable

to check

    Test Protection
    csrutil status 

Should show DTrace Restrictions: disabled if not repeat


*Deactivate Gatekeeper*

    sudo spctl --master-disable

to check

    spctl --status

**Add Guest Additions Signature**

    Allow VirtualBox
    spctl kext-consent add VB5E2TV963

To check

    Check
    spctl kext-consent list

**Make the folder writeable in MacOS**

    sudo mount -uw /

    sudo chown :admin /System/Library/Extensions/

    sudo chmod 775 /System/Library/Extensions/ 