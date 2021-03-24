
# **Activity Page API**

#### URL
`/recommend/Activity`

#### Method
`GET`

#### **Arguments**

Parameter  |   Description
-------| -------------
token	| Authentication token
userId	| CookieId
offset	| The start position of return results, 0 based
limit	| Total number of return results
activityId	| Flashsale activity ID

#### Sample Request
`/recommend/Activity?userId=25d044b768cf84ca&token=12232&activityId=324233&offset=1&limit=3`

#### **Sample Output**

```json
{
    "result": 0,
    "message": "kOk",
    "meta": {
      "traceid": “ILAMBDARSACTIVITY”,
      "totalItems": 30
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
