
# **Detail Page API**

#### URL
`/recommend/detail`

#### Method
`GET`

#### **Arguments**

Parameter  |   Description
-------| -------------
token	| Authentication token
userId	| CookieId
itemId	| Product Id
offset	| The start position of return results, 0 based
limit	| Total number of return results

#### Sample Request
`/recommend/Detail?userId=25d044b768cf84ca&token=12232&itemId=14912440&offset=1&limit=3`

#### **Sample Output**

```json
{
    "result": 0,
    "message": "kOk",
    "meta": {
      "traceid": “ILAMBDARSDETAIL",
      "totalItems": 3535
    },
    "data": {
      "itemIds": [
        "14184251",
        "16361008",
        "16261159"
      ],
      "scores": [
        0.10418500006198883,
        0.07089799642562866,
        0.040778998285532
      ]
    }
}
```

----
