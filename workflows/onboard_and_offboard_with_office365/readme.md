# Workflows Template: Onboard and Offboard with Office365


## <span style="text-decoration:underline;">Overview</span>

File download:[ office365.flopack](https://drive.google.com/file/d/1GGbbKDbIU2C6QVaXrCu6jZYy040VRmDr/view?usp=sharing)

This page outlines a sample workflow pack that contains three workflows:



1. An **Office 365 Staged Deactivation** flow: In this flow, once a user is removed from a specified Okta group:
    *   The user’s Office 365 account will be disabled immediately.
    *   An email to the user’s manager to that effect will be sent.
    *   After a specified delay, the user’s Office 365 license will be removed.
    *   An email to the user’s manager to that effect will be sent.  \

2. An **Office 365 Activation** flow: Once a user is added to a specified Okta group:
    *   The user’s Office 365 account will be enabled immediately.
    *   The user’s previously assigned Office 365 licenses will be reassigned immediately.
    *   An email to the user’s manager to that effect will be sent.
3. A Store **All Microsoft License** flow: This flow stores the current Microsoft subscription licenses in a Okta Workflows table called Office 365 Licenses to be used in assigning the Microsoft license to the target user during the O365 Activation flow.


## <span style="text-decoration:underline;">Before you get Started / Prerequisites</span>


### Pre-Requisites:

For this flow pack in order to send an email to the manager on the creation of a user, an Office 365 Mail connection and an Office 365 Admin connection needs to be configured in addition to the Okta tenant connection. _You will need to have these connections created and authorized prior to installing the flow pack. _

You will also need Access to the Microsoft Office 365 Admin Portal as an admin user. [https://admin.microsoft.com/AdminPortal/](https://admin.microsoft.com/AdminPortal/)

 


         


## <span style="text-decoration:underline;">Setup Steps</span>


### Office 365 Setup Steps



1. Create a manager user in the Office 365 tenant

    Open the Microsoft Admin Center ([https://admin.microsoft.com](https://admin.microsoft.com)) and login as your .onmicrosoft.com administrator account.

    Navigate to Users -> Active Users

    Click on Add a User

    Fill out the information for the following fields:

    *   First name
    *   Last name
    *   Display name
    *   Username
    *   Username domain (you should select your email domain here not your .onmicrosoft.com domain here)
    *   Password

    Leave “Require this user to change their password when they first sign in” and “Send password in email upon completion” unchecked.

    Record the First name, Last name, Username, Username domain and Password somewhere for the manager user as you will need them later. _

    Click Next

    On the Assign Product licenses page ensure that “Assign user a product license” is checked. It should default to your subscription license for your tenant. Make sure that the license installed will create an Exchange mailbox so that the manager can receive email messages

    Click Next

    On the Optional settings page click Next

    On the Review and finish page, click Finish Adding

2. Create a target user in the Office 365 tenant

    In the Microsoft Admin Center ([https://admin.microsoft.com](https://admin.microsoft.com))  console that you should still be logged into

    Navigate to Users -> Active Users

    Click on Add a User

    Fill out the information for the following fields:

    *   First name
    *   Last name
    *   Display name
    *   Username
    *   Username domain (you should select your email domain here not your .onmicrosoft.com domain here)
    *   Password

    Leave “Require this user to change their password when they first sign in” and “Send password in email upon completion” unchecked.

    Record the First name, Last name, Username, Username domain and Password somewhere for the target user as you will need them later. _

    Click Next

    On the Assign Product licenses page ensure that “Assign user a product license” is checked. It should default to your subscription license for your tenant.

    Click Next

    On the Optional settings page click Next

    On the Review and finish page, click Finish Adding

### Okta Organization Setup Steps



1. Create the Okta group that will be used to trigger the Okta Workflows in this flow pack.

    Login to your Okta tenant as a Super Administrator user.

    Go to the Admin console in your Okta tenant

    Navigate to Directory -> Groups

    Click on Add Group

    Type in Office 365 Assignments for the group name and the description

    Click on Add Group

2. Create the Okta group that will be used to trigger the Okta Workflows in this flow pack.

    Navigate to Directory -> People

    Click on Add Person

3. Enter the following information based on information that you recorded above in the “Create a target user in the Office 365 tenant” step.
    *   First name: use the First name that you recorded for target user
    *   Last name: user the Last name that you recorded for the target user
    *   Username: use the Username that you recorded for the target user +  \
    @ + the Username domain that you recorded for the target user (ex. [Tammy.tester@example.com](mailto:Tammy.tester@example.com))
    *   Primary email: this should be the same as the Username field
    *   Password: Select “Set by admin”
    *   Enter Password: the desired password for this user.  (for ease of testing this Okta workflow, make it the same password you recorded for this user in the “Create a target user in the Office 365 tenant” step.

    Click the Save button

4. Enter the following information based on information that you recorded above in the “Create a manager user in the Office 365 tenant” step.
    *   First name: use the First name that you recorded for manager user
    *   Last name: user the Last name that you recorded for the manager user
    *   Username: use the Username that you recorded for the manager user + @ + the Username domain that you recorded for the manager user (ex. [Terry.manager@example.com](mailto:Tammy.tester@example.com))
    *   Primary email: this should be the same as the Username field
    *   Password: Select “Set by admin”
    *   Enter Password: the desired password for this user.  (for ease of testing this Okta workflow, make it the same password you recorded for this user in the “Create a manager user in the Office 365 tenant” step.
5. Edit the target user in Okta to add the manager

    Navigate to Directory -> People

    In the Search dialog start typing the name of your target user in Okta

    Once the target user in Okta shows up in the search click on that user

    Click on the Profile tab

    Click on Edit

    Scroll down to the Manager field

    Put in the Okta username for the Okta manager user that you created in the step above.

    Click Save.



### Okta Workflows Setup Steps



1. Install the flow pack

    Create a new folder in Workflows and label the name of the folder **_Office 365_**

    Click on the gear icon for the new Office 365 folder and select import.

    Drag and Drop the flow pack that you downloaded into the Choose File section and click OK

2. Modify and run the Store all Microsoft Licenses workflow

    Open the Store all Microsoft Licenses workflow

    Change the name of the Okta group to use for the testing (if desired)

    Run the Store all Microsoft License Workflow

    Go to Tables in the Office 365 folder

    You will now see the subscription license model that you have assigned to your Microsoft 365 tenant along with the specified Okta group associated with it.

    Navigate back to the Flows tab.

3. Modify the O365 Staged Deactivation Workflow

    Open the O365 Staged Deactivation workflow

    Leave the value of the Office Group as it already matches the Okta group that you created in “Create the Okta group that will be used to trigger the Okta Workflows in this flow pack” step above

    Change the setup variables as desired:

     *   Delay Integer: The increment of time as specified by the Delay Interval Type that will transpire between the time the users Office 365 account is disabled and the users Office 365 licenses are removed.

     *   Delay Interval Type: The Delay Interval Type of time as specified by the Delay Integer that will transpire between the time the users Office 365 account is disabled and the users Office 365 licenses are removed. (Ex. if Delay Integer is set to 1 and Delay Interval Type is minute then there will be a delay of one minute.  The valid Delay Interval Types are: second, minute, hour, week, month, year.

    After making changes to the O365 Staged Deactivation workflow click the save icon to save the changes.

Turn on the following workflows by clicking the On / Off button so that they are green

    *   Clear Microsoft License Table
    *   [Child] Store all Microsoft License
    *   [Child] Clear Microsoft License Table
    *   Store all Microsoft License
    *   O365 Staged Deactivation

## <span style="text-decoration:underline;">Testing the Flow</span>

1. Open the Store All Microsoft License flow and run that flow.
2. Observe the current Office 365 target user

    Open and login to the Microsoft Office 365 [Admin Portal](https://admin.microsoft.com/AdminPortal/) as your Office 365 admin user.

Go to Users → Active Users

    Click on the username for the test user that is a member of your Okta group.

    Observe that the user has an Office 365 license assigned and is allowed to Sign In.

3. Deactivate the current Office 365 User

    Remove the user from the specified Okta group.

    Open the email mailbox for the manager user.

    You should see an email message that the user removed from the Okta group specified has been disabled in Office 365.

    If you return to the Microsoft Office 365 Admin Portal and refresh the page, then select that user that the user is not allowed to sign in. The user still has an Office 365 License assigned.

    Then after the specified delay, in the default configuration that is one minute, the manager gets an email that the Office license for the target user has been removed.

    If you return to the Microsoft Office 365 Admin Portal and refresh the page, sure enough the user targeted is unlicensed.

4. Activate the current Office 365 User

    In the Okta Workflows console, turn on the O365 Activation flow.

    Now go to the Okta Admin console.

    We will reset the users Office 365 status. Put that same user back in the Okta specified group.

    The manager will get an email that the user's Office 365 user has been enabled and license restored.

    Sure, enough if you return to the Microsoft Office 365 Admin Portal and refresh the page, then click on the target user, you can see that the license has been restored and the user is allowed to sign in again.

## <span style="text-decoration:underline;">Limitations & Known Issues</span> 

**NOTE:** You will need to make sure the prerequisites are met and that you run the Store all Microsoft Licenses workflow

The scope of this workflow does not include creating Office 365 users, federating the Office 365 tenant with Okta for Single Sign On or turning on Office 365 provisioning with Okta.
