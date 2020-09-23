## **Workflows Template: Manage GSuite User Licenses**


## **<span style="text-decoration:underline;">Overview</span>**

This page outlines a sample workflow pack that contains two workflows:


    1. 	An G Suite User Deactivation Flow: In this flow, once a user is removed from a specified Okta group:


        1. 	The userís G Suite account will be disabled immediately.


        2. 	An email to the users manager to that effect will be sent.


        3. 	After a specified delay, the userís G Suite license will be removed.


        4. 	An email to the users manager to that effect will be sent.


    2. 	An G Suite User Activation Flow: Once a user is added to a specified Okta group:


        1. 	The userís G Suite account will be enabled immediately.


        2. 	The userís previously assigned G Suite licenses will be reassigned immediately.


        3. 	An email to the users manager to that effect will be sent.


## **<span style="text-decoration:underline;">Before you get Started / Prerequisites</span>**

For this flow pack in order to send an email to the manager on the creation of a user, an GMail connection and an G Suite Admin connection needs to be configured in addition to the Okta tenant connection.

_You will need to have these connections created and authorized prior to installing the flow pack._

Google G Suite will want to automatically assign licenses to new users in the G Suite tenant. You need to turn this off for Workflows to be able to add and remove licenses. To do this go to the[ G Suite Admin Console](https://admin.google.com/u/1/ac/home) and then click on Billing

Once in Billing you will need to do two things:


    1. 	Add an additional license. I chose the Android Management license as it is zero cost / free.


    2. 	ONLY after you have added the additional license will you see the setting to auto assign licenses so that you can turn it off for everyone. 

Along with the connectors specified above you will need:

**_NOTE: If you use the G Suite Initialization flow outlined further down this page, steps 1 and 2 below will be created and done for you except for number 2 item c. The initialization flow will not create the G Suite users._**


    1. 	An Okta group that will be used to trigger the workflow. No applications or directories should be assigned to this group.


    2. 	An Okta User that will be added and removed from the above Okta group as part of the demo.


        1. 	A valid Okta user (username) should be populated in the manager field for this user to represent the user assigned as the manager to this user.


        2. 	Both this user and the manager user should have a valid primary email address assigned to them and you need to have access to the email mailbox inbox for the manager user during the demo.


        3. 	Both the target user and the manager user need to already exist in G Suite as this flow does not provision the G Suite accounts. The target user needs to have a valid G Suite License assigned to them before beginning the demo.


    3. 	Access to the Google G Suite Admin Portal as an admin user.


        1. 	[https://admin.google.com/u/1/?hl=en](https://admin.google.com/u/1/?hl=en)


         


## **<span style="text-decoration:underline;">Setup Steps</span>**

Create a new folder in Workflows and label it **_G Suite Flows_**

Click on the gear icon for the new G Suite Flow folder and select import.

Drag and Drop the flow pack that you download[ here](https://okta.box.com/s/iwbxmhdq2yrlhsk9lih1vogrd39o5vvt) into the Choose File section and click OK 

Navigate to the G Suite Flows folder.

Turn on the following flows:



*   GSute Store License flow
*   [Child] Delete Row from Table
*   [Child] Add License Row to Table

Open the GSuite Store License flow

Change the OktaGroupName variable value in the Assign card to the desired Okta group name that will be used to trigger the flow when a user is added or removed from this group. 

Change the G Suite License to Assign variable value in the Assign card to the name of the G Suite license you wish to assign a user in the G Suite Activation flow. 

Save the GSuite Store License flow.

Run the GSuite Store License flow.

Navigate to the GSuite License table and ensure that one record exists

If there are no records in the table, validate the value in the G Suite License to Assign - Assign card to ensure that the name of the desired license is correct and rerun the flow if necessary.

Open the G Suite Initialization Flow

Change the values for the G-Suite target user


    Change the User Name field to match the email address of your existing G Suite target user. (The user that will have licenses removed or added to them)


    Change the First Name, Last Name and Password fields as desired for the target user that will be created.

 Change the values for the G-Suite manager user


    Change the User Name field to match the email address of your existing G Suite manager user. (The user that receive the email messages about the target users licenses being removed or added.) This user must have a valid email inbox so you can check the email messages.


    Change the First Name, Last Name and Password fields as desired for the target user that will be created.

Change the Okta group name if desired.


    Change the name of the Okta group to use for the demo (if desired)

Save the G Suite Initialization Flow

Run the G Suite Initialization Flow

Open the G Suite Staged Deactivation workflow 

Change the setup variables as desired:


    **Okta Group Name**: The name of the existing Okta group that will be used to trigger the G Suite Workflows. If you used the G Suite Initialization flow make sure the group name is the same as the one defined when you ran that flow.


    **Delay in Minutes**: The increment of time as specified by the Delay Interval in minutes that will transpire between the time the users G Suite account is disabled and the users G Suite licenses are removed.

 After making changes to the G Suite Staged Deactivation workflow click the save icon to save the changes.

Open the G Suite Activation workflow and change the Okta Group Name to match the Okta group that you defined in the G Suite Staged Deactivation workflow.

Okta Group Name:  The name of the existing Okta group that will be used to trigger the G Suite Workflows. Make sure this is the same group name you set in the G Suite Staged Deactivation flow.

Click the Save icon to save the changes.

Turn on both workflows by clicking the On / Off button so that they are green as shown below:


    ∑   	G Suite Activation


    ∑   	G Suite Staged Deactivation 

 


## **<span style="text-decoration:underline;">Demo Flow</span>**

Open and login to the Google G Suite[ Admin Portal](https://admin.google.com/u/1/?hl=en) as your G Suite admin user.

Goto Directory ? Users

Click on the username for the test user that is a member of your Okta group.

Point out that the user is allowed to Sign In.

Scroll all the way to the bottom to show what licenses are assigned to the user. 

Remove the user from the specified Okta group.

Open the email mailbox for the manager user.

You should see an email message that the user removed from the Okta group specified has been disabled in G-Suite. 

If you return to the G Suite Admin Portal and refresh the page, then select that user that the user is not allowed to sign in. The user still has an G Suite License assigned.

Then after the specified delay, in the default configuration that is one minute, the manager gets an email that the G Suite license for the target user has been removed. 

If you scroll down the page after refreshing the page, sure enough the user targeted is unlicensed.

Now we will reset the users G Suite status. Put that same user back in the Okta specified group.

The manger will get an email that the users G Suite user has been enabled and license restored.

Sure enough if you return to the G Suite Admin Portal and refresh the page, then click on the target user, you can see that the license has been restored and the user is allowed to sign in again.


## **<span style="text-decoration:underline;">Limitations & Known Issues</span> **

**Additional limitation**: Does not work with cloud identity free licenses, since license list pulls as empty in Okta if that is the only license assigned to a user. Worked with G Suite Business license

 
