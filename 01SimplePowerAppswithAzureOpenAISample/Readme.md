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




# Step 11 



