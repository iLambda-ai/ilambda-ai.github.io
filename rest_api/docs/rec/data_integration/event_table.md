
# **Event API**

#### URL
`/upload/event`

HTTP header: `content: application/json`

#### Method
`POST`

#### **JSON Parameters**

Field  |   Type   | Required | Description
-------| ------------- | ------------ | ----------
event\_id	| String	|  | Unique id to indicate one event. System assigns one unique id if empty.
site\_id	| String	|  | Support mutiple sites. If only one site, set to 1.
cookie\_id	| String	|  | Cookie Id of current event.
user\_id	| String	|  | User Id of current event. Leave it null if not available.
event\_key	| String	| yes | Event types: <br> - click <br> - addCart <br> - addWish <br> - order <br> - orderPay <br> - imp <br> - pageView
target\_id	| String	| yes | Item Id or order Id in terms of the context.
server\_time	| Integer	| | Event time receive at the server. (unix timestamp). All events use same timezone.
section	| String | |	Refer to the source of the events. e.g. landing, detail, list etc.
context |	String |	| Context information for section.
algorithm	| String	| yes | EDA algorithm source tracecode in order to assist analysis.
page\_id	| String	| | Extra information about current page. Optional.
prev\_page\_id	| String	| | Extra information about previous page. Optional.
price	| Number	| | Event price, valid for addCart, order and imp events. Optional
currency	| String	| | Currency. e.g. USD, CNY.
item\_count	| Integer	|  | The total item number of addCart/order.
channel	| String	 | | Event source channel. e.g mobile, pc, h5 and apple etc.

##### Section
```
Section attribute specify the source of the event.
It could be one of the following:
    - landing
    - detail
    - list
    - flashsale
    - activity
    - search
    - cart: shopping cart recommendation
    - other
Section field is valid for click, addCart, imp, other events.
```

##### Context
```
Context attribute provides extra information besides section.
    - landing: the actual position for landing section
    - detail: the position of main item id for detail section
```

#### Sample input
```json
{
    "events": [
        {
           "cookie_id": "3872edfe33432",
            "user_id": "edacloud",
            "event_key": "addCart",
            "target_id": “323333333",
            "section": "detail",
            "context": “132342342@12”,
            "algorithm": “ILAMBDARSDNNDETAIL",
            "price": 13.91,
            "item_count": 1
        },
        {
            "site_id": "0",
            “cookie_id”: "1942234444",
            "event_key": "click",
            "server_time": 1583853406,
            "target_id": "1111"
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
