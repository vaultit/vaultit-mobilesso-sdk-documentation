# Viewing the VaultITMobileSSOFramework documentation

Checkout the repository and open the index.html from the OS specific folder.

# Getting started with VaultITMobileSSOFramework

One key component of the Vaultit ecosystem is the Gluu SSO service, which acts as an OpenID Connect Provider for Relying Parties/clients. The relying parties use OpenID Connect Provider for authenticating users and then can use the access token to make authorized requests to the API backends.

To get started with using the Vaultit SSO system, you must register a client (see below information about registration) and choose one contact person for acting as the main contact point. After registration, see separate guides for integrating the VaultITMobileSSOFramework for Android and iOS applications.

# Registration

To register a client, you may contact the Tilaajavastuu or ID06 API teams. The email subject should have "Client registration for Vaultit SSO" as a subject and should include the following information:

    - Environments that will be used: ID06 and/or Tilaajavastuu
    - Name of the company developing application
    - Name of the contact person
    - Email address of the contact person
    - Mobile phone number of the contact person
    - Name of the client/relying party
    - Login redirect URLs for the application (these depend on the OS, see OS specific documentation for details)
    - Logout redirect URLs for the application (these depend on the OS, see OS specific documentation for details)
    - ID token signing algorithm (defaults to `RS512`)
    - If need access to virtual card backend-service (see more information below)
    
The redirect urls must start with https or with prefix for mobile application's custom namespace. When registration is complete, the client id and secret for connecting to the OpenID Connect provider are sent to the contact person via secure mail. The client is given default scopes (openid and profile).

# Beta environments

Tilaajavastuu and ID06 Beta environments have OpenID Connect providers for authentication. List of the OpenID Connect endpoints and supported configuration values are available in the OpenID Discovery Endpoint, the URL is below. Beta environments currently support three different authentication methods, Swedish Bank ID (`acr_values=bankid`), Finnish Tupas (`acr_values=tupas`) and general username/password (no `acr_values` parameter provided).

In Tilaajavastuu Beta environment, the OpenID Connect Discovery URL is available at: `https://auth.beta.tilaajavastuu.fi/oxauth/.well-known/openid-configuration`
In ID06 Beta environment, the OpenID Connect Discovery URL is available at: `https://int-id06beta.id06.se/oxauth/.well-known/openid-configuration`

Several backends are developed to offer service API's to the application providers. This document describes the integration against the virtual card backend.

# Virtual card backend

To access more detailed data about the authenticated user, you can use virtual card backend service: 

* In Tilaajavastuu Beta environment: `https://vc.beta.tilaajavastuu.fi/`.
* In ID06 Beta environment: `https://vcbeta.id06.se/`.

The service has the following request endpoints (examples from Tilaajavastuu Beta environment):
  
    - GET https://vcalpha.id06.se/cards Lists all cards issued to the authenticated user.
    - GET https://vcalpha.id06.se/html/<card id>/front Returns the front side of the card in HTML format.
    - GET https://vcalpha.id06.se/html/<card id>/back Returns the back side of the card in HTML format.
    - GET https://vcalpha.id06.se/visual/<card id>/matrix Returns the card number as a data matrix.
    - GET https://vcalpha.id06.se/visual/<card id>/qrcode Returns the card number as a QR code.
    - GET https://vcalpha.id06.se/person Returns the basic profile information of the authenticated user.
    - GET https://vcalpha.id06.se/person/photo Returns the profile photo of the authenticated user.
    - GET https://vcalpha.id06.se/jwks Returns the JSON web keys that can be used for QR code validation.
    
Requests must have authorization http header with access token in it, eg. `"Authorization: Bearer eyJpc3MiOiJodHRwczovL25vcm..."`.

Additional virtual card backend documentation can be asked from Tilaajavastuu or ID06 API teams.

# Test data 

In Tilaajavastuu Beta environment you may register your test users through the portal: `https://portal.beta.tilaajavastuu.fi`

In ID06 Beta environment the test users must be registered separately. Contact ID06 API team and put "Test user registration" as a subject. For each test user the following information must be provided:
  
    - Test user last and first name
    - Email
    - Username
    - Optional Swedish identity number for BankID testing.
    - Company affiliation
    
After the user is created the password for the account will be delivered via email.

# Known issues

    - Single sign on session checking is not working in iOS 11.

Full list of known issues can be found from Vaultit Confluence.

# Contact
If you have any questions or need guidance, you can contact the Tilaajavastuu or ID06 API teams.


