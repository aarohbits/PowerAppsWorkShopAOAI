#02 PowerApps & Azure OpenAI with Different Actions within Davinci



# 02 Azure Open AI (GPT) with Power Apps

In this example you will able to use Power Apps as front end for end users to ask question, then call Power Automate for Azure OpenAI service, the request come back to Power Automate and then anwer shown to end user. 

This is inspired by this blogpost [Build a Power App to create Demo or Personal Knowledge Bot](https://techcommunity.microsoft.com/t5/ai-machine-learning-blog/azure-open-ai-gpt-with-power-apps-build-a-power-app-to-create/ba-p/3730864)

## STEP 1 

- Create a new Power Apps Canvas App
- Select Tablet format 
- Add different controls such as 
  - Textbox
  - Text labels 
  - Buttons as follows:
 
   ![01 Canvas App controls](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/dc570a40-d8a7-4f7d-bf3d-fdeb249be8f9)


## Step 2

Add a new flow from Cavas apps 
![02 Create new flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/416a6b82-9038-4eb0-b8f7-4b9c3deba32a)



## Step 3

Add new blank flow


## Step 4

Rename the flow, add new step, add new HTTP action and set to post 

![03 Rename, HTTP Action, POST](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/fd09936c-dd51-4c8b-b893-06fd1d4988f0)

## Step 5 

Nagivate to the Azure portal, under playground select Compleltions >> Select Question answring >> select the View code 

![04 Az Open AI - Competions - Questions - View Code](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/99a7c2b6-9922-4f68-a60d-8caf4b9c2af5)


## Step 6

Copy the Endpoint and Key from Azure OpenAI service 

![05 View Code](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/2cd52351-1d13-4883-b330-31e81c688b18)


## Step 7 

Copy the URL to URI at Power Automate and for key type in api-key amd paste the key 

![06 HTTP Copy](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/551d396c-b5cf-4755-acb3-add7cd7bf5ac)

## Step 8 

For Body of HTTP, you need a craft JSON content from [Azure OpenAI API refrence](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/reference).


~~~
{
  "prompt": "",
  "max_tokens": 200,
  "temperature": 0,
  "top_p": 1,
  "frequency_penalty": 0
}

~~~

For getting the question from PowerApps, **double click** on Ask in PowerApps within prompt
![07 Ask In PowerApps](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/be46e497-9ad1-435b-b617-9ba3d71e6a97)


![08 Ask In PowerApps ](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/84084e60-a7e7-4841-b315-11e8c05e9e8f)



## Step 09 

In next step, search for **compose** message >> select the **Add dynamic content** >> Under HTTP heading select Body 

![11 Compose Body](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/996d82b3-37f9-46c9-b371-0cdeabdf7199)


![12 Compose Body](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/9f0b6713-ad11-4784-8fc6-63359d286a9a)

## Step 10 


At the Canvas App, create a global variable and trigger the flow as follows

```
Set(gOpenAIText, '16JunePPAzireOpenAIFlow'.Run(txtQuestion.Text))
```

![11 Canvas App FLow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/170b73d7-9f13-4e66-8b8e-6e6f93906e71)

and run the Power App


![11 Canvas App FLow 2](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/aa7d9937-463b-4910-a647-43506f7777f4)


## Step 12


Once the flow is successful, copy the output JSON to a text file that you will use in upcoming steps 

~~~
{
  "id": "cmpl-7S9Cbnovtz5bYPzna5TK8dW7gnZV7",
  "object": "text_completion",
  "created": 1686942913,
  "model": "text-davinci-003",
  "choices": [
    {
      "text": "\n\nPower Apps is a powerful and easy-to-use platform for creating custom business applications. It is a low-code platform that enables users to quickly create applications without the need for coding. It is a great tool for businesses to quickly create applications that can be used to automate processes, improve customer service, and increase efficiency. Power Apps is also popular because it is cloud-based, meaning that applications can be accessed from anywhere with an internet connection. Additionally, Power Apps integrates with other Microsoft products, such as Office 365, Dynamics 365, and Azure, making it easy to create applications that are connected to existing data sources.",
      "index": 0,
      "finish_reason": "stop",
      "logprobs": null
    }
  ],
  "usage": {
    "completion_tokens": 127,
    "prompt_tokens": 6,
    "total_tokens": 133
  }
}
~~~

![12 Flow Run'](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/912de84f-9ad3-417a-b22d-9742173ec2ab)

![10 Compose Body 2](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/68dc00d4-1f72-4231-95f5-2ab033ec70b3)


## Step 13 

Edit the flow 
![13 Edit Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/a5dc3afb-e85e-4e57-a1eb-3583d7985fed)

