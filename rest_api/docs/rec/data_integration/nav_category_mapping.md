
# **Nav Category Mapping API**

#### URL
`/upload/NavCategoryMapping`

HTTP header: `content: application/json`.

#### Method
`POST`

#### **JSON Parameters**

Field  |   Type   | Required | Description
-------| ------------- | ------------ | ----------
item\_id	| String	| yes | Unique id to indicate the item.
site\_id	| String	| yes | Support mutiple sites. If only one site, set to 1.
cat\_id	| String	| yes | Unique id to indicate the category.

#### Sample input
```json
{
  "items": [
    {
      "item_id": "1134",
      "site_id": "0",
      "cat_id":"1135"
    },
    {
      "item_id": "1130",
     "cat_id":"1134"
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
