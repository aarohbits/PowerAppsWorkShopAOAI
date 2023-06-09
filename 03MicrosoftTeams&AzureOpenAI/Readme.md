# 03 Teams Bot with Azure OpenAI

In this example, user will ask question within Teams, Power Automate calls Azure OpenAI, Azure OpenAI's text-davinci-003 model is executed and question is answered within Teams. 

## Step 1 

From Solution, Select New >> Automation >> Cloud Flow >> Automated 

![01 Automated Teams Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/6a133c6b-e455-4207-a146-1dadc61cda6a)



## Step 2

Name the flow, select **when a new channel message** from the flow trigger, click in **Create**

![02 When new channel is added](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/e9daf679-2db3-46da-90e0-4a81b795181b)


## Step 3

Select a **Team** and **Channel**

![03 TEams and Channel](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/010d0ba0-742f-4ec6-8923-49d98617f387)


# Step 4 

Rename the flow, add new step, add new HTTP action and set to post 

![04 Rename flow  - HTTP - Post](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/1dd7a5cf-7535-41dc-adff-b4eb1ec2c2e8)


# Step 7 

Nagivate to the Azure portal, under playground select **Compleltions** >> Select **Question answring** >> select the **View code**


![07 Az Open AI - Competions - Questions - View Code](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/4be798ee-1063-4f6a-8b41-147e2f4245e5)

# Step 8

Copy the Endpoint and Key from Azure OpenAI service

![08 View Code](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f1c4ec94-af8e-4aec-8b28-c49e28defebd)


# Step 9


- Copy the URL to URI at Power Automate
- For key type in **api-kpi** amd paste the key
- Craft JSON content for the Body. 

For Body of HTTP, you need a craft JSON content from [Azure OpenAI API refrence](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/reference). 


```
{
  "prompt": "@{triggerOutputs()?['body/body']}",
  "max_tokens": 200,
  "temperature": 0
}

```

![07 HTTP Copy](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/d08e5aaf-3e9b-4c61-ba33-5f9a38f5aeeb)



# Step 11 

In next step, search for **compose** message >> select the **Add dynamic content** >> Under HTTP heading select Body  >> Click on Save button. 

![09 Compose Body](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/c73e873a-56fe-4a6f-a79f-6bd93d88c8d1)


# Step 12  


a) Test the flow

![15 Test Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f0841b51-dd9b-4d7a-a5f5-cffbe03066ea)

b) Perform Manual Test

![15 Test Flow 2](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/25b0d289-508f-4daa-bd50-1ca771c4dc7a)

c) Add a new message to the channel 

![15 Test Flow 3](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/48f91299-28b0-4517-a313-6f666a063cde)

# Step 13 

Type a question in Teams channel (within OpenAI messages) 

![16 Teams Message](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f0aeba42-dac5-45b6-af40-97d127515981)

# Step 14 

Test the flow 



 ![17 Flow Test](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/91f916ed-bfbf-4608-9f44-9b3bd3e6f62e)

 Test within Teams 

 
![18 Teams message](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/af8786f1-7b1f-495e-9007-10d3437d4cbb)


# Step 13 

Once the flow is successful, **copy the output JSON to a text file** that you will use in upcoming steps

~~~
{
    "type": "object",
    "properties": {
        "id": {
            "type": "string"
        },
        "object": {
            "type": "string"
        },
        "created": {
            "type": "integer"
        },
        "model": {
            "type": "string"
        },
        "choices": {
            "type": "array",
            "items": {
                "type": "object",
                "properties": {
                    "text": {
                        "type": "string"
                    },
                    "index": {
                        "type": "integer"
                    },
                    "finish_reason": {
                        "type": "string"
                    },
                    "logprobs": {}
                },
                "required": [
                    "text",
                    "index",
                    "finish_reason",
                    "logprobs"
                ]
            }
        },
        "usage": {
            "type": "object",
            "properties": {
                "completion_tokens": {
                    "type": "integer"
                },
                "prompt_tokens": {
                    "type": "integer"
                },
                "total_tokens": {
                    "type": "integer"
                }
            }
        }
    }
}
~~~


![14 Compose Output JSON](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f1e8385c-37af-4ac1-92ea-99474679bd1a)


# Step 13 

Edit the flow

![15 Edit Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/742cdd96-e61a-47b9-b1a5-bd29c8c77849)


# Step 14

in next step search for Parse JSON, rename the action, select the **Add dynamic content** and select **body**

![22 Parse JSON 1](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/14f3f640-fce5-4579-94f1-45f3580fe0e5)


![23 Parse JSON - Generte from Sample](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/eba3b962-a11b-43bd-a0fb-292c27d32106)



![24 Parse JSON - Generte from Sample PASTE JSON ](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/0f77561a-10d0-468c-b14d-4b7cfffb8e15)



![25 Parsse JSON NExt Step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/c29327a9-df58-4e0d-89b8-7bd732d2676a)


# Step 15 

In next step, create a new varibale, initialize varibale called **outsummary** with string data datatype

![20 Init Var outsummary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f051c8f2-2bea-4e0f-bd4d-12883ad5a3f9)


# Step 17 

In next step, search of **apply to each** control, select **Add dynamic content** and select **choices** from Parse JSON from above steps

![21 Apply to each](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/08b8ef7d-0d69-4296-9fb5-a85a56ba5eee)



# Step 18 
Within **apply to each** control, select a set variable and in the value property set the **Current item** 

![22 Apply to each - Current Item](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/ba9c2910-3bbe-41df-b9a1-36558428d21b)


# Step 19 

Click on runnning flow 

![19 run of flow run](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/897d65d2-bc66-42c0-8bce-8989389ed068)


# Step 20

Copy the output JSON from compose to a text file. You will use in next step

~~~
{
    "text": "\n\nPower Platform governance is critical because it helps ensure that the platform is used in a secure, compliant, and efficient manner. It also helps ensure that the platform is used in a way that meets the organization's business objectives. Governance helps ensure that the platform is used in a way that is consistent with the organization's policies and procedures, and that it is used in a way that is compliant with applicable laws and regulations. Additionally, governance helps ensure that the platform is used in a way that is cost-effective and that it is used in a way that maximizes the value of the platform for the organization.",
    "index": 0,
    "finish_reason": "stop",
    "logprobs": null
  }
~~~


![20 Copy Output from Compose Message](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/26b9eb19-1637-4124-8e8c-37c6ebad6e56)


# Step 21 

Edit the flow 


![21 Edit Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/3669d08f-16cd-41cf-8281-ff6ac47f7841)



# Step 22 

In next step, search of Parse JSON, select **outsummary**, click on **Generate from Sample**

![22 Parse JSON 1](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/880f0c4b-cbf2-4b67-a5e6-1c9e8bfb9faa)

# Step 23 

Paste the JSON content that you copied from Step 20 


![24 Parse JSON - Generte from Sample PASTE JSON ](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/34a30db2-03c0-43dc-b55f-e8b45e87a19a)

![25 Parsse JSON NExt Step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/c8eec182-0116-4f48-bf8b-661d6e22c956)


# Step 24 

In Next Step, search for Parse JSON action, select **Add dynamic content** and use outsummary variable 
![28 Parse JSON Output summary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f40bfc52-356b-4cbe-9bd7-2936c52fabd9)


# Step 25 

Click on **Generate from Sample** button

![29 Parse JSON  Generate Sample](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/ad47ef47-444e-409b-83c1-2dbb19ea52d1)


# Step 26

Paste the JSON content that you copied from Step 22 


~~~
{
    "text": "\n\nPower Apps help with digital transformation by providing a platform for businesses to quickly and easily create custom applications that can be used to automate processes, streamline operations, and improve customer experiences. Power Apps can be used to create applications that can be used to capture data, automate processes, and integrate with other systems. This helps businesses to quickly and easily create applications that can be used to improve customer experiences, increase efficiency, and reduce costs. Additionally, Power Apps can be used to create applications that can be used to create custom reports, dashboards, and analytics. This helps businesses to gain insights into their operations and make better decisions.",
    "index": 0,
    "finish_reason": "stop",
    "logprobs": null
  }
~~~

![30 Paste JSON cONTENT FROM previois step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/b97fb88c-e375-4215-bb09-8c3fbf8f89d1)

![31 Paste JSON cONTENT FROM previois step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/3400435a-e8ee-42c9-92d2-b52708e27d37)

# Step 27 
In next step, search for **Reply with a message in a channel** 

![32 Respond to Poweer Apps  or flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/38b2c7d1-4fa5-4d5e-96c1-1217045c54b3)

![30 Reply with a message in a channel](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f9eeaf05-44b2-4cb3-a19c-10c0527a1460)

# Step 28

From **Add dynamic content** 
- search for **Message id**
- Select Team
- Select Channel
- Select **text** from Message

![31 Message text](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/612186e4-070a-4dc6-b5c4-d1a009ae3203)


# Step 29

Save the flow

![32 Save flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/60044cc3-c865-4a73-ba7f-4f4aa0134c60)

# Step 30

Create a  **New Conversation** within **OpenAI messages** in Teams


![33 Test Message in Teams](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/7047fc32-1ff6-4758-a1a8-75fd22bd20cd)


# Step 31

After few seconds, a new messages shows up from Azure OpenAI. 


![34 Teams Message](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/a12510b1-a7ee-4ad1-8454-2c335481f5e9)











