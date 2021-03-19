
# Recommendation Data Upload

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


API          |   Purpose
------------ | ------------- 
/upload/ItemTable | upload item meta
/upload/ItemProperty | upload item attributes
/upload/CategoryTable | upload category information

----
