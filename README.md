<h1>Creating a simple File Integrity Monitoring (FIM) script</h1>

<h2>Description</h2>
This File Integrity Monitoring (FIM) project is a PowerShell-based solution designed to monitor changes in a directory by creating a baseline of file hashes and comparing them to their current state. The script detects and alerts users of file modifications, deletions, and the addition of new files. This ensures the integrity of sensitive files and helps detect unauthorized changes.
<br/>
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/d160e76a-85f9-4856-9c6e-93f5825c50f1" width="700">
</div>
<br/>
<i>Estimated completion time: 2 hours</i>
<br/>
<br/>

<h2>Objectives</h2>
The objective of this lab is to create a baseline of file hashes in a specified directory, monitor files continuously against the baseline for changes, additions, or deletions and if any other theses was detected, user will be notified of any integrity violations in real-time.
<br/>
<br/>

<h2>Skills learned</h2>

- Hashing and integrity checking.<br />
- Real-time monitoring using PowerShell.<br />
- Log file creation and management.<br />
<br/>
<h2>Tools Used </h2>
<b>PowerShell:</b> For scripting and real-time monitoring.<br />
<b>SHA512 Hashing:</b> To ensure file integrity.<br />
<b>Baseline File:</b> Stores the initial state of monitored files.<br />
<br/>
<h2>Program walk-through:</h2>
<h3>Step 1 -Setting Up the Script:</h3> 
First thing I did was open PowerShell ISE and I started a new script file by defining the necessary functions:
<br/> 
<br/> 
<b>Calculate-File-Hash:</b> Computes the SHA512 hash of a given file.
<br/> 
<b>Erase-Baseline-If-Already-Exists:</b> Deletes the baseline file (baseline.txt) if it exists.
<br/> 
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/454674f1-c642-4118-a323-62fb9e7ee81b" width="400">
</div>
<br/> 
<h3>Step 2 - Adding User Interaction:</h3>  
<br/>
Next thing was creating the code to prompt the user for the desired action:
<b>Option A:</b> Create a new baseline.
<b>Option B:</b> Start monitoring files using an existing baseline. 
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/ef58a318-9ac3-4256-9363-ba25a926c046" width="400">
</div>
<br/>
<h3>Step 3 - Implementing Baseline Collection:</h3>
If the user selected <b>A</b>, it would clear any existing baseline and calculate the hashes for all files in the directory. Next it would save the file paths and their corresponding hashes to <b>baseline.txt</b>.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/45709db8-5555-4b03-bd3b-e7a4d574d387" width="400">
</div>
<br />
<h3>Step 4 - Implementing File Monitoring</h3>
But if <b>B</b> was selected, it would load the existing baseline from <b>baseline.txt</b> into a dictionary for fast lookup. Then it would start monitoring the files in a continuous loop detecting new files, detecting modified files and detecting deleted files.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/c138b576-0a09-43fa-98cd-56c0a2d9975e" width="500">
</div>
<br />
<h3>Step 5 - Testing and Running the Script</h3>
To run the script, first thing is save the script as FIM.ps1. Once ran, two options would be given to the user:
<br />
<br />
<img src="https://github.com/user-attachments/assets/123e6c58-e38c-4b46-973c-dc419eb4dcd2" width="400">
</div>
<br />
<br />
When entering <b>A</b>, considering the folder contained the following files. the baseline.txt file would be created with the following data:
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/cd164da5-e828-4ffc-9fb6-77a37e764a8b" width="500">
</div>
<br />
<br />
Once there’s baseline created, if <b>B</b> was chosen the script would monitor for changes. If a file was created the following message would start to popup:
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/e312eada-d65f-4173-848f-6b6829475e9f" width="500">
</div>
<br />
<br />
If a file was modified, this would be the message:
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/7fb6b355-04e2-46d9-ac8a-fb2297765d5e" width="400">
</div>
<br />
<br />
If a file was deleted, this would be the message:
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/5d79d04c-0c96-47aa-8f5c-5ad03ba4c2f0" width="400">
</div>
<br />
<h2>Summary</h2>
This projected aimed the creation of a FIM script that automates the detection of changes to files in a specific folder using hash comparisons. By understanding and following this walkthrough, I gained insights into practical PowerShell scripting techniques, hash-based integrity monitoring and real-world applications for file monitoring in cybersecurity.

  <!--
 ```diff
