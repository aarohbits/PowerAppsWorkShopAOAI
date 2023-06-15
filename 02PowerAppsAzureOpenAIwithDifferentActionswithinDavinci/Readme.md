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

## Step 2

Add a new flow from Cavas apps 

## Step 3

Add new blank flow

## Step 4

Rename the flow, add new step, add new HTTP action and set to post 

## Step 5 

Nagivate to the Azure portal, under playground select Compleltions >> Select Question answring >> select the View code 

## Step 6

Copy the Endpoint and Key from Azure OpenAI service 

## Step 7 

Copy the URL to URI at Power Automate and for key type in api-kpi amd paste the key s