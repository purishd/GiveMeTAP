# GiveMeTAP
| Title | Description |Author|
|-----:|---------------|-----|
| Give Me TAP|This repo is created to help build a quick PowerApps application that helps your users generate TAP and makes your administrators/helpdesk job easier.               |purishd|


# Problem Statement
Often customer's end users need TAP for either first time use when they join the organisation or for other sceanrios later. This task is usually done by adminstrators manually as per design. However, what if customers could build a user facing application that could give them TAP whenever they need it. Isn't that better than having to manually generate a TAP.

# Solution
This can be easily achieved by a simple PowerApps application which reduces operational overhead by giving control to the end users. Off course, while designing the application cutomer needs to consider security implications of handing this application to end users and design security controls around TAP generation and usage etc.

# Detailed Design
From technical implementation perspective, following are high level steps.
1. Build a Power App UI that will collect user's UPN. This is the front-end that will be used by the end user to generate TAP ans display it on the screen itself.
2. Build Power Automate flow that will read the user's UPN and generate TAP by calling Graph API.

# Build a Power App

# Build a Power Automate flow
This is how my sample Power App looks like. Follow below guidelines to create a similar Power App or use your own creativity to extend this Power App and make it even better.

![image](https://github.com/purishd/GiveMeTAP/assets/11908199/a64dee82-9a65-42e4-b19b-5b954c92a0de)

Following controls are being used in this super simple app.
1. An Image for customer logo.
2. Label for the name of the app.
3. Label and text input to get the user UPN.
4. Button to share TAP that will hook into my Power Automate flow.
