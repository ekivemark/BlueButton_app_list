# BlueButton_app_list
Purpose: JSON schema and api specification to publish a list of approved blue button 2.0 consumer applications that connect to a data holder's HL7 FHIR endpoint.

## API Endpoint

https://domain.tld/.well-known/applications

## Access

Open

## Scope

Identify production approved applications only.

The api is not intended to identify sandbox or test applications from a development environment. This is only to document the applications that have been provided OAuth2.0 credentials to access user information in a production environment.

## Json schema

The Schema has the following elements:

- A count of applications included in the results section.
- Paging information: Next / Previous (if more than one page of results.
- Publisher information: Organization, contact, endpoint and logo information.
- Results: A list of applications.

Within the Results list the following elements are included:

- Name: Application Name.
- Website url: Link to website information about the application.
- logo url: a link to a 256x256 jpg image of the application logo.
- logo_allowed_use: identifies restrictions on the use of the logo. Data Holder use only, Restricted use or Public Use. Logos may only be published by organizations who are not the publisher of the list if the logo_allowed_use is set to "public use".
- tos_uri: Link to the application's terms of service.
- policy uri: Link to the application's privacy policy.
- support uri: Link to the support page for the application (optional).
- support email: contact email for the application. 
- support phone number: phone number for application help desk support.
- description: a plain text description of the application. 1024 characters.
- labels: A list of labels that may be used to categorize the application in the publishers application lists.

``` json
{
  "count": nnn,
  "next": "https://domain.tld/.well-known/applications?page=n",
  "previous": "https://domain.tld/.well-known/applications",
  "publisher": {
      "organization": "name of organization",
      "contact_email": "application_manager@email.example",
      "api_endpoint": "https://path_to/api_endpoint",
      "logo_url": "https://path_to/logo_url",
  },
  "results": [
{
      "name": "application_name",
      "website_uri": "https://domain,tld/path_to/application_url/",
      "logo_uri": "https://path_to_logo_url/logo_filename.jpg",
      "logo_allowed_use": ["Data Holder Only", "restricted", "public use"],
      "tos_uri": "https://path_to/terms_of_service",
      "policy_uri": "https://path_to/privacy_policiy",
      "support_url": "https://path_to/support/landing_page",
      "support_email": "Support@organization.email",
      "support_phone_number": "support phone number",
      "description": "1024 character plain text application description",
      "labels": [
        {
          "name": "Organize \u0026 Share",
          "slug": "organizeandshareclaims",
          "description": "Organize \u0026 share medical information \u0026 claims"
        }
      ]
    },      
]
}
```


