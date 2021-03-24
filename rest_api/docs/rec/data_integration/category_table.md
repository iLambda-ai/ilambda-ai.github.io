
# **Category Table API**

#### URL
`/upload/CategoryTable`

HTTP header: `content: application/json`

#### Method
`POST`

#### **JSON Parameters**

Field  |   Type   | Required | Description
-------| ------------- | ------------ | ----------
cat\_id	| String	| yes | Unique id to indicate the category.
parent\_id	| String	| yes | Parent category id.
cat\_name	| String	| yes | Category name and could be null value.

#### Sample input
```json
{
  "items": [
    {
      "cat_id": "1139",
      "site_id": "0",
      "parent_id":"1135",
      "cat_name": "man cloth"
    },
    {
      "cat_id": "11381",
     "parent_id":"1134",
      "cat_name": "man shorts"
    }
  ]
}
```

#### **Sample Output**

##### **Success**
```json
{
  "status": "OK",
  "result": 1
}
```

##### **Error** - `Invalid Token`
```json
{
  "errors": {
    "message": "invalid signature",
    "error": {
      "status": 401,
      "name": "UnauthorizedError",
      "message": "invalid signature",
      "code": "invalid_token"
    }
  }
}
```

##### **Error** - `Data Format Error`
```json
{
  "errors": {
    "message": "json not comply with schema: 0:
                instance.items[0] requires property \"item_id\"\n",
    "error": { }
  }
}
```

----
