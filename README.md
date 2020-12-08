# teams-health-feature-monitoring
Microsoft Teams Service Health and Message Center Notifications as Teams posts and to SharePoint lists.


## Table of Contents

- [teams-health-feature-monitoring](#teams-health-feature-monitoring)
  - [Table of Contents](#table-of-contents)
  - [About The Project](#about-the-project)
    - [Built With](#built-with)
  - [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
      - [1. Clone the repo or download the files directly](#1-clone-the-repo-or-download-the-files-directly)
      - [1. Create an App Registration in Azure AD](#1-create-an-app-registration-in-azure-ad)
      - [2. Create a SharePoint site](#2-create-a-sharepoint-site)
      - [3. Import the SharePoint lists](#3-import-the-sharepoint-lists)
      - [4. Import the Power Automate flow](#4-import-the-power-automate-flow)
      - [5. Adjust the values in the Power Automate](#5-adjust-the-values-in-the-power-automate)
  - [Usage](#usage)
  - [Roadmap](#roadmap)
  - [Contributing](#contributing)
  - [License](#license)
  - [Contact](#contact)


## About The Project

The project includes a simple Power Automate solution to stay informed about the Microsoft Teams Service Health status and upcoming changes to the service that may require administrator or end-user attention.  

![Solution Image](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/main_img_new.png)

The flow will fetch every **20 Minutes** the latest updates from the Office 365 Service Health Status and the Message Center using the Office 365 Management API and post them to Teams (if required) and store the information to SharePoint lists.

*The solution is designed for Microsoft Teams but can also be used for all other Office 365 services by simply changing the filters inside the flow.*

### Built With

* [Power Automate](https://us.flow.microsoft.com/)
* SharePoint Online Lists

## Getting Started

To get a local copy up and running follow these simple steps.

### Prerequisites

The solution require an Office 365 subscription including the following:

- Microsoft Teams license
- Power Automate license (Premium Connector)
- SharePoint and OneDrive license
- PnP PowerShell Module (SharePoint Online)
- Access to Azure AD to create App Registration

### Installation

#### 1. Clone the repo or download the files directly

Clone the repo:

```sh
git clone https://github.com/tobiheim/teams-health-feature-monitoring.git
```

#### 1. Create an App Registration in Azure AD

   First open the Azure AD Portal (https://aad.portal.azure.com) and select **App registrations**.  

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/azure_portal.png)

   Create a new registration:  

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar1.png)

   Provide a name to your new app and select the supported account type as shown in the screenshot below. Now you can register the app.

   ![Name and register App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar2.png)

   Also copy the **Application ID** and the **Tenant ID** from the overview section.

   ![Copy app id and tenant id](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar11.png)

   Next you need to add permissions to your app registration.

   ![View permissions](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar3.png)

   Select **Add a permission**

   ![Add permissions](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar4.png)

   Select **Office 365 Management APIs**

   ![Select Mgmt API](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar5.png)

   Next select **Application permissions**

   ![Select app permissions](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar6.png)

   Select the permissions listed in the screenshot below:

   ![Select the required permissions](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar7.png)
  
   After selecting the permissions, click **Add permission**.

   Don't forget to grant admin consent for your organization.

   ![Grant admin permissions](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar8.png)

   As last step you need to create a client secret for your app.
   **Note:** It is up to you what name and expiration time you select based on your requirements.

   ![Create client sec](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar9.png)

   Make sure to copy the client secret. You will need it later.

   ![Copy client sec](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar10.png)  

#### 2. Create a SharePoint site

   To create a new SharePoint page navigate to SharePoint Online using the menu in the top right corner.

   ![Navigate to SP](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp_hamb1.png)  

   ![Create SP site](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp1.png)

   Select a Modern Team Site and add the required members and owners.

   ![Select Teams site](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp2.png)

   **Note:** You can also use a already existing modern SharePoint site.  

   Copy the URL of the SharePoint site. You will need it later.

   ![Create SP site](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp_url.png)  

#### 3. Import the SharePoint lists

   After the new site is created you can apply the list template.
   The template includes two lists for the service health and the message center notifications.

   Make sure to install the PnP PowerShell module.  
   https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps

   `Install-Module SharePointPnPPowerShellOnline`

   `Connect-PnPOnline -Url "https://{Vanity domain host name}.sharepoint.com/sites/{Your site name}`

   ![Connect to SP site](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp3.png)

   The list template is part of this repo. You can apply it using the following cmdlet.

   `Apply-PnPProvisioningTemplate -Path "C:\Temp\SP_Lists_Template_TeamsHealthandFeatureUpdates_v1.0.xml" -Handlers Lists`

   ![Apply the SP template](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp4.png)

   After you applied the template you should see the following newly created lists. If not, please refresh the browser.

   ![Verify the lists](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp5.png)

#### 4. Import the Power Automate flow  

   Navigate to the Power Automate portal (https://us.flow.microsoft.com) and go to **My flows**.

   Select **Import** to add the flow template to your environment.

   ![Select flow import](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa1.png)

   When you import the flow you need to make sure to replace the existing connections as shown below:

   ![Replace the connections](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa2.png)

   More details how to replace the connections can be found here:  
   https://docs.microsoft.com/en-us/power-automate/add-manage-connections  
   https://docs.microsoft.com/en-us/power-automate/create-team-flows#modify-a-connection  
   
   The included connections are used for the following reasons:  

|**Connections** |Description  |
|---------|---------|
|OneDrive for Business    |This connector is used to fetch the product logo files from OneDrive.        |
|SharePoint Online     |This connector is used to connect, read and write to the SharePoint lists.         |
|Microsoft Teams     |Required to post messages to a Teams channel.        |
|Content Conversion    |Required to convert HTML to plain text.         |  

</br>

   After you replaced all the connections the import screen should look like this:

   ![flow import view](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa3.png)

   Finally you can import the flow to your environment.

   ![final view after flow import](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa4.png)

   ![flow successful import](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa5.png)

#### 5. Adjust the values in the Power Automate  

   As every last step you need to adjust the OneDrive, SharePoint and Teams connections inside the flow.

   First you need to upload the logos you want to use to a OneDrive for Business location and add the path to the following steps.  
   ![Logo path](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa7.png)

   **Note:** The images in the Teams post will be displayed as long as the link to it is valid. It will expire over time. You can use a variable that points to any kind of web server as a replacement for the OneDrive Thumbnail approach.

   Next you need to adjust the app registration information as showing in the following example:  
   ![Logo path](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa8_new.png)

   You need to adjust 6 times the SharePoint steps *(Make sure to select the correct list)*.  

   The flow is divided into two trees, each to control a specific aspect of the monitoring:  
    a. **Left hand side tree** to monitor a product health status (in this case Microsoft Teams and SfBO)  
    b. **Right hand side tree** to monitor the Message Center Notifications

   The flow is shipped with two SharePoint lists that you imported earlier, in the Service Health Status side of the flow-tree, you need to point all SharePoint lists flow steps to Service Health Notification SharePoint List, the same for the Message Center Notification flow-tree but by pointing to the Message Center Notification SharePoint list instead.

   ![Logo path](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa_tree.png)   

   ![Logo path](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa9.png)

   Last but not least you need to adjust the Teams steps to your channel (3 times).  
   ![Logo path](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa10.png)

   **Note:** You could separate the incident posts from the message center posts into different channels if needed.

   **Let's go! Try it.**  
## Usage  

**Service Incidents:**  
The flow will check for any Microsoft Teams or Skype for Business Online message that are classified as **Service Degradation** and store this information to a SharePoint list.

![Incident List](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/usage1.png)

As you can see the list template is configured with **conditional formatting** to highlight every degradated (red) and restored (green) service.

In addition to the list the flow will also post directly to a defined Teams channel. This way the admins stay informed without the need of checking the service health section in the Office 365 admin center all the time or subscribe to the notification mails that spams their inbox.

Here an example of a service degradation post:  
![Incident Post](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/service_deg.png)


**Note:** The degradation posts include more details then the restored post (degradation status and description).

The admin can directly access the SharePoint item using the button "Go to item" in the post to see more details.

**Feature Updates:**  
The message center notification follows the same logic. Every Teams related entry will be stored in a SharePoint list.
The list also includes pre-defined **conditional formatting** to highlight every entry that is tagged a "Plan for Change".

Here an example:  
![MC List](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/usage3.png)

Furthermore any entry with the category **Plan for Change** will be posted to Teams as "Call to Action".

Example post:  
![MC List](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/usage4.png)


## Roadmap  

The following item are on the Roadmap:

- Add a planner step for any "Call to Action" Message Center notifications to follow up with these items
- Add samples for each Office 365 workload and the required filters
- Image location alternative using Azure Storage

See the [open issues](https://github.com/tobiheim/teams-health-feature-monitoring/issues) for a list of proposed features (and known issues).

## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Contact

Tobias Heim - [@saibothe](https://twitter.com/saibothe)  

**Thanks a lot to:**  
Mostafa Eid [@Lyncdude](https://twitter.com/Lyncdude) for contributing to the documentation.