![Example-Logo](https://media.discordapp.net/attachments/457174919944339458/458404230601113620/twitter_header.png)
# NextON Masternode Setup Guide (Ubuntu 16.04)
***
## Required
1) **50000 NextON coins**
2) **Local Wallet (Cold) https://github.com/Next-ON/NextON/releases**
3) **VPS with UBUNTU 16.04 [https://www.vultr.com](https://www.vultr.com/?ref=7465341)**
4) **Putty https://www.putty.org/**
5) **Text editor on your local pc to save data for copy/paste**
***

***On your cold wallet***
* Create an address with a label MN1 and send exactly 50000 NXTON to it. Wait to complete 6 confirmations on “ Payment to yourself “ created.

* Open the Debug Console ( Tools – Debug Console ) and type ***masternode genkey***.
You will then receive your private key, save it in a txt to use it later.
  ```
  Exemple:
          masternode genkey
          w8723KqiiqtiLH6y2ktjfwzuSrNucGAbagpmTmCn1KnNEeQTJKf
* Still at Debug Console type ***masternode outputs*** and save txhash and outputidx on a txt
  ```
  Exemple:
          "txhash" : "12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa",
		         "outputidx" : 0
***
***On Putty***

* Once logged in your vps, *copy/past* each line one by one with *Enter*

	:arrow_forward: `wget https://github.com/Next-ON/NextON/releases/download/0.0.1/Linux_X64.tar`

	:arrow_forward: `tar -zxvf ./Linux_X64.ta`

	:arrow_forward: `cd Linux_X64/`

	:arrow_forward: `./nxtond`

	Previous command will return you a warning message where you can find info similar to this:

		rpcuser=nxtonrpc
		rpcpassword=6fDot74g2YzvaGDfnGEqKUidhw27yf9rh2iS4uaXqa345

	Save rpcuser and rpcpassword you got in warning message in a txt. You will need it in next step

	:arrow_forward: `nano /root/.NXTON/nxton.conf`

	It will open a text editor in your VPS where you need to paste the following:
	(just change what’s between ** to your personal information)

	```
	rpcallowip=127.0.0.1
	rpcuser=**THE ONE YOU SAVED BEFORE**
  	rpcpassword=**THE ONE YOU SAVED BEFORE**
	server=1
	daemon=1
	logtimestamps=1
	maxconnections=256
	masternode=1
	externalip=**YOUR VPS IP**
	masternodeprivkey=**MASTERNODE_PRIVATE_KEY**
	```
	When you finish just press CTRL + X and then hit Y follow by ENTER

	:arrow_forward: `./nxtond`

	Leave the putty open for now
***
***Go back to your cold wallet***

* Open the Masternode Configuration file (tools – open masternode configuration file) and add a new line (without #) using this template (bold needs to be changed) in the final save it and close the editor

**ALIAS VPS_IP**:32698 **masternodeprivkey TXhash Output**

		Exemple:
		MN1 125.67.32.10:32698 w8723KqiiqtiLH6y2ktjfwzuSrNucGAbagpmTmCn1KnNEeQTJKf
		12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa 0

* Close and Re-open cold Wallet and at Masternode Tab you will find your MN with status MISSING

***(For the next steps you need to have already 21 confirmation on “Payment to yourself “ created in first step)***

* At Masternode Tab choose the Masternode with the status MISSING and press “ Start Alias “.
	(You will get an error, it’s suppose to)

* Go to Debug Console type the following: ***startmasternode alias false (mymnalias)***

		Exemple:
		startmasternode alias false MN1

***
***Go back to Putty***

   :arrow_forward: `./nxton-cli startmasternode local false`

You will get the message “ Masternode successfully started “

At this point if all correct you will get your Masternode Running, to double check it in Putty type:

   :arrow_forward: `./nxton-cli masternode status`

You need to get **"status" : 4**

## Congratulations your NextON node it's running
