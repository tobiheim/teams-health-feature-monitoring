# teams-health-feature-monitoring
Microsoft Teams Service Health and Message Center Notifications to SharePoint List and Teams


## Table of Contents

- [teams-health-feature-monitoring](#teams-health-feature-monitoring)
  - [Table of Contents](#table-of-contents)
  - [About The Project](#about-the-project)
    - [Built With](#built-with)
  - [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
      - [1. Clone the repo](#1-clone-the-repo)
  - [Usage](#usage)
  - [Roadmap](#roadmap)
  - [Contributing](#contributing)
  - [License](#license)
  - [Contact](#contact)

## About The Project

[![Product Name Screen Shot][product-screenshot]](https://example.com)

The project includes a simple Power Automate solution to stay informated about the Microsoft Teams Service Health status and upcoming changes to service that may require admininstrator attention. The flow will fetch every 20 Minutes the latest updates of the Office 365 Service Health and the Message Center using the Office 365 Management API. 

### Built With

* [Power Automate](https://us.flow.microsoft.com/)
* SharePoint Online Lists

## Getting Started

To get a local copy up and running follow these simple steps.

### Prerequisites

The solution require an Office 365 subscription including the following:

- Microsoft Teams license
- Power Automate license
- SharePoint and OneDrive license
- Access to Azure AD
- SharePoint Online PnP PowerShell Module


### Installation

#### 1. Clone the repo
```sh
git clone https://github.com/tobiheim/teams-health-feature-monitoring.git
```
1. Create an App Registration in Azure AD

   First open the Azure AD Portal (https://aad.portal.azure.com) and select **App registrations**.

   Create a new registration:
   
   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar01.png)

   Provide a name to your new app and register it.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar02.png)

   Next you need to add permissions to your app registration.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar03.png)

   Select **Add a permission**

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar04.png)

   Select **Office 365 Manangement APIs**

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar05.png)

   Next select **Application permissions**

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar06.png)

   Select the permissions listed in the screenshot below:

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar07.png)
  
   Don't forget to grant admin consent for your organisation.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar08.png)

   As last step you need to create a client secret for your app.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar09.png)

   Make sure to copy the secrect. You will need it later.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar10.png)

   Also copy the **Application ID** and the **Tenant ID**.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/ar11.png)

2. Create a SharePoint site or a Team
   
   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp01.png)

   Select a Modern Team Site and add the required members and owners.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp02.png)

   **Note:** You can also use a already existing modern SharePoint site. 

3. Import the SharePoint lists
   
   After the new site is created you can apply the list template.
   The template includes to lists for the service health and the message center notifications.

   Make sure to install the PnP PowerShell module.  
   https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-pnp/sharepoint-pnp-cmdlets?view=sharepoint-ps

   `Install-Module SharePointPnPPowerShellOnline`

   `Connect-PnPOnline -Url "https://m365xXXXXXX.sharepoint.com/sites/TeamsHealthFeatureMonitoring"`

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp03.png)

   The list template is part of this repo. You can apply it using the following cmdlet.

   `Apply-PnPProvisioningTemplate -Path "C:\Temp\SP_Lists_Template_TeamsHealthandFeatureUpdates_v1.0.xml" -Handlers Lists`

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp04.png)

   After you applied the template you should see the following newly created lists.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/sp05.png)

4. Import the Power Automate flow
   
   Navigate to the Power Automate portal (https://us.flow.microsoft.com).
   
   Select Import to import the template in this repo.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa01.png)

   When you import the flow you need to make sure the replace the existing connections as shown below:

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa02.png)

   After you replaced all the connections the import screen should look like this:

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa03.png)

   Finally you can import the flow to your environment.

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa04.png)

   ![Create App Registration](https://www.saibot-lab.com/GitHub/teams_health_feature_monitoring/pa05.png)

5. Adjust the values in the Power Automate



## Usage

<!-- Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources. -->




## Roadmap

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

