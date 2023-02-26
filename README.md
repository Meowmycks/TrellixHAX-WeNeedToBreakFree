# Trellix HAX 2023 Write-Up - *We Need to Break Free*

## Challenge Description

Our large-scale scans of possible networked machines used by the opposite coast have produced an interesting result: an unprotected repository which bears the same telltale fingerprint of known enemy hosts. However, the contents of the repository appear to be arbitrary, lacking in any significance... A honeypot, perhaps? You'd better have a poke around this system, just to make sure.

## Step 1 - Reconnaisance

Accessing the provided address ```trellixhax-we-need-to-break-free.chals.io``` reveals a simple HTML website that does checksum generation of various text files on the web server's directory.

![image](https://user-images.githubusercontent.com/45502375/221381875-661721ae-2fed-4620-9a76-d720f3ecc975.png)

Using Burp Suite, I capture the request made when generating a checksum of one of the files.

![image](https://user-images.githubusercontent.com/45502375/221381950-a1ee1073-ab74-4348-b54a-ee4fd3f36894.png)

## Step 2 - Exploitation

Testing for RCE, I append ```;id``` to the value assigned to the variable ```computeHashDropDown```. This proves successful.

![image](https://user-images.githubusercontent.com/45502375/221382062-e2e140cf-e5e5-4667-b4b3-90214821e03e.png)

The next step I take is to open a reverse shell that can be accessed externally.

Using [this guide](https://systemweakness.com/how-to-catch-a-reverse-shell-over-the-internet-66d1be5f7bb9), I open a Netcat listener and an Ngrok server redirecting external traffic to it.
I also generate a reverse bash payload using Msfvenom to be executed on the web server.

![image](https://user-images.githubusercontent.com/45502375/221382300-552c6217-bbf5-4abf-b3a6-dc5f84e03737.png)

Then, I use Burp Suite's Hackvertor extension to URL-encode the payload before executing it.

![image](https://user-images.githubusercontent.com/45502375/221382329-fd5ab610-6e43-4182-8719-d6582392c0a5.png)

After which, I add the final payload to the request and successfully gain a reverse shell.

![image](https://user-images.githubusercontent.com/45502375/221382347-3b888ca0-3efc-4531-b754-94ba07c163d6.png)

From there, I traverse the directory and ultimately find the flag.

![Untitled-1](https://user-images.githubusercontent.com/45502375/221382579-d99c735a-3e95-47ec-bb48-697a9cfaaf8b.png)
