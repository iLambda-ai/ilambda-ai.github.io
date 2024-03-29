# Token API


Most API in EDA requires access token for authentication purpose. User may fetch a token from EDA token API by specifying user name and password.
If you do not have your own user id and password assigned yet, please follow this link to create your account in ILAMBDA Cloud.

[Click Here To Create New Account](open_account.md)


----

## URL
Send a request to the following URL:
`https://openapi.ilambda.com/openapi/auth/token`

Must set HTTP header:  
`content: application/json`

## Method
`POST` - message body must be valid JSON format.

## JSON Parameters

Parameter    |   Required    | Description
------------ | ------------- | ------------
username | Yes  | user registration name
password | Yes  | user registration password
duration | Yes  | integer, token validity period in seconds

"duration" should be set wisely. In a environment that token would be exposed to external world, use a short duration like hundreds of seconds so that risk will be minimized even if token is leaked.
On the other hand, you may use much higher duration if it is in a secured environment.

## Sample Request

```shell
curl -X POST -H  "content-type:application/json" \
    -d '{
        "username":"test_user",
        "password":"password",
        "duration": 3600
        }' \
    "https://openapi.ilambda.com/openapi/auth/token"
```

## Sample Output

```json
{
  "result": 1,
  "message": "Get token successfully.",
  "data": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyaW5mby"
}
```

----

## How to pass token

Token are needed in both data upload and service API. No matter which API you are using, you can always pass token to EDA by using request parameter:

```token=xxxxxx```

