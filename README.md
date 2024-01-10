# GiveMeTAP
| Title | Description |Author|
|-----|---------------|-----|
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

This is how my sample Power App looks like. Follow below guidelines to create a similar Power App or use your own creativity to extend this Power App and make it even better.

![image](https://github.com/purishd/GiveMeTAP/assets/11908199/a64dee82-9a65-42e4-b19b-5b954c92a0de)

Following controls are being used in this super simple app.
1. An Image for customer logo.
2. Label for the name of the app.
3. Label and text input to get the user UPN.
4. Button to share TAP that will hook into my Power Automate flow.

Calling below code on "OnSelect" property of the Share TAP button. This code will help set the buttonPressed and then call Power Automate flow and set the value of variable newTAP to generated TAP.
```
If(IsBlank(UPNTextInput.Text), Notify("Please enter user UPN",NotificationType.Error),
Set(buttonPressed,"shareTAPButton");
Set(newTAP,TAPFlow.Run(UPNTextInput.Text).tap););
```
5. A hidden label that only lights up when the TAP is generated and shows the generated TAP on the screen for end user to view it.

   Making this label visible when share TAP button is pressed.
```
   If(buttonPressed = "shareTAPButton", true, false)
```
   Setting the "Text" property of this button to variable newTAP. This variable is blank initially but its value is set when the Power Automate flow sends the TAP back to the Power App.
  
6. A reset button that I am using to quickly reset the values of controls. Feel free to use any other ways as you like to reset the form values.
```
  Reset(UPNTextInput);
  Set(newTAP,"")
```
# Build a Power Automate flow
Follow below steps to create Power Automate Flow. This is how your overall flow will look like once all the steps are added to it.

   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/05dc79a8-2fe5-434e-9411-85657bc6a6c5)


1. Create a new instant cloud flow.
2. Choose PowerApps as trigger of this flow.

   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/9f17ec93-266a-4e4e-a167-190074f3156f)

3. Intialize a variable that will collect the user UPN value from Power Apps.
   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/57fb54cb-2240-4f3d-b4cc-ed8720788e18)

4. Get a graph token using the client credential flow. You can choose other ways to get a graph token as you prefer.

   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/bece3754-6b97-4a9c-97b7-adc23673ea13)

5. Parse the JSON output from above step to get the access token.

   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/b4bdb038-f5d6-4757-9062-73944bb092cd)

6. Make a Graph API call to generate TAP.

   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/6a684038-dd82-47fb-b961-9e8c10572f90)

7. Parse the JSON output from above step to get the newly genrated TAP.

   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/5f51f174-3488-4f15-b90a-af024b5b10be)

8. Add compose action to get value of TAP.

   ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/45b0e1b3-e606-4e76-afac-052733a026c1)

9. Send the generated TAP to Power App in a variable.
    
    ![image](https://github.com/purishd/GiveMeTAP/assets/11908199/4a7c329b-e0b6-4e1f-a9a7-bd97f680f08d)


