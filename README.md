# Chat GPT-3 AI with Blip chat
<div align="center">  
  
![Logo](https://1000logos.net/wp-content/uploads/2023/02/ChatGPT-Logo.png "Open AI")
  
</div>

## Description

<p align="center">
<img src="src/assets/finalGIFGPT.gif">
</p>

This is a simple example of a conversational flow in which the GPT chat AI creates the phrases that will be shown to the user based on the context of the user's input. And when it is noticed that the user wants to see the photos of the product, the bot shows a carousel with the catalog of images.

This is an example of how to use **GPT-3 chat** with the **Blip chat framework**.
To install and run, follow the steps below:

# Step by step
* Create an account on https://openai.com/
* After creating your account and logging in, **click** on "**Upgrade**" in the upper right corner
* Create your API Key. **Click** on [API Keys](https://platform.openai.com/account/api-keys) 
* Click in **+ Create new secret key** and then copy the key

<p align="center">
<img src="src/assets/copyKey.PNG">
</p>

***Your key will look like this:***

**Api key** 👉 *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* 🔑

* Create a chat from scratch on the Take **Blip platform** and then open the **Blip builder** and click on **settings**.

<p align="center">
<img src="src/assets/config.PNG">
</p>

*Still in configuration click on **variables** and then on **configuration variables**. Click in **+ Add extra information***.

<p align="center">
<img src="src/assets/configextra.PNG">
</p>

*In configuration variables, create **environment variables**.*
*For it to work correctly in the flow that we will upload, the variables must have the same names as in the example below:*

**apiKey** = *Put as value the **api key** you copied* 🔑

**urlGpt3** = *https://api.openai.com/v1/completions*

**urlGpt3Images** = *https://api.openai.com/v1/images/generations*

<p align="center">
<img src="src/assets/enviroment.PNG">
</p>

# Install

Go to the [chatbot](https://github.com/cristiano-muroni/ChatGPTandBLIP/tree/main/chatbot) folder of this repository, download the flow in JSON.

After that, go back to the **builder** and go to **configurations** and then to **versions** and then click on **Upload flow** and select the JSON.

<p align="center">
<img src="src/assets/upload.PNG">
</p>


* Once uploaded, click on "Publish flow".
Then go to "Channels" and select "Blip Chat", then "Setup" and then click on "avalaible here", this is the link of your published bot.

<p align="center">
<img src="src/assets/channelsetup.PNG">
</p>

