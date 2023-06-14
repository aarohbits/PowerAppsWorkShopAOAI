# 01 Simple Power Apps with Azure OpenAI Sample

In this example you will able to use Power Apps as front end for end users to ask question, then call Power Automate for Azure OpenAI service, the request come back to Power Automate and then anwer shown to end user. 

## STEP 1 

Create an app and selecte a Canvas App 

![01CanvasApp](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/c5db6ef3-0528-420b-b2a2-1218f862336d)


## Step 2

Create app from blank 

![02 Tablet](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/2487ba6b-1683-42ed-a977-d4e3f9ac8aae)


## Step 3 

Please 3 controls 

- Textbox
- Button
- Label 


![03 Place 3 Controls](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/0b24374d-8a38-4691-8ce7-63a8efd693fa)

# Step 4 

Add a new flow from Cavas apps 


![04 Add Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/328268e9-e4c8-46bd-8b16-c3a335684fbb)


# Step 5 

Add new blank flow 

![05 Add Blank Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/67d61559-ba7f-472d-aeea-81b5a9c6f756)


# Step 6 

Rename the flow, add new step, add new HTTP action and set to post 

![06 Rename flow  - HTTP - Post](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/d185070a-8670-4207-9054-f3f8e1b5a5bb)


# Step 7 

Nagivate to the Azure portal, under playground select **Compleltions** >> Select **Question answring** >> select the **View code**


![07 Az Open AI - Competions - Questions - View Code](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/4be798ee-1063-4f6a-8b41-147e2f4245e5)

# Step 8

Copy the Endpoint and Key from Azure OpenAI service

![08 View Code](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f1c4ec94-af8e-4aec-8b28-c49e28defebd)


# Step 9

Copy the URL to URI at Power Automate
and for key type in **api-kpi** amd paste the key 

![09 HTTP Copy](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/51a0fd77-34cf-4992-b1dd-147a8b63e80e)

# Step 10 

For Body of HTTP, you need a craft JSON content from [Azure OpenAI API refrence](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/reference). 


```
{
  "prompt": "",
  "max_tokens": 200,
  "temperature": 0,
  "top_p": 1,
  "frequency_penalty": 0
}

```

For getting the question from PowerApps, double click on **Ask in PowerApps** within **prompt**

![10 Ask In PowerApps](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/92742cb8-7e7f-46af-b00f-91115619b7fa)


![10 Ask In PowerApps 2](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/e81ad777-798c-4e6c-8420-541214a950e8)



# Step 11 

In next step, search for **compose** message >> select the **Add dynamic content** >> Under HTTP heading select Body 

![11 Compose Body](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/996d82b3-37f9-46c9-b371-0cdeabdf7199)


![12 Compose Body](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/9f0b6713-ad11-4784-8fc6-63359d286a9a)

# Step 12  


At the Canvas App, create a global variable and trigger the flow as follows

```
Set(gOutout,'13JunePPAzOpenAI'.Run(txtQuestion.Text))
```

Run the Power Apps 

![13 Button Run Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/6d7dd46a-a9da-4bc4-be51-cd6c71b0a983)

 

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

![16 Parse JSON](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/ba3c7eb8-0bb1-49b5-bdda-62dd9db4f1d8)


![17 HTTP Rename Action](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/e64a15e9-09d0-4a10-8271-cf94ee8f63a4)


![18 Parse JSON Body](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/a3230873-5909-4a8b-b87e-372d2557ea60)

# Step 15 

Now, paste the JSON the content that you copied at **Step 13**  as follows


![19 Parse JSON Reanme Paste JSON](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/c8350660-bb26-463b-8ff1-6c2e9ab76dd9)


# Step 16 

In next step, create a new varibale, initialize varibale called **outsummary** with string data datatype

![20 Init Var outsummary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f051c8f2-2bea-4e0f-bd4d-12883ad5a3f9)


# Step 17 

In next step, search of **apply to each** control, select **Add dynamic content** and select **choices** from Parse JSON from above steps

![21 Apply to each](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/08b8ef7d-0d69-4296-9fb5-a85a56ba5eee)



# Step 18 
Within **apply to each** control, select a set variable and in the value property set the **Current item** 

![22 Apply to each - Current Item](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/ba9c2910-3bbe-41df-b9a1-36558428d21b)


# Step 19 

Go back to Canvas app, select the flow 

![23 Canvas App - Refresh PA](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/055f29c5-b0c6-4c5c-89cc-ca9c7ba0fa06)


# Step 20

Type a question in textbox and cilck on Submit button 

![24 Canvas App - Run the flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/5eaa9e76-ada2-47c9-8794-bb19dc6094a0)


# Step 21 

Click on the flow link 


![25 Click on flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/b39d7f81-c9bb-467b-a96e-64c720852b52)


# Step 22 

Copy the output JSON from compose to a text file. You will use in next step 

![26 Copy the Output Compose](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/9d4cf06d-4071-4919-a672-1e863762f674)


# Step 23 

Edit the flow
![27 Edit Flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/2856a94c-2939-41d5-94e7-663591bfbadd)


# Step 24 

In Next Step, search for Parse JSON action, select **Add dynamic content** and use outsummary variable 
![28 Parse JSON Output summary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/f40bfc52-356b-4cbe-9bd7-2936c52fabd9)


# Step 25 

Click on **Generate from Sample** button

![29 Parse JSON  Generate Sample](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/ad47ef47-444e-409b-83c1-2dbb19ea52d1)


# Step 26

Paste the JSON content that you copied from Step 22 
![30 Paste JSON cONTENT FROM previois step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/b97fb88c-e375-4215-bb09-8c3fbf8f89d1)

![31 Paste JSON cONTENT FROM previois step](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/3400435a-e8ee-42c9-92d2-b52708e27d37)




# Step 27 
In next step, search for **Respond to a PowerApp or flow action** 

![32 Respond to Poweer Apps  or flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/38b2c7d1-4fa5-4d5e-96c1-1217045c54b3)


# Step 28 

Add text input variable called **response** and use **text** from Parse JSON 

![33 Output Summary](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/4689890d-9a07-4334-8b3a-95eb39c6924a)

# Step 29 

Save the flow 

![33 Save flow](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/0c92eec3-4b3f-46e2-83f2-83481000f5e7)


# Step 30 

Back to Power Apps, Set the response variable at the **Get Answer** 
![34 Adjust Flow Response](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/b0383ae5-b96e-4693-8277-63748e7a13c6)


# Step 31 

Assign gOutput the label control 

![35  Output label](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/1ad7ae76-95ca-4b83-9e4b-0a8b7ac24056)

# Step 32 

Run the Power Apps, ask question, click on Get Anwser and anwser is shown at output label


![36 Final Output](https://github.com/aarohbits/PowerAppsWorkShopAOAI/assets/35991723/09d2473d-2d4c-4dea-ab5c-f30f7e3cd6e6)








