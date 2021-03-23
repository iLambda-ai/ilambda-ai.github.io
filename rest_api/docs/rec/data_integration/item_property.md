
# **Item Property API**

#### URL
`/upload/ItemProperty`

HTTP header: `content: application/json`

#### Method
`POST`

#### **JSON Parameters**

Field  |   Type   | Required | Description
-------| ------------- | ------------ | ----------
item\_id	| String	| yes | Unique id to indicate the item, unique per site.
site\_id	| String	| yes | Support mutiple sites. If only one site, set to 1.
label\_id	| String	| yes | Property ID, e.g Color.
label\_value	| String	| yes | Property Value ID, e.g Red.

#### Sample input
```json
{
  "items": [
    {
      "item_id": "123123111",
      "site_id": "0",
      "label_id":"COLOR",
      "label_value": "RED"
    },
    {
      "item_id": "123123222",
      "site_id": "0",
      "label_id":"SIZE",
      "label_value": “LARGE"
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
