# Memory’s Tech Tips’ Unattended Windows Installation

## Overview

Microsoft gives you the ability to add [Answer Files](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/update-windows-settings-and-scripts-create-your-own-answer-file-sxs?view=windows-11) (or Unattend files) to Windows Installation Media, which can be used to modify Windows Settings and Packages in the Windows Image (ISO) during the Windows Setup process.

If you’ve ever used Rufus to create Windows Installation Media, you might have seen options like “Remove Windows 11 Hardware Requirements” and “Disable Privacy Questions”. When you select those options, Rufus creates an answer file with your selected options and includes it on the installation media.

I've created a few of these answer files that I use to automate and streamline my Windows installs, and that’s what I’m sharing with you in this project. 
  - The answer files work on any edition (Home/Pro) of Windows 10 22H2 and Windows 11 23H2.
  - *Windows 11 24H2 will be tested once it's fully released.*

My motivation for this project is to get an “IoT-LTSC-Like” or even better experience on the Pro and Home versions of Windows 10 and Windows 11 without having to worry about getting an LTSC License or ISO file.

> [!NOTE] 
> 
> I made these answer files to fit my needs, and they work great for me. They might not work for you, and that's okay. I can't help with every problem you might have. Check out the [Troubleshooting](https://github.com/memstechtips/UnattendedWinstall/blob/main/TROUBLESHOOTING.md) page for fixes to common "issues", or you can [create your own file](https://schneegans.de/windows/unattend-generator/) using these [video instructions.](https://youtu.be/WyLiJl-NQU8)
<br/>
<br/>

## Why should I use an Answer File?

### <ins>Security:</ins>
  - You can see all of the changes that will be made to the Windows Image by inspecting the answer file.
  - It runs on the Official Windows 10 or 11 ISO downloaded directly from Microsoft, no need to download edited ISO files from Unofficial sources.
  - It's not dependent on any third party tools and is an Official Microsoft Feature used to make Mass Windows Deployments easier.
### <ins>Automation:</ins>
  - When installing Windows on multiple computers, there's no need to manually configure settings and run scripts on each machine, which saves a lot of time (and effort).
<br/>

## What does Memory's UnattendedWinstall answer files do?

I've taken the time to add descriptions to almost all of the tweaks and registry entries in the answer files, and you can inspect them right here on GitHub. Alternatively, you can download the answer file and use a code editor like [Cursor](https://www.cursor.com/), [VSCode](https://code.visualstudio.com/) or [Notepad++](https://notepad-plus-plus.org/downloads/) to inspect it and make changes to it if needed.

### <ins>In addition to my tweaks, it contains elements and scripts from the following sources:</ins>

- Base Answer File generation:
  - [Schneegans Unattend Generator](https://schneegans.de/windows/unattend-generator/)
- Windows Tweaks & Optimizations:
  - [ChrisTitusTech WinUtil](https://github.com/ChrisTitusTech/winutil)
- Various Tweaks:
  - [Tiny11Builder](https://github.com/ntdevlabs/tiny11builder)
  - [Ten Forums](https://www.tenforums.com/)
  - [Eleven Forum](https://www.elevenforum.com/)
  - [Winaero Tweaker](https://winaerotweaker.com/)

### <ins>The Most Notable Tweaks & Registry Entries:</ins>

- Bypasses Windows 11 System Requirements.
- Removes Preinstalled Bloatware Apps.
- Bypasses FORCED Microsoft Account creation during Onboarding Experience.
- Disables Windows Spotlight.
- Disables Xbox GameDVR.
- Customizes Start Menu and Taskbar settings.
- Disables various Windows features like Cortana, Telemetry, and Location Tracking.
- Configures Windows Update to only install security updates and delay other updates for 1 year (max period).
- Disables Windows Error Reporting, Update Delivery Optimization, and Windows Remote Assistance (not RDP).
- Sets various performance and privacy-related registry keys, mostly found in the [ChrisTitusTech WinUtil](https://github.com/ChrisTitusTech/winutil).
- Enables and sets the Ultimate Performance power plan as active.
- Sets numerous Windows services to manual or disabled to optimize performance.
- Enables Dark Mode by default.
- Aligns the Start Button in Windows 11 to the left by default.
- Makes the Taskbar on Windows 10 Small and Transparent.
- Executes PowerShell and batch scripts to apply additional tweaks and remove specific applications like Microsoft Edge *(Standard & Core Only)*, OneDrive, and Teams.
> [!NOTE]
>  Due to the removal of Microsoft Edge, I also include a Powershell Script on the Desktop called "LAUNCH-CTT-WINUTIL.ps1" <br/> 
>  - Make sure you are connected to the internet, then right click on this file and select Run with Powershell. <br/>
>  - Accept the UAC prompt and it will launch the Chris Titus Tech Windows Utility and you can use that to install your browser of choice (even Edge) and any other software for that matter.
<br/>

## Usage Instructions

### <ins>Choose one of the following versions:</ins> <br/> 
*32bit, 64bit and arm64 is supported on all versions.*
### [**IoT-LTSC-Like**](https://github.com/memstechtips/UnattendedWinstall/blob/main/IoT-LTSC-Like/autounattend.xml)
### *Recommended for most people*
   - Includes most of the same Windows Packages as the official IoT-LTSC version of Windows:
     - (Windows Security, Edge, Notepad, Snipping Tool, Calculator, Paint, Legacy Windows Media Player) with added Microsoft Store.
   - Only Security updates are installed, others are delayed for 1 year (max period)
   - Includes better privacy settings and various other tweaks, view [CHANGELOG](https://github.com/memstechtips/UnattendedWinstall/blob/main/CHANGELOG.md) for a full list.
<br/>

## <ins>**Installing Windows with an Answer File**</ins>
In short, you need to include the `autounattend.xml` answer file on your Windows Installation Media so it can be read and executed during the Windows Setup. 

> [!NOTE]<br/>
> - The filename included on the root of the Windows image USB Drive must be `autounattend.xml` or else it won't execute.
<br/>

### <ins> Create a Bootable Windows Installation Media using Ventoy</ins> 

1. Download the  `autounattend.xml` file and save it.
2. Create a Windows iso image [UUP Dump](https://uupdump.net/) and write to a [Ventoy](https://www.ventoy.net/en/download.html) bootable USB drive. (Minimum storage requirement = 8gb)
3. Copy the `autounattend.xml` file you downloaded in Step 1 to the root of the Bootable Windows Installation USB you created in Step 2.
4. Boot from the Ventoy USB, do a clean install of Windows as normal, and the scripts will run automatically.
</br>

## FAQ

### Can I use the answer file with an in-place Upgrade?
  - No.

Happy installing!
