
# **Item Table API**

#### URL
`/upload/ItemTable`

HTTP header: `content: application/json`

#### Method
`POST`

#### **JSON Parameters**

Field  |   Type   | Required | Description
-------| ------------- | ------------ | ----------
item\_id	| String	| yes | Unique id to indicate the item, unique per site.
site\_id	| String	| yes | Support mutiple sites. If only one site, set to 1.
spu\_id	| String	|  | Different item from different site can map to one SPU ID. Could be null if not available.
cat\_id	| String	| yes | Leaf node category id.
item\_name	| String	| yes | Name
item\_desc	| String	| yes | Item description, could be null.
is\_onsale	| Integer	| | - 0: Discontinued <br> > - 0: inventory number
onsale\_time	| Integer | |	When product is available online. (Unix timestamp)
original\_price |	Number |	| Item original price.
price	| Number	| yes | Item price.
currency	| String	| | Currency. e.g. USD, CNY.
add\_time	| Integer	| | When product add into stock. (unix timestamp)
last\_update	| Integer	| | Most recent access timestamp. eg. 1500000000
season	| Integer	| | Product season. <br> - 0: default <br> - 1: spring <br> - 2: summer <br> - 3: fall <br> - 4: winter <br> - 5:  spring and summer <br> - 6: summer and fall <br> - 7: spring and winter <br> - 8: summer and fall <br> - 9: summer and winter <br> - 10: fall and winter
img\_url	| String	| yes | Image URL，use ";" to separate multiple image pathes. The first one is the main image.
thumb\_url	| String	 | | Thumbnail image URL，use ";" to separate multiple image pathes. The first one is the main image. 
item\_url	| String	 | | Product URL link.

#### Sample input
```json
{
  "items": [
     {
      "item_id": "123123111",
      "site_id": "big",
      "cat_id": "1135",
      "item_name": "Men Sports Sweater",
      "item_desc": "description",
      "is_onsale": 1,
      "original_price": 35.8,
      "price": 25.8,
      "currency": "USD",
      "add_time": 1583853406,
      "season": "1",
      "img_url": "http://testtest.com/ttt"
    },
    {
      "item_id": "123123222",
      "site_id": "small",
      "cat_id": "1135",
      "item_name": "Women's Sports Sweater",
      "item_desc": "description",
      "is_onsale": 1,
      "original_price": 55.8,
      "price": 35.8,
      "currency": "USD",
      "add_time": 1583853806,
      "season": "1",
      "img_url": "http://testtest.com/ttt"
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
