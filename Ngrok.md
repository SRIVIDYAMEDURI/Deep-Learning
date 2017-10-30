# Development and Testing with Ngrok
 
## 1.	Objectives
 
With Microsoft Bot Framework, to configure the bot to be available to a particular channel, you will need to host the Bot service on a public URL endpoint. The channel won’t be able to access your bot service if it is on a local server port hidden behind a NAT or firewall.
  
When designing / building / testing your code you don’t always want to have to keep redeploying. This will result in additional hosting costs. This is where ngrok can really help in speeding up the development/testing phases of bots. The goal of this lab is to use ngrok to expose your bot to public internet and use the public endpoints to test your bots in the emulator.
  
## 2.	Setup
  
1.	If you do not have ngrok installed, download ngrok from https://ngrok.com/download and install for your OS
2.	Open any Bot project (from the previous labs) in Visual Studio and run it. If you are using EchoBot, you should be seeing the below message in the browser:

EchoBot

Describe your bot here and your terms of use etc.

Visit Bot Framework to register your bot. When you register it, remember to set your bot's endpoint to

## 3.	Forwarding

1.	Given the bot is being hosted on localhost:3979, we can use ngrok to expose this port to the public internet
2.	Open terminal and go to the folder where ngrok is installed
3.	Run the below command and you should see the forwarding url:

````ngrok.exe http 3979 -host-header="localhost:3979"````

![Forwarding Url](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/ForwardingUrl.png)

4.	To use public urls in the bot emulator, you will also need to generate a forwarding url using ngrok for Emulator url (port 9000). Run the below command and you should see the forwarding url for port 9000:

````ngrok.exe http -host-header=rewrite 9000````

![Emulator Url](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/EmulatorUrl.png)

5.	Enter the forwarded urls in the bot emulator (bot url and emulator url). The bot url will have /api/messages appended to the forwarding url. Test the bot in the emulator by sending messages.

![Bot Url](https://github.com/SRIVIDYAMEDURI/Deep-Learning/blob/master/images/BotUrl.png)

## 4.	Exercise

1.	When you register the bot on the Microsoft Bot Framework, can you use the forwarding url for the Messaging Endpoint?
2.	Test the bot on a channel using the forwarding URL on a channel.


