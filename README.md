# BlueButton 2.0 Application List
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

- `software_id`: A Universally Unique Identifier
      (UUID) assigned by the client developer or software publisher.
- `name`: Application Name
- `client_uri`: If present, the server SHOULD display this URL to the end-user in
      a clickable fashion.  It is RECOMMENDED that clients always send
      this field.  The value of this field MUST point to a valid web
      page.  The value of this field MAY be internationalized.
- `logo_uri`: a link to a 256x256 jpg image of the application logo.
- `logo_allowed_use`: identifies restrictions on the use of the logo. Data Holder use only, Restricted use or Public Use. Logos may only be published by organizations who are not the publisher of the list if the logo_allowed_use is set to "public use".
- `tos_uri`: Link to the application's terms of service.
- `privacy_uri`: Link to the application's privacy policy.
- `contacts`: Array of strings representing ways to contact people responsible
      for this client, typically email addresses.  The authorization
      server MAY make these contact addresses available to end-users for
      support requests for the client. 
- `email`: contact email for the application. 
- `phone_number`: phone number for application help desk support.
- `jwks_uri`: URL string referencing the client's JSON Web Key (JWK) Set
     [RFC7517] document, which contains the client's public keys.  The
      value of this field MUST point to a valid JWK Set document.  These
      keys can be used by higher-level protocols that use signing or
      encryption.
      - `jwt` : Array of strings containg valid JWK, JWS, or JWE.
- `description`: a plain text description of the application. 1024 characters.
- `labels`: A list of labels that may be used to categorize the application in the publishers application lists.


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
      "software_id": "uuid",
      "client_uri": "https://domain,tld/path_to/application_url/",
      "logo_uri": "https://path_to_logo_url/logo_filename.jpg",
      "logo_allowed_use": ["Data Holder Only", "restricted", "public use"],
      "tos_uri": "https://path_to/terms_of_service",
      "policy_uri": "https://path_to/privacy_policiy",
      "contacts" ["Support@organization.email","https://path_to/support/landing_page", "+1555554HELP", "123 Pleasant St. Anywhwere, WV 26505 USA"]
      "email": "Support@organization.email",
      "jwks_uri": "Optional. For support of highjer level signing protocols.",
      "phone_number": "support phone number",
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


