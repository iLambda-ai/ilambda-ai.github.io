
# **Impression API**

#### URL
`/upload/impression`

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

#### Sample input
```json
{
    "events": [
        {
           "cookie_id": "3872edfe33432",
            "user_id": "edacloud",
            "event_key": “imp",
            "target_id": “323333333",
            "section": "detail",
            "context": “132342342@12”
        },
        {
           “cookie_id": "1942234444",
            "event_key": “imp",
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
