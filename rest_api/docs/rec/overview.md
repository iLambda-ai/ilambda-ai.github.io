
# **Recommendation API**

## **Data Integration API**

EDA Recommendation requires two kinds of data to provide high quality recommendation services:

- item metadata
- event log and impression log


There are a group of API for data uploading.
Before diving into the API details, you need to figure out what is your data collector server endpoint by following URL.

[Find out your data collector server]()

----
## **Item Metadata Data Upload API**

----

### Item metadata API


API          |   Description
------------ | -------------
/upload/ItemTable | upload item meta
/upload/ItemProperty | upload item attributes
/upload/CategoryTable | upload category information


----
## **Service API**

----

### Recommendation Service API


API          |   Description
------------ | -------------
/recommend/Detail | detail page recommendation
/recommend/Landing | landing page recommendation
/recommend/Activity | activity page recommendation

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
