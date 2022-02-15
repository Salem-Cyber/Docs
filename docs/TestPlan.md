| [Docs Home](../index.md) |

# Walk Through of Salem Functionality

## 1. Follow Salem Quick Start 
The Salem quick start guide found [here](/docs/Quickstart.md) will guide you through creating an AD app registration, deploying the Salem App and installing the MS Teams app

### Notes about deployment
When deploying as a managed app, a notification is sent that kicks off a platform verification and app update.  This process can take up to 15 minutes.  During this time you won't be able to use Salem.

## 2. Test Salem Chat
From MS Teams, select apps and find the Salem app. Add to your chat

After a few seconds you should receive some welcome text, if not send a message to Salem.

Follow the log in prompt to authenticate and authorize your Salem access.

If you've successfully logged on, you should see a welcome card showing options such as alerts and metics

## 3. Upload a test alert
The core function of Salem is to analyze cybersecurity alerts. To test this functionality you can upload an alert via Salem Chat and verify the alert was processed.
From the Welcome card select alerts

a. From the welcome card, select 'alerts' (if you need to recall a new welcome card type 'menu' into the chat). Select 'add new' and add and submit the following:
```
Source: User Added
Alert Name: Malware
Alert Body: 2022-02-10 08:23:24 action=blocked file=/tmp/scary.py user=$wd123455687 dest=wd12345687
```

b. The returned messages should contain the alert id.  Select 'yes' to view the alert card.  Some data will be populated but it might take a minute to get all populated.  Hit update periodically until the Salem threat Likelihood is populated

c. Once the alert is done processing, select 'False Positive'

d. On the expanded card, select this exact user in the left most dropdown list.

e. Select 'Yes' to Confirm report as False positive

## 4. Answer a Salem Question
Salem asks questions in an attempt to collect contextual information used to improve future threat predictions.  Salem will at most once a day send a request to have you answer a question.  To force a new question to be asked, do the following:

a. Recall the menu card by sending Salem a new message with text "menu"

b. Select "Help Salem Learn", the card should be updated with a question.  If no new questions are available, Salem will respond with a message saying as much.

c. Select that you don't know the answer, and don't want to answer other questions

## 5. View Salem Metrics
The metrics view provides some basic information about the volume of work process by Salem.

a. To view metrics recall the menu card by sending Salem a new message with text "menu"

b. On the returned menu card select metrics.  The card should be updated with current metrics which should include indication of processing the alert entered in a prior step

## 6. View a configuration file
Configuration files provide users the ability to customize their Salem experience.

a. To view a configuration file. Type 'configure' into the Salem Chat in MS Teams

b. Follow the props to select 'ParsingConf' and then 'default'

c. You should see a json object containing the requested configuration information

d. To Update a configuration, type 'update conf' in the Salem Chat in MS Teams

e. Follow the prompt to select ParsingConf, and then paste the json object from step c into the text box.  If you make a modification you can follow steps a through c to confirm the change
