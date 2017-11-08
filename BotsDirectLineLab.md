# Developing and Deploying Intelligent Chat Bots

# Connect directly to a Bot  - Direct Line

## Objectives

In certain scenarios such as testing, communication directly to your bot may be required. Communication between your bot and your own client application can be performed using Direct Line API. This hands-on lab introduces key concepts related to Direct Line API.

## Setup

For this lab, you can use a published Bot to talk to via Direct Line API. 

Download the sample from:
https://github.com/Microsoft/BotBuilder-Samples/tree/master/CSharp/core-DirectLine and import the solution in Visual Studio.

In the DirectLineBot solution, you will find two projects – DirectLineBot and DirectLineSampleClient. If you do not have a published app, you can publish DirectLineBot. The previous labs should have prepared you with the steps related to publishing bots. 

DirectLineSampleClient is the client that will send messages to the bot.

## Authentication

Direct Line API requests can be authenticated either by using a secret that you obtain from the Direct Line channel configuration page in the Bot Framework Portal. Go to the Bot Framework Portal and find your bot. Add Direct Line via *Connect to channels* for your bot.

![Connect to channels]()

You can obtain a Secret Key from the Direct Line channel after adding as shown below:

![Direct Line]()

**Security Scope**

Secret Key: Secret key is application wide and is embedded in the client application. Every conversation that is initiated by the application would use the same secret. This makes it very convenient.

Tokens: A token is conversation specific. You request a token using that secret and you can initiate a conversation with that token. Its valid for 30 minutes from when it’s issued but it can be refreshed.

## App Config

The Secret key obtained from *Configure Direct Line* in the Bot Framework Portal is then added to the Configuration settings in App.config file as shown below. In addition, for the published bot, capture the bot id and enter in the appSettings part of App.config from DirectLineSampleClient project. The relevant lines of App.config to enter in the App.config are listed as follows:

````
<add key="DirectLineSecret" value="YourBotDirectLineSecret" />
<add key="BotId" value="YourBotId" />

````

## Sending and Receiving Messages

Using Direct Line API, a client can send messages to your bot by issuing HTTP Post requests. A client can receive messages from your bot either via WebSocket stream or by issuing HTTP GET requests.

![Configuration]()

In this lab, we will explore HTTP Get option to receive messages.

1.	Run project DirectLineSampleClient after making the Config changes.

2.	Submit a message via console and obtain the conversation id using the below line:

````Console.WriteLine("Conversation ID:" + conversation.ConversationId);````

![Console]()

3.	Once you have the conversation id, you can retrieve user and bot messages using HTTP Get. To retrieve messages for a specific conversation, you can issue a GET request to 
https://directline.botframework.com/api/conversations/{conversationId}/messages endpoint. You will also need to pass the Secret Key as part of raw header (i.e. Authorization: Bearer {secretKey}).

4.	Use any Rest Client to receive messages via HTTP Get. In this lab, https://advancedrestclient.com/ is used for receiving messages from the bot. The below images indicate the conversations obtained from Advanced Rest client. Note the conversation “Hi there” and the corresponding bot response that is echoed back.

![HTTPRequest]

![HTTPRequest1]


