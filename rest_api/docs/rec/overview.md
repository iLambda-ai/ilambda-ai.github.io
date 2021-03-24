
# Recommendation API

To unleash the power of EDA personalization system, user must:
1. upload necessary data to EDA
2. fetch the personalized recommendation result from EDA

You may do this through a set of REST APIs provided by EDA.

## Prerequisites

To access the API system shipped with EDA, you need to make sure:
1. You have already get customer account ID and password by following [this link](../open_account.md).
2. You already get the access token by following [this link](../token.md).
3. Figure out the server names to talk to by following [this link](../server_names.md).
   
The 2nd step you may do it manually for in code.


## Data Integration API

EDA requires two kinds of data to provide high quality recommendation services:

- item metadata such as attributes, category and properties
- event log and impression log in a stream manner



Before diving into the API details, you need to figure out what is your data collector server endpoint by following URL.

[Find out your data collector server](../server_names)

For example if you get an account ID "foo", you should send request to the following server address:

```https://data-collector.foo.cloud.ilambda.com```

Don't forget to attach the API endpoint at the end of the server. For example to upload event, the final URL would be like:


```https://data-collector.foo.cloud.ilambda.com/upload/event```

----

### Item metadata API


API          |   Description
------------ | -------------
[/upload/ItemTable](data_integration/item_table.md) | upload item meta
[/upload/ItemProperty](data_integration/item_property.md) | upload item attributes
[/upload/CategoryTable](data_integration/category_table.md) | upload category information

### Event and Impression API


API          |   Description
------------ | -------------
[/upload/event](data_integration/event_table.md) | upload user events
[/upload/impression](data_integration/impression_table.md) | upload impression data

----
----
## Service API

EDA service API are designed to export recommendation results. Those API are hosted by EDA Online Serving service in CCU. You may find more details about CCU [from this link](../server_names.md).

Customer with account ID "foo" will find out that the URL to send request will be something like: "https://eda.foo.cloud.ilambda.com".

Don't forget to attach the API endpoint to the end. Let's make landing API as an example, for user "foo" the final URL will be like:
```https://eda.foo.cloud.ilambda.com/recommend/Landing```

### Recommendation Service API

API          |   Description
------------ | -------------
[/recommend/Detail](api/detail.md) | detail page recommendation
[/recommend/Landing](api/landing.md) | landing page recommendation
[/recommend/Activity](api/activity.md) | activity page recommendation

----
### HTTP Status Code


Code         |   Description
------------ | -------------
200 | OK
400 | Parameter Error
401 | Invalid Token
402 | Expired Token
404 | ID not exist/no result

----
