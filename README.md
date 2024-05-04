# BTLO-Bruteforce

<hr>
<h3>Overview</h3>

<hr>

<h4>Cloud Tools and Evnironment</h4>
PowerShell, Text editor, Excel, Google sheet

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
After extracting the zip file, you will find the following files:

- `BTLO_Bruteforce_Challenge.csv`
- `BTLO_Bruteforce_Challenge with Event log type`
- `BTLO_Bruteforce_Challenge with Text document type`
- `READ ME.md`
<br>
Please ensure you read the "READ ME" document as it may contain valuable information.
<br>
You can use any tool suitable for handling .csv files, such as PowerShell, a Text Editor, Excel, or Google Sheets. Please note that Google Sheets might alter the formatting when you upload the file.

<img src="images/4.png" width="550">
<br>
We will be utilizing PowerShell for this task. 

Open up the PowerShell then type <b>cat .\BTLO_Bruteforce_Challenge.txt</b> to display the contents of the file. 
<br>
Please note that loading everything might take some time.

<img src="images/5.png" width="1000">
<br>
This is the screen you will see, and you'll notice that the scrollbar has gotten much smaller and moved all the way down.

Now that we have the logs displayed in PowerShell, let's dive into the questions.

<img src="images/6.png" width="550">
<br>

<br>
<h4>Question #1: How many Audit Failure events are there?</h4>
We have the option to go through entire logs to find the answers we need, or we can efficiently use the command line in PowerShell.

Let's clear the screen with the <b>cls</b> command and start afresh.then type the following command:
<br>
<b>(Get-Content BTLO_Bruteforce_Challenge.csv | Select-String -Pattern "Audit Failure").Count</b> then we get our answer 3103.

<img src="images/7.png" width="1000">
<br>
<h4>Question #2: What is the username of the local account that is being targeted?</h4>
To find this, open a new PowerShell window and type:<b>cat .\BTLO_Bruteforce_Challenge.csv</b>

Then, scroll up to the last audit failure log. As you can see, the account name being targeted is "administrator."

<img src="images/8.png" width="550">
<br>
<h4>Question #3: What is the failure reason related to the Audit Failure logs?</h4>
To answer this, refer back to the last log entry. Under the "Failure Information" section, you will find the failure reason listed as:

Failure Reason: Unknown user name or bad password.
<br>
This tells us that the audit failures are due to either unrecognized usernames or incorrect passwords.

<img src="images/9.png" width="550">
<br>
<h4>Question #4: What is the Windows Event ID associated with these logon failures?</h4>
To find this, look at the last log entry. The Event ID associated with these logon failures is 4625.

<img src="images/10.png" width="550">
<br>
I've also included this information in case you are not familiar with the term "Event ID."

Below is a sample log from the BTLO file:

<img src="images/11.png" width="550">
<br>
<h4>Question #5: What is the source IP conducting this attack?</h4>
You can find this information under "Network Information." Look for "Source Network Address," which is 113.161.192.227.

<img src="images/12.png" width="550">
<br>
<h4>Question #6: What country is this IP address associated with?</h4>
For this we are going to utilize <a href="https://ipgeolocation.io/">ipgeolocation</a>.

This website offers detailed geographical information about IP addresses.
<br>
Copy and paste the IP address from question 5, then press Enter.

<img src="images/13.png" width="550">
Here you will find various details such as the country, city, and even latitude and longitude. However, the specific answer we are looking for is the country: Vietnam.
<img src="images/14.png" width="550">
Find another engaging lab using the ipgeolocation service in our project on GitHub:<a href="https://github.com/J-SinwooLee/Azure-SIEM-Honeypot">Azure-SIEM-Honeypot</a>.
<br>
<h4>Question #7: What is the range of source ports that were used by the attacker to make these login requests?</h4>
This question could be answered more quickly using Excel or Google Sheets, but we will continue to use PowerShell.
Type:<b>(Get-Content 'BTLO_Bruteforce_Challenge.csv' | Select-String -Pattern 'Source Port:' | ForEach-Object { $_ -replace '.*Source Port:\s*(\d+).*', '$1' }).Trim() | Out-File 'source_ports.txt'</b>
<img src="images/15.png" width="1000">
This will result in a file named 'source_ports.txt' that contains one source port number per line, with each number being a port extracted from lines containing 'Source Port:' in the original CSV file. This file will not contain any other information besides the port numbers, stripped of all additional text and whitespace.
<img src="images/16.png" width="550">
<br>
<h2>Conclusion</h2>

