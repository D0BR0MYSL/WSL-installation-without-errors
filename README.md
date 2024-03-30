# WSL installation without errors - guide

## ![Platform](https://img.shields.io/static/v1?label=platform&message=windows11/10&color=blue&style=flat)  ![language](https://img.shields.io/static/v1?label=feature&message=WSL&color=orange&style=flat)

## About this guide

This is a short "step by step" guide that helps to prevent / fix some common errors during WSL installation.

This document was written as a useful note due to lack of comprehensive and straightforward instructions. As we all know, Microsoft is quite huge corp having different dev-teams working separately, thus if people still facing issues with WSL installation since so many years, the underlying cause is definitely related to subproducts isolation and bad cooperation between dev-teams. You'll see for yourself that security team (Windows Defender) and WSL team may have quite bad collaboration during releases, and this guide prooves this fact.

Obviously, I am unable to give 100% guarantee that it will work on future WSL and Windows updates, but it worked nicely since 2024 and will work some time ahead.

### Requirements/Target

- Windows 11 Pro
- Windows 10 Pro
- Windows Defender in any condition (working, disabled or forecefully inhibited forever)

This page does not include any files to download, so following this guide will be enough to get positive result on your PC.

### Errors covered

- 0x80370114 The operation could not be started because a required feature is not installed (but everyhting is installed correctly)
- 0x8007019e
- 0x8000000d
- and others

This guide is suitable for fresh install or already broken, In case of broken installation, you can undone everithing (uninstall) or just perform all oprations step by step.

## **Step by step guide**

**Step 1.** Enabling Windows features related to virtualization

Start typing to search in Start menu:

_**feat**_

and open suggested Control panel applet called:

**Turn Windows features on or off**

In Windows features list enable following features:  
(there is no need to reinstall any if already enabled)

- Hyper-V
- Virtual Machine Platform
- Windows Hypervisor platform
- Windows Subsystem for Linux

**Step 2.** Restart PC

**Step 3.** Running console commands

Subsequently run following commands as Administrator from CMD or Powershell:  
(there is nothing bad in repeating, if you already entered them many times trying to make things work)

`net start vmms`

`dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

`dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`

`wsl --set-default-version 2`

**Step 4.** Updating WSL engine

Update WSL engine/kernel by downloading and installing MSI package:

[https://aka.ms/wsl2kernelmsix64](https://aka.ms/wsl2kernelmsix64)

Additionally (**recommended**) run Windows Update and check for updates to install them (wsl engine update usually goes from there).

**Step 5.** Granting access in Windows Defender for virtual machine services (the main panacea!)

Start typing to search in Start menu:

_**exploit**_

and open suggested Windows Defender applet called:

**Exploit protection**

In Exploit protection settings window:

Click **Add program to customize** > **Choose extract file path**:  
Choose file

`c:\windows\system32\vmcompute.exe`

Click added file and click **Edit.**

Scroll down a bit to option called **Control folw guard (CFG)**

Enable checkbox called **Enable Override System settings**

Switch it into **On** state and enable checkbox **Use srtict CFG**

Add another system executable same way by enabling the "CFG" thing for it:

`c:\windows\system32\vmwp.exe`

**Step 5.** Install/register WSL distribution that suits your liking. Following command is an example of deploying the Ununtu 22.04 LTS:

`wsl --install -d Ubuntu-22.04`

That's all. Linux system will start without errors and you will see promt for entering user name and password.
