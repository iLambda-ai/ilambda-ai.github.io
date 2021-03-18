## **Introduction**

----
EDA requires product related information and user realtime event data. EDA has a set of RESTful API to help importing the data.

----
## **Authentication**

----
EDA uses token for API authentication.

* Contact iLambda for registration.
* Use REST API to obtain token.

### **HTTP Request**
`POST https://openapi.ilambda.com/openapi/auth/token`

### **JSON Parameters**

Parameter    |   Required?   | Description
------------ | ------------- | ------------
username | Yes  | user registration name
password | Yes  | user registration password
duration | Yes  | token validity period in seconds

### **Sample Output**

```json
{
  "result": 1,
  "message": "Get token successfully.",
  "data": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyaW5mby"
}
```

----
