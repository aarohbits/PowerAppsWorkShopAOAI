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


## Step 14 

In next step search for Parse JSON, rename the action, select the Add dynamic content and select body

![16 Parse JSON](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/82cddbde-6e9b-4973-9278-42a29991cd9f)

![17 HTTP Rename Action](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/29a2d600-6ebe-46ef-9227-baa7ad276725)

![18 Parse JSON Body](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/40f56a61-68db-428a-9828-7c4c07005c43)




## Step 15

Now, paste the JSON the content that you copied at Step 12 as follows


![19 Parse JSON Reanme Paste JSON](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/1397c29e-a644-4816-aa0a-c95358c02b98)


## Step 16 

In next step, create a new varibale, initialize varibale called outsummary with string data datatype


![20 Init Var outsummary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/bf3aea0e-eedc-4325-a04f-6945ddfcd2ad)


## Step 17

In next step, search of **apply to each** control, select **Add dynamic content** and select **choices** from Parse JSON from above steps

![21 Apply to each](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/7d5ccc70-1395-487b-adf8-0edc4a378d4a)


![22 Apply to each - Choices](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/109f7516-a713-4506-b377-e783054c2f44)

## Step 18 

Within apply to each control, select a **set variable** and in the value property set the **Current item**

![22 Apply to each - Current Item](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/6ef6309c-ef7e-4404-b7fb-5fc3cbc6194f)


## Step 19 

Go back to Canvas app, select the flow

![19 Parse JSON Reanme Paste JSON](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/e5deb8ce-3dbc-47f4-b10f-1ff4b2c9319f)


## Step 20

Type a question in textbox and cilck on **Summarize Text** button 


![24 Canvas App - Run the flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/70c040eb-6a31-4f00-98b2-f642a1e374c6)


## Step 21

Click on the flow link 

![25 Click on flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/8ac78c92-ff7c-4be5-b9c2-1acee575a8cf)



## Step 22 

Copy the output JSON from compose to a text file. You will use in next step

![26 Copy the Output Compose](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/49e3d949-df1a-43ac-b5df-3e3c1aaeb0d8)


## Step 23 

Edit the flow 

![27 Edit Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/411aecec-6e1f-4ce7-a859-3bcd8b0418bc)


## Step 24  

In Next Step, search for **Parse JSON action**, select **Add dynamic content** and use outsummary variable

![28 Parse JSON Output summary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/2aa540ee-dfc8-4f16-91c2-34e22c0d1bdb)




## Step 25 

Click on **Generate from Sample** button 


![29 Parse JSON  Generate Sample](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/565e78eb-2a57-489f-938d-1552626df104)

## Step 26 

Paste the JSON content that you copied from Step 22

![30 Paste JSON cONTENT FROM previois step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f105f380-19a3-40ae-a783-af19e476ede5)


![31 Paste JSON cONTENT FROM previois step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/0e0bc93f-ad2d-44e9-9454-8c0ce2caf476)

## Step 27

In next step, search for **Respond to a PowerApp or flow** action

![32 Respond to Poweer Apps  or flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/d673d3b3-7aaf-4339-b2b2-52b9657dec83)


## Step 28 

Add text input variable called **response** and use **text**

from Parse JSON
![33 Output Summary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/a6f5941a-84e8-4309-b031-f899da8cd505)



## Step 29 

Save the flow

![33 Save flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/fa25242c-9446-4840-9ead-0ce78242220f)


## Step 30 


Back to Power Apps, 

a) Set the response variable at the **Summarize Text** Button

![39 - Summarize Text](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/d1c07d51-6075-41ac-b994-cfde95e9d8fd)


b) Set the response variable at the **SQL** Button

![40 SQL](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/77f479fa-76fe-472c-a5cd-388ecdb6d0fc)


c) Set the response variable at the **Classify Text** Button

![41 Classify ](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/77746ea7-ffb0-4a98-885b-184dfefee3bb)


d) Set the response variable at the **Parsed Unstructured** Button 


![42 Unstrcuted](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f49e1e56-532a-48b7-a0ff-2d965078f19d)

e) Set the response variable at the **Classify** Button

![43 Classfiy](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/d33aa772-f1b4-442f-b6d3-800d0c51568c)



## Step  31 

Assign gOutput the label control


![36 Final Output](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/6e61d0d2-ad4c-4e96-8024-eb69132e7327)


## Step 32

Run the Power Apps, ask question, click on buttons and anwser is shown at output label

![50 Final Summarize](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/dad2a248-ec2f-4779-8ce9-15b206ef0dc5)

![51 Final SQL](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/bc9b633c-320c-4b8e-a5c9-32a5fa3a50e9)

![52  Final Classify Text](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/8747b417-e950-4d43-96c5-7ef4abefa3fe)


![53 Unstsrcu](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/519ab059-bbff-4ff7-84f0-67f627e35b69)

![54 Classify](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/bcf6f7ac-ccf6-420d-9126-382468cf9f70)





