# Walk Through of Salem Functionality

## 1. Follow Salem Quick Start 
The Salem quick start guide found [here](/guides/Quickstart.md) will guide you through creating an AD app registration, deploying the Salem App and installing the MS Teams app

### Notes about deployment
When deploying as a managed app, a notification is sent that kicks off a platform verification and app update.  This process can take up to 15 minutes.  During this time you won't be able to use Salem.

## 2. Test Salem Chat
1. From Microsoft Teams, select apps and find the Salem app. Add to chat 
    * The app will likely be found under `Build for your org` section

2. After a few seconds you should receive some welcome text, if not send a message to Salem.

3. Follow the log in prompt to authenticate and authorize your Salem access.

4. If you've successfully logged on, you should see a welcome card showing options such as alerts and metics

## 3. Upload a test alert
The core function of Salem is to analyze cybersecurity alerts. To test this functionality you can upload an alert via Salem Chat and verify the alert was processed.
From the Welcome card select alerts

1. From the welcome card, select 'alerts' (if you need to recall a new welcome card type 'menu' into the chat). Select 'add new' and add and submit the following:
```
Source: User Added
Alert Name: Failed authentication to Azure key vault
Alert Body: 2022-04-10 08:23:24 action=failed src=10.0.0.1 user=appDev_svc dest=devKeyVault
```

2. The returned messages should contain the alert id.  Select 'yes' to view the alert card.  Some data will be populated but it might take a minute to get all populated.  Hit refresh periodically until the Salem threat Likelihood is populated

3. Once the alert is done processing, select 'False Positive'

4. On the expanded card, select this exact account in the left most dropdown list.

5. Select 'Yes' to Confirm report as False positive

## 4. Answer a Salem Question
Salem asks questions in an attempt to collect contextual information used to improve future threat predictions.  Salem will at most once a day send a request to have you answer a question.  To force a new question to be asked, do the following:

1. Recall the menu card by sending Salem a new message with text "menu"

2. Select "Help Salem Learn", the card should be updated with a question.  If no new questions are available, Salem will respond with a message saying as much.

3. Select that you don't know the answer, and don't want to answer other questions

## 5. View Salem Metrics
The metrics view provides some basic information about the volume of work process by Salem.

1. To view metrics recall the menu card by sending Salem a new message with text "menu"

2. On the returned menu card select metrics.  The card should be updated with current metrics which should include indication of processing the alert entered in a prior step

## 6. View a configuration file
Configuration files provide users the ability to customize their Salem experience.

1. To view a configuration file. Type 'configure' into the Salem Chat in MS Teams

2. Follow the props to select 'ParsingConf' and then 'default'

3. You should see a json object containing the requested configuration information

4. To Update a configuration, type 'update conf' in the Salem Chat in MS Teams

5. Follow the prompt to select ParsingConf, and then paste the json object from step c into the text box.  If you make a modification you can follow steps a through c to confirm the change
