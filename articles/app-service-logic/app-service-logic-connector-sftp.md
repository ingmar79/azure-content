<properties
	pageTitle="Using the SFTP Connector in Logic Apps | Microsoft Azure App Service"
	description="How to create and configure the SFTP Connector or API app and use it in a logic app in Azure App Service"
	authors="anuragdalmia"
	manager="erikre"
	editor=""
	services="app-service\logic"
	documentationCenter=""/>

<tags
	ms.service="app-service-logic"
	ms.workload="integration"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="03/16/2016"
	ms.author="sameerch"/>

# Get started with the SFTP Connector and add it to your Logic App
>[AZURE.NOTE] This version of the article applies to logic apps 2014-12-01-preview schema version. For the 2015-08-01-preview schema version, click [SFTP API](../connectors/connectors-create-api-sftp.md).

Use the SFTP Connector to move data to and from an SFTP server. You can download files from or upload files or list files to and from an SFTP server.

Logic apps can trigger based on a variety of data sources and offer connectors to get and process data as a part of the flow. You can add the SFTP Connector to your business workflow and process data as part of this workflow within a Logic App. 

## Creating an SFTP connector for your Logic App ##
A connector can be created within a logic app or be created directly from the Azure Marketplace. To create a connector from the Marketplace:  

1. In the Azure startboard, select **Marketplace**.
2. Search for “SFTP Connector”, select it, and select **Create**.
3. Configure the SFTP connector as follows:  
![][1]
	- **Location** - choose the geographic location where you would like the connector to be deployed
	- **Subscription** - choose a subscription you want this connector to be created in
	- **Resource group** - select or create a resource group where the connector should reside
	- **Web hosting plan** - select or create a web hosting plan
	- **Pricing tier** - choose a pricing tier for the connector
	- **Name** - give a name for your SFTP Connector
	- **Package settings**
		- **Server Address** - Specify the SFTP Server name or IP address
		- **Accept Any SSH Server HostKey** - Determines if any SSH public host key fingerprint from the Server should be accepted. If set to false, the host key will be matched against the key specified in the “SSH Server Host Key Finger Print” property
		- **SSH Server HostKey** - Specify the fingerprint of the public host key for the SSH server - *optional*.
		- **Root Folder** - Specify a root folder path.  If blank will default to root.
		- **Encrypt Cipher** - Specify the encryption cipher - *optional*.
		- **Server Port** - Specify the SFTP Server port number
4. Click on Create. A new SFTP Connector is created.

5. Browse to the just created API App via Browse -> API Apps -> <Name of the API App just created> and you can see that the "Security" component is not configured:  
![][2]
6. Click on "Security" component to configure Security (User Name, Password, Private Key, PPK File password) for SFTP connector.
Select "Password" or "Privatekey" or "MutliFactor" authorization tab under Security and provide the required properties:  
![][3]  
![][4]  
![][5]  
6. Once the security configuration is saved, you can create a logic App in the same resource group to use the SFTP connector.

## Using the SFTP Connector in your Logic App ##
Once your API app is created, you can now use the SFTP connector as a trigger/action for your Logic App. To do this, you need to:

1.	Create a new Logic App and choose the same resource group which has the SFTP connector:  
![][6]
2.	Open “Triggers and Actions” to open the Logic Apps Designer and configure your flow:  
![][7]
3.	The SFTP connector would appear in the “API Apps in this resource group” section in the gallery on the right hand side:  
![][8]
4.	You can drop the SFTP Connector API app into the editor by clicking on the “SFTP Connector”.

5.	You can now use SFTP connector in the flow. You can use the File retrieved from the SFTP trigger ("TriggerOnFileAvailable") in other actions in the flow.

	> [AZURE.IMPORTANT] The SFTP trigger "TriggerOnFileAvailable" deletes the retrieved file after processing the file.

6.	Configure the input properties for SFTP trigger as Follows:

	- **Folder Path** - Specify the path of the Folder from which Files needs to be retieved.
	- **The type of the file: text or binary** - Select the type of the file.
	- **File Mask** - Specify the file mask to be applied for retrieving files. '*' retrieves all the files in the specified folder.
	- **Exclude File Mask** - Specify the file mask to be applied for excluding files. If the "File Mask" property is also set, the Exclude File Mask will be applied first.


	![][9]  
	![][10]

7.	In the similar way you can use the SFTP actions in the flow. You can use the "upload File" action to upload a file to SFTP server. Configure the input properties for "Upload File" action as follows:

	- **Content** - Specifies the content of the file to be uploaded
	- **Content Transfer Encoding** - Specify none or base64
	- **File Path** - Specify the file path of the file to be uploaded
	- **Overwrite** - Specify "true" to overwrite the file if it already exists
	- **Append If Exists **- Specify "true" or "false". When set to "true", the data is appended to the file if it exists. When set to "false", the file is overwritten if it exists
	- **Temporary Folder** - If provided, the adapter will upload the file to the 'Temporary Folder Path' and once the upload is done the file will be moved to 'Folder Path'. The 'Temporary Folder Path' should be on the same physical disk as the 'Folder Path' to make sure that the move operation is atomic. Temporary folder can be used only when 'Append If Exist' property is disabled.

	![][11]  
	![][12]

## Do more with your Connector
Now that the connector is created, you can add it to a business workflow using a Logic App. See [What are Logic Apps?](app-service-logic-what-are-logic-apps.md).

>[AZURE.NOTE] If you want to get started with Azure Logic Apps before signing up for an Azure account, go to [Try Logic App](https://tryappservice.azure.com/?appservice=logic), where you can immediately create a short-lived starter logic app in App Service. No credit cards required; no commitments.

View the Swagger REST API reference at [Connectors and API Apps Reference](http://go.microsoft.com/fwlink/p/?LinkId=529766).

You can also review performance statistics and control security to the connector. See [Manage and Monitor your built-in API Apps and Connectors](app-service-logic-monitor-your-connectors.md).


<!-- Image reference -->
[1]: ./media/app-service-logic-connector-sftp/img1.PNG
[2]: ./media/app-service-logic-connector-sftp/img2.PNG
[3]: ./media/app-service-logic-connector-sftp/img3.PNG
[4]: ./media/app-service-logic-connector-sftp/img4.PNG
[5]: ./media/app-service-logic-connector-sftp/img5.PNG
[6]: ./media/app-service-logic-connector-sftp/img6.PNG
[7]: ./media/app-service-logic-connector-sftp/img7.png
[8]: ./media/app-service-logic-connector-sftp/img8.png
[9]: ./media/app-service-logic-connector-sftp/img9.PNG
[10]: ./media/app-service-logic-connector-sftp/img10.PNG
[11]: ./media/app-service-logic-connector-sftp/img11.PNG
[12]: ./media/app-service-logic-connector-sftp/img12.PNG
