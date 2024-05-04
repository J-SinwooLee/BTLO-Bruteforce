# BTLO-Bruteforce

<hr>
<h3>Overview</h3>

<hr>

<h4>Cloud Tools and Evnironment</h4>
Powershell, Text editor, Excel, Google sheet

<h4>Source material</h4>

[Blue Team Lab Online](https://blueteamlabs.online/home)

<h2>Project walk-through</h2>
<hr>
Firt go to Blue Team Lab Online aka BTLO to download the file.

<img src="images/1.png" width="350">
<br>
Once you download the zip file. You will have to extract them and this will require a password which you can find next download file on BTLO website.

<img src="images/2.png" width="350">
<img src="images/3.png" width="350">
<br>
Files Included

After extracting the zip file, you will find the following files:
- `BTLO_Bruteforce_Challenge.csv`
- `BTLO_Bruteforce_Challenge with Event log type`
- `BTLO_Bruteforce_Challenge with Text document type`
- `READ ME.md`
<br>
Please ensure you read the "READ ME" document as it may contain valuable information.
<br>
You can use any tool suitable for handling .csv files, such as PowerShell, a Text Editor, Excel, or Google Sheets. Please note that Google Sheets might alter the formatting when you upload the file.

<img src="images/4.png" width="350">
<br>
For us we are going to utilize powershell.

Let's use <b>cat</b> command to get this thing out! Note that this may take awhile to load everything.

<img src="images/5.png" width="1000">
<br>
This is the screen you will see, and you'll notice that the scrollbar has gotten much smaller and moved all the way down

<img src="images/6.png" width="550">
<br>
We have the option to comb through entire logs to find the answers we need, or we can efficiently use the command line in PowerShell.

Let's clear the screen with the <b>cls</b> command and start afresh.
<br>
The first question we need to address is: How many Audit Failure events are there?
<br>
To find this, type the following command:
<b>(Get-Content BTLO_Bruteforce_Challenge.csv | Select-String -Pattern "Audit Failure").Count</b> then We get our answer 3103.

<img src="images/7.png" width="1000">
<br>
Moving on to the next question: What is the username of the local account that is being targeted?

To find this, open a new PowerShell window and type:<b>cat .\BTLO_Bruteforce_Challenge.csv</b>
<br>
Then, scroll up to the last audit failure log. As you can see, the account name being targeted is "administrator."

<img src="images/8.png" width="550">
<br>
<h2>Conclusion</h2>

