
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


### **Item Table API**

#### URL
`/upload/ItemTable`

#### Method
POST
#### **JSON Parameters**

Field  |   Type   | Required | Description
-------| ------------- | ------------ | ----------
item_id	| VARCHAR	| yes | 商品唯一ID, unique per site.主键
site_id	| VARCHAR	| yes | 商品站点ID, 主键。默认值为0，如果只有一个站点无需传入。
cat_id	| VARCHAR	| yes | 后台叶子类目id
item_name	| VARCHAR	| yes | 商品名称 
item_desc	| VARCHAR	| yes | 商品描述 
is_onsale	| INT	| | 0: 商品下架或者售罄, > 0 商品的在售（库存件数）
onsale_time	| BIGINT | |	Unix timestamp 商品的开始售卖时间点
original_price |	FLOAT |	| 原价
price	| FLOAT	| yes | 售价
currency	| VARCHAR	| | 货币类型，如USD, CNY, 如果只有一个币种可不填
add_time	| BIGINT	| | 商品上传的时间戳，unix timestamp，如1500000000
last_update	| BIGINT	| | 商品最后一次状态变化的时间戳，.eg. 1500000000
img_url	| VARCHAR	| yes | Image URL，可以包含多个链接，用逗号分隔，第一个是主图链接
thumb_url	| VARCHAR	 | | 商品缩略图 URL，可以包含多个链接，用逗号分隔，第一个是主图链接
item_url	| VARCHAR	 | | 商品原始链接，链接到商品详情页面。

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
