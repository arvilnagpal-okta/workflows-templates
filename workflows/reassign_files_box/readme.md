## **Workflows Template: Reassign Files while Deprovisioning with Box**


## **<span style="text-decoration:underline;">Overview</span>**

File download:[ BoxComFlows.flopack](https://drive.google.com/file/d/1i76OfhbakXL1h1bx55AjM42BZ1wQrhB4/view?usp=sharing)

The purpose of this Workflow pack is to automatically transfer a target user’s Box files and folders to that target user’s manager as part of the off-boarding process. This workflow is triggered by a user being removed from a specified Okta group.


## **<span style="text-decoration:underline;">Before you get Started / Prerequisites</span>**

For the workflows in the Okta Workflow Pack to work you will need:

    ·   	An Okta Workflow connector in to your Okta tenant that has Workflows enabled

    ·   	A[ Box.com](http://Box.com) Workflow connector in Workflows

    ·   	An Office 365 Mail connector in Workflows

    ·   	An existing user (that will represent the manager user) in Okta and[ Box.com](http://Box.com) where the username in Okta and in Box are the same (the user’s email address) The manager user’s email address needs to point to a valid email address so that the manager can get the email notifications as part of the flow.

    ·   	An exiting user (that will represent the target user) in Okta where the manager attribute in Okta Universal Directory is the username of the Okta user that represents the manager.

    ·   	An Okta Group that will be used to trigger this Workflow.

    ·   	[Optionally]: Federate your[ Box.com](http://Box.com) tenant with your Okta tenant that has Okta Workflows enabled.

    ·   	If you do not choose to federate your[ Box.com](http://Box.com) tenant with Okta, you will need to configure a[ Box.com](http://Box.com) application in your Okta tenant that has Okta Workflows enabled configured as Secure Web Authentication.

    ·   	DO NOT enable provisioning for the[ Box.com](http://Box.com) application in Okta.

    ·   	Add the[ Box.com](http://Box.com) application to the Okta Group that will be used to trigger this Workflow.

## **<span style="text-decoration:underline;">Setup Steps</span>**

    1. 	Select the “Okta Box User - Deprovision Flow” flow from the folder.

    2. 	If you have not already done so, authorize the connections to Box.com, Office 365, and Okta.

    3. 	Change the name of the “[Box.com](http://Box.com) Assignment Group” variable to match the Okta group you created in the prerequisites section.

    4. 	If you do not wish to have the target user automatically deleted from your[ Box.com](http://Box.com) tenant, set the “Remove Box User” variable to False.

    5. 	Save the “Okta Box User - Provision Flow”

    6. 	Turn on the “Okta Box User - Provision Flow”

    7. 	Navigate back to the flows in the flow pack

    8. 	Select the “Okta Box User - Provision Flow”

    9. 	Change the name of the “[Box.com](http://Box.com) Assignment Group” variable to match the Okta group you created in the prerequisites section.

    10.  Save the “Okta Box User - Provision Flow'

    11.  Turn on the “Okta Box User - Provision Flow”

    12.  Navigate back to the flows in the flow pack.

    13.  Turn on the “[UTIL] Send Manager Email Message Flow”

## **<span style="text-decoration:underline;">Testing this Flow</span>**

To test this flow Workflow pack:

[Box.com](http://Box.com) User Onboarding:

    1. 	Start by adding an existing Okta user to the Okta group that you created as part of the prerequisites section as well as defined in the “[Box.com](http://Box.com) Assignment Group” variable in the “Okta Box User - Provision Flow”.

    2. 	Go into your Box tenant and view the users in your Box tenant. You should see the user you added to the Okta group in step 1 added to your[ Box.com](http://Box.com) tenant.

    3. 	If you login to Okta as the user that you added to the Okta group specified in step 1 you should see the[ Box.com](http://Box.com) application assigned to them. If you have federated[ Box.com](http://Box.com) to the Okta tenant you should be able to click on the[ Box.com](http://Box.com) chicklet and the user will have Single Sign On into Box.com.

    4. 	The user in[ Box.com](http://Box.com) will have a folder created with their name in[ Box.com](http://Box.com) as well.

    5. 	For testing go ahead and put a test text file into the personal folder created for the target user (the one just created) in Box.com

    6. 	Check the email box for the manager user assigned to the target user. There should be an email message about the box user being created.

[Box.com](http://Box.com) User Off-boarding:

    1. 	Start by removing the existing Okta target user from the Okta group that you created as part of the prerequisites section as well as defined in the “[Box.com](http://Box.com) Assignment Group” variable in the “Okta Box User - Provision Flow”.

    2. 	Go to the manager user’s email box. You should see an email about the target user’s files and folders being transferred to the manager user.

    3. 	Login to[ Box.com](http://Box.com) as the manager user if[ Box.com](http://Box.com) is not federated to Okta

        * 	If[ Box.com](http://Box.com) is federated to Okta, login to Okta as the manager user and click on the[ Box.com](http://Box.com) chicklet to Single Sign On into Box.

    4. 	Check that you should see a new folder in that manager user’s[ Box.com](http://Box.com) with a format of:

    ”&lt;[Box.com](http://Box.com) username of target user> - &lt;full name>'s Files and Folders”

    5. 	If you selected to have the target user’s[ Box.com](http://Box.com) account removed, when you view the[ Box.com](http://Box.com) users you should also see that the target user is no longer in the[ Box.com](http://Box.com) tenant.

## **<span style="text-decoration:underline;">Limitations & Known Issues</span>**

None
