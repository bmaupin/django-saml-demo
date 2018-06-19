Minimal demo connecting python3-saml to a Shibboleth IdP

Based largely on code copied from [onelogin/python3-saml/demo-django](https://github.com/onelogin/python3-saml/tree/master/demo-django) with a few small changes:
- Configured to run on localhost
- Set `wantAssertionsEncrypted` to `true` (Shibboleth IdP encrypts assertion response by default)
- Change URLs to closer reflect Shibboleth IdP format
- Output decoded SAML response for testing/debugging

Tested with Django 2.0.6

### Instructions

1. [Install Django](https://docs.djangoproject.com/en/stable/intro/install/)

2. Install [python3-saml](https://github.com/onelogin/python3-saml)

        sudo apt install libxmlsec1-dev
        pip install python3-saml

3. Change SAML settings as needed ([saml/settings.json](saml/settings.json))
    1. Change the hostname in the IdP URLs
    2. Add the IdP signing cert

4. Create a cert/key pair and copy them to saml/certs/sp.crt and saml/certs/sp.key
    - These are needed for the Shibboleth IdP to encrypt the response assertion, which it will do by default unless [overridden in the relying party configuration](https://wiki.shibboleth.net/confluence/display/IDP30/SecurityConfiguration#SecurityConfiguration-SigningandEncryptionEnablement)

5. Configure the Shibboleth IdP as needed
    1. Add the SP metadata to the IdP
        - This can be retrieved from http://localhost:8000/metadata

    2. Configure attribute release to SP as desired

6. Start the app

        python manage.py runserver
