# Handling errors

The `getResponseCode()` method of the `LineLoginResult` object returns one of the following response codes.

Response code | Description
-------------- | -------------
SUCCESS | The login was successful.
CANCEL | The login failed because the user canceled the login process.
AUTHENTICATION_AGENT_ERROR | The login failed because the user tapped the Cancel or Back button on the consent screen.
SERVER_ERROR | The login failed due to a server-side error.
NETWORK_ERROR | The login failed because the SDK could not connect to the LINE Platform.
INTERNAL_ERROR | The login failed due to an unknown error.
