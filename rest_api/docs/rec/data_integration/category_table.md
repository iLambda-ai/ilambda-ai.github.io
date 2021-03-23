
# **Item Table API**

#### URL
`/upload/ItemTable`

#### Method
`POST`
#### **JSON Parameters**

Field  |   Type   | Required | Description
-------| ------------- | ------------ | ----------
item\_id	| VARCHAR	| yes | Unique id to indicate the item, unique per site.
site\_id	| VARCHAR	| yes | Support mutiple sites. If only one site, set to 1.
spu\_id	| VARCHAR	|  | Different item from different site can map to one SPU ID. Could be null if not available.
cat\_id	| VARCHAR	| yes | Leaf node category id.
item\_name	| VARCHAR	| yes | Name
item\_desc	| VARCHAR	| yes | Item description, could be null.
is\_onsale	| INT	| | 0: Discontinued , > 0 inventory number.
onsale\_time	| BIGINT | |	When product is available online. (Unix timestamp)
original\_price |	FLOAT |	| Item original price.
price	| FLOAT	| yes | Item price.
currency	| VARCHAR	| | Currency. e.g. USD, CNY.
add\_time	| BIGINT	| | When product add into stock. (unix timestamp)
last\_update	| BIGINT	| | Most recent access timestamp. eg. 1500000000
season	| INT	| | Product season. 0. default, 1. spring, 2. summer, 3, fall, 4, winter, 5, spring and summer, 6. summer and fall, 7. spring and winter, 8. summer and fall, 9. summer and winter, 10. fall and winter.
img\_url	| VARCHAR	| yes | Image URL，use ";" to separate multiple image pathes. The first one is the main image.
thumb\_url	| VARCHAR	 | | Thumbnail image URL，use ";" to separate multiple image pathes. The first one is the main image. 
item\_url	| VARCHAR	 | | Product URL link.

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

```json
{
  "result": 1,
  "message": "Get token successfully.",
  "data": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyaW5mby"
}
```

----
