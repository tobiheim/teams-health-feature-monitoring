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

1. Clone the repo
```sh
git clone https://github.com/tobiheim/teams-health-feature-monitoring.git
```
1. Create a SharePoint site or a Team


**Note:** You can also use a already existing team or SharePoint site. 

1. Create an App Registration in Azure AD

2. Import the SharePoint lists

3. Import the Power Automate flow

4. Adjust the values in the Power Automate



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

