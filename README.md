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

# Open AI API information

## Authentication

<p align="center">
<img src="src/assets/auth.PNG">
</p>

[Auth docs](https://platform.openai.com/docs/api-reference/authentication)

## Requests for the completions service

```
POST https://api.openai.com/v1/completions
```

*Body*
```
{
  "model": "text-davinci-003",
  "prompt": "Say this is a test",
  "max_tokens": 7,
  "temperature": 0,
  "top_p": 1,
  "n": 1,
  "stream": false,
  "logprobs": null,
  "stop": "\n"
}
```
*Response*
```
{
  "id": "cmpl-uqkvlQyYK7bGYrRHQ0eXlWi7",
  "object": "text_completion",
  "created": 1589478378,
  "model": "text-davinci-003",
  "choices": [
    {
      "text": "\n\nThis is indeed a test",
      "index": 0,
      "logprobs": null,
      "finish_reason": "length"
    }
  ],
  "usage": {
    "prompt_tokens": 5,
    "completion_tokens": 7,
    "total_tokens": 12
  }
}
```

<p align="center">
<img src="src/assets/complet.PNG">
</p>

[Completions docs](https://platform.openai.com/docs/api-reference/chat/create)

## Requests for the create images service

```
POST https://api.openai.com/v1/images/generations
```
*Parameters*
```
{
  "prompt": "A cute baby sea otter",
  "n": 2,
  "size": "1024x1024"
}
```
*Response*
```
{
  "created": 1589478378,
  "data": [
    {
      "url": "https://..."
    },
    {
      "url": "https://..."
    }
  ]
}
```
[Create image docs](https://platform.openai.com/docs/api-reference/images/create)

## Request headers

Key                | Value
------------------ | ------------------
Authorization      | Bearer {your key}
Content-Type       | application/json
                   |

# Builder Blip Chat

## SET prompt
```
function run(prompt, TypeClothes, gender, color, meshClothes, description, complement, price, size) {
    const prompt = `Considere a descrição do seguinte produto.

    Tipo: ${TypeClothes}
    Gênero: ${gender}
    Cor: ${color}
    Malha: ${meshClothes}     
    Tamanhos: ${size}
    Descrição: ${description}
    Composição: poliester ou a base de algodão.
    Complemento: ${complement}
    Preço: ${price}
    Agora, baseado exclusivamente nas informações acima, responda a seguinte pergunta do cliente.
    Pergunta:`
    return prompt; 
};
```
## SET payload
```
function run(prompt, askTheUser) {
    const payload = {
        "model": "text-davinci-003",
        "prompt": `${prompt} ${askTheUser}`,
        "temperature": 0.9,
        "top_p": 0.9,
        "frequency_penalty": 1,
        "presence_penalty": 1,
        "best_of": 2,
        "max_tokens": 256,
        "stop": null
    };
return JSON.stringify(payload);
}
```
## HTTP request to GPT-3 API

Method               | Value
-------------------- | --------------------
POST                 | {{config.urlGpt3}}

*Headers*
Key                    | Value
---------------------- | ----------------------
Authorization          | Bearer {{config.apiKey}}
Content-Type           | application/json

*Body*
```
{{payload}}
```
*Save return*

Response status variable   | Response body variable 
-------------------------- | --------------------------
statusGptApi               | responseGptApi


*Filter Response*
```
function run(statusGptApi, responseGptApi) {
    if (statusGptApi == 200) {
        const item = JSON.parse(responseGptApi);
        const resp = item.choices[0].text;
        return resp;
    }
    return "Algo deu errado, tente novamente";
};
```
## Request for the chat service to create images

*SET prompt*
```
function run(askTheUser, gender, color) {
    const promptImage = `${askTheUser} ${gender} ${color}`;
    return promptImage;
};
// save the return variable as "promptImage"
```

Method               | Value
-------------------- | --------------------
POST                 | {{config.urlGpt3Images}}

*Headers*
Key                    | Value
---------------------- | ----------------------
Authorization          | Bearer {{config.apiKey}}
Content-Type           | application/json

*Body*
```
 {
    "prompt": "{{promptImage}}",
    "n": 10,
    "size": "1024x1024"
 }
```
*Save return*

Response status variable   | Response body variable 
-------------------------- | --------------------------
statusGptImagesApi         | responseGptImagesApi


*Filter Response*
```
function run(responseGptImagesApi, TypeClothes) {
    responseGptImagesApi = JSON.parse(responseGptImagesApi);
    const { data } = responseGptImagesApi;
    let itens =[];
   data.forEach((event) => {

       itens.push({
           "header": {
               "type": "application/vnd.lime.media-link+json",
               "value": {
                   "title": TypeClothes,
                   "text": "Description",
                   "type": "image/jpg",
                   "uri": event.url
               }
           },
           "options": [
                {
                    "label": {
                        "type": "application/vnd.lime.web-link+json",
                        "value": {
                            "title": "Comprar",
                            "uri": "https://...",

                        }
                    }
                }
            ]
          
       });
   });

   return {
       itemType: "application/vnd.lime.document-select+json",
       items: itens
   };

}
```




