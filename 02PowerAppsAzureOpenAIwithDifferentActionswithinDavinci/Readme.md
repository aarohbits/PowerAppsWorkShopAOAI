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
