# Chat GPT-3 AI with Blip chat
<div align="center">  
  
![Logo](https://1000logos.net/wp-content/uploads/2023/02/ChatGPT-Logo.png "Open AI")
  
</div>

## Description

<p align="center">
<img src="src/assets/finalGIFGPT.gif">
</p>

This is an example of how to use **GPT-3 chat** with the **Blip chat framework**.
To install and run, follow the steps below:

# Step by step
* create an account on https://openai.com/
* After creating your account and logging in, **click** on "**Upgrade**" in the upper right corner
* Create your API Key. **Click** on [API Keys](https://platform.openai.com/account/api-keys) 
* Click in **+ Create new secret key** and then copy the key

<p align="center">
<img src="src/assets/copyKey.PNG">
</p>

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

**apiKey** = *Put as value the **api key** you copied*

**urlGpt3** = *https://api.openai.com/v1/completions*

**urlGpt3Images** = *https://api.openai.com/v1/images/generations*

<p align="center">
<img src="src/assets/enviroment.PNG">
</p>

