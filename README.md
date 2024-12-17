# Windows Autoruns

<h2>Description</h2>
In this task, I created a backdoor in Ubuntu through a previously created malware, used Registry Editor to enumerate the backdoor registry key, installed a powershell autoruns modeule from github, used the module to create a abseline without the backdoor, then recreating the backdoor from Ubuntu to create a save state with the backdoor, then using autoruns script to compare the two baselines to enumerate the backdoor. 


<h2>Languages and Utilities Used</h2>

- <b>Windows cmd</b>
- <b>Windows powershell</b>
- <b>linux CLI</b>


<h2>Environments Used </h2>

- <b>Unbuntu</b>
- <b>Windows 10 Enterprise</b> 

<br />
<br />
Exploring Windows Registry going into Current User Runs. 

![1) run under HKEY_Current_User](https://github.com/user-attachments/assets/62078113-0b5a-4bd3-b00b-610b83324d59)

<br />
<br />
Exploring Windows Registry going into Local Machine Runs. 

![2) run under HKEY_LOCAL_MACHINE](https://github.com/user-attachments/assets/ee9882db-e023-426f-a3da-fc58a3c00301)

<br />
<br />  
Using the cmd in windows to query Current User and Local Machine Runs and RunOnce.

![3) using cmd to query hkey run registry keys for current user and LM](https://github.com/user-attachments/assets/32309896-bf3e-4ad3-aa24-06c3336b2298)

<br />
<br />
Using get-itemproperty in powershell to show Run in current user registry. 

![4) querying registry run in powershell](https://github.com/user-attachments/assets/85bb001d-1ee6-4646-8239-9e976b3bd68b)

<br />
<br />
On my ubuntu vm, started metasploit to use handler, set reverse shell, listening host and port, and run exploit. 

![5) reinfecting windows vm with reverse tcp](https://github.com/user-attachments/assets/367d232f-2946-4d5e-9e09-612c4c6da2e5)

<br />
<br />
With the shell running, wrote reg add "registry key path" /v "NotABackdoor" /t REG_SZ "path to malware" /f. 

![6) in shell, create regirstry to run notmalware exe](https://github.com/user-attachments/assets/d8d53199-3f1f-41ac-916b-7a5a21763b06)

<br />
<br />
Showing the active backdoor in Registry Editor, cmd, and pwoershell. 

![7) HKCU keys shows notabackdoor as autorun](https://github.com/user-attachments/assets/90be1a2c-0f0c-4918-9cbe-ce13ca1c9f7e)

<br />
<br />
Exiting and restarting msfconsole and signing out then signing back in to windows vm to show the backdoor to autorun. 

![8) exiting and restarting msfconsole and signing out andin in windows autoruns the backdoor session](https://github.com/user-attachments/assets/3001074c-24e5-49c5-9844-dd0addfb165b)

<br />
<br />
In sysinternals autoruns shows NotABackdoor along with properties. 

![9) autoruns highlights notabackdoor and shows properties](https://github.com/user-attachments/assets/aa432775-0967-4b7d-a242-0f6cc062c8bc)

<br />
<br />
Downloading the autoruns script for powershell from https://github.com/p0w3rsh3ll/AutoRuns, I imported the module by setting execution policy to unrestricted then enumerating the get-commands for autoruns. 

![10) downloading github powershell autorun script and imporitng module in powershell](https://github.com/user-attachments/assets/70af8cc4-adf3-409e-925e-3b274ae6d1f6)

<br />
<br />
I then deleted the NotABackdoor so I could follow the strings to create a baseline of the system in a baseline directory. 

![11) making a baseline of the current windows system using autoruns github](https://github.com/user-attachments/assets/17f2b928-1e9b-4b1f-a8bb-abf27c627272)

<br />
<br />
I then recreated the backdoor in Ubuntu. 

![12) recreating the backdoor ](https://github.com/user-attachments/assets/25ffecc4-bed9-4935-b504-816c74feae7f)

<br />
<br />
Running the same strings to save a Current State snapshot in baseline directory. 

![13) creating current state snapshot](https://github.com/user-attachments/assets/25238be0-5953-4423-b178-0226331a2110)

<br />
<br />
Finally, running compare-autorunbaseline to compare the two snapshots shows NotABackdoor and its imagepath enumerated in the current state snapshot. 

![14) backdoor identified coparing baseline and current state](https://github.com/user-attachments/assets/5917d94c-30cf-4df3-a308-cb9269e6a1b4)

<br />
<br />
