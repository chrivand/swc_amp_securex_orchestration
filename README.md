![License: CISCO](https://img.shields.io/badge/License-CISCO-blue.svg) [![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/aligarci/swc_amp_securex_orchestration)

# swc_amp_securex_orchestration
Workflow of SecureX Action Orchestrator module.
 
 
# Authors:
- Hanna Jabbour
- Alicia Garcia Sastre
- Remi Vacher
 

# Motivation
The goal of this workflow is to trigger an automated response when we receive an email with an alarm triggered in Stealthwatch Cloud. Leveraging AMP for endpoints API, we will isolate the host and hence, protect our network.

Having a SOC analyst reviewing the event and then taking a decision about the required mitigation is not fast enough. 
We need to isolate the host from the network to reduce the threat ability to spread. 

https://youtu.be/lJnXQhRhUZg


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/orchestration.png) 



# Scenario
- Remote or local worker connected to the network.
- The end device has AnyConnect and AMP for endpoint installed for endpoint security and connectivity
- AnyConnect is integrated with SWE to share process information and flow information
- Stealthwatch is monitoring the network end to end
- Stealthwatch is integrated with CTR, SecureX and AO


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/scenario.png) 



# Workflow steps


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/steps.png) 


1. Device initiate a suspicious behavior
2. SWC triggers an alert on this communication and sends a notification to the admin
3. Action Orchestrator (AO) parsing constantly email events. 
4. When the alarm email is received, it will trigger the response workflow
5. Parsing of endpoint IP from email
6. Find AMP GUID that is the source of the malicious behavior
7. Isolate host with AMP GUID
8. Send a message to a webex teams room notifying about the endpoint isolation


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/webex_teams.png) 


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/workflow.png) 



# How to use it

## Stealthwatch cloud configuration
Configure Stealthwatch Cloud to send you an email every time an alert is triggered:


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/swc1.png) 


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/swc2.png) 




## Action Orchestration configuration
- Log into SecureX  
- Click on Orchestration tab
- Click on import


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/secureX_1.png) 

- Import from: "browse"
- Paste JSON file content into text box or browse for the JSON file locally in your PC
- Check "import as a new workflow (clone)
- Click on import


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/secureX_2.png) 

- You will see a message to update the credentials for email address, AMP and webex teams.


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/update.PNG) 


- "Stealthwatch Cloud email" will need to get the target id modified to match your email credentials
![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/email.png) 


- You will need to add the target and account keys of your AMP4E endpoints.
![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/amp.png) 


- Lastly, "Webex Teams Post a Message about isolation" will need to get the Webex Teams bot and Webex Teams Room modified:


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/webex_teams_config.png) 


   - The access token of your Webex Teams bot (You can create one and obtain the acces token here: https://developer.webex.com/)
   - Also add the room id of your webex room, where you want to post the message (You can obtain your room id going to https://developer.webex.com/docs/api/v1/rooms/get-room-details and pasting the name of your room)
   

![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/id.png) 


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/id2.png)


- Now the workflow is imported. You can click on it and will be able to modify it:


![alt text](https://github.com/aligarci/swc_amp_securex_orchestration/blob/master/workflow2.png) 


