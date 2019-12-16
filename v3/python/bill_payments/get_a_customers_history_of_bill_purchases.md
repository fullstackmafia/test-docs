## Get a customer's history of bill purchases

You can retrieve a history of the bills a customer has purchased as well as the commission involved via the  `fly_history`  service. When you pass this in your  `POST`  request, also pass in a service payload as well. Below is a code sample showing how this is done:

```python

    import requests
    
    url = "https://api.ravepay.co/v2/services/confluence"
    
    querystring = {
     {
      "secret_key": "YOUR SECRET KEY",
      "service": "fly_history",
      "service_method": "post",
      "service_version": "v1",
      "service_channel": "rave",
      "service_payload": {
        "FromDate": "2018-08-01",
        "ToDate": "2018-08-27",
        "PageSize": 20,
        "PageIndex": 0,
        "Reference": "+233494850059"
      }
    }
      }
    }
    
    headers = {
      'content-type': 'application/json'
    }
    try:
    res = requests.request("POST", url, headers = headers, params = querystring)
    print(res.text)
    except requests.exceptions.RequestException as e:
      print(e)

```

Below is an example of the response you'll get should your request be successful:

```python

    {
        "status": "success",
        "message": "SERVICE-RESPONSE",
        "data": {
            "Summary": [
                {
                    "Currency": "NGN",
                    "SumBills": 3500,
                    "SumCommission": 40,
                    "SumDstv": 0,
                    "SumAirtime": 2000,
                    "CountDstv": 0,
                    "CountAirtime": 4
                },
                {
                    "Currency": "KES",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                },
                {
                    "Currency": "GHS",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                },
                {
                    "Currency": "USD",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                },
                {
                    "Currency": "EUR",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                },
                {
                    "Currency": "ZAR",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                },
                {
                    "Currency": "GBP",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                },
                {
                    "Currency": "TZS",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                },
                {
                    "Currency": "UGX",
                    "SumBills": 0,
                    "SumCommission": 0,
                    "SumDstv": 0,
                    "SumAirtime": 0,
                    "CountDstv": 0,
                    "CountAirtime": 0
                }
            ],
            "Transactions": [
                {
                    "Currency": "NGN",
                    "CustomerId": "+2349082930030",
                    "Frequency": "Hourly",
                    "Amount": "500.0000",
                    "Product": "AIRTIME",
                    "ProductName": "FLY-API-NG-AIRTIME-9MOBILE",
                    "Commission": 10,
                    "TransactionDate": "2018-08-24T05:35:07.213Z",
                    "TransactionId": 7895
                },
                {
                    "Currency": "NGN",
                    "CustomerId": "+2349082930030",
                    "Frequency": "One Time",
                    "Amount": "500.0000",
                    "Product": "AIRTIME",
                    "ProductName": "FLY-API-NG-AIRTIME-9MOBILE",
                    "Commission": 10,
                    "TransactionDate": "2018-08-24T01:06:31.55Z",
                    "TransactionId": 7891
                },
                {
                    "Currency": "NGN",
                    "CustomerId": "+2349082930030",
                    "Frequency": "One Time",
                    "Amount": "500.0000",
                    "Product": "AIRTIME",
                    "ProductName": "FLY-API-NG-AIRTIME-9MOBILE",
                    "Commission": 10,
                    "TransactionDate": "2018-08-23T16:56:07.193Z",
                    "TransactionId": 7868
                },
                {
                    "Currency": "NGN",
                    "CustomerId": "+2349082930030",
                    "Frequency": "One Time",
                    "Amount": "500.0000",
                    "Product": "AIRTIME",
                    "ProductName": "FLY-API-NG-AIRTIME-9MOBILE",
                    "Commission": 10,
                    "TransactionDate": "2018-08-23T16:55:49.413Z",
                    "TransactionId": 7867
                }
            ],
            "Total": 4,
            "Status": "success",
            "Message": "Successful",
            "Reference": null
        }
    }

```

| Parameter 	| Required 	| Description 	|
|-----------	|----------	|-------------------------------------------------------------------------------------------------------	|
| `FromDate` 	| True 	| This is the start date it can be in formats: `YYYY-MM-DDTHH:MM:SSZ` or `YYYY-MM-DD` 	|
| `ToDate` 	| True 	| This is the end date, it can be in formats: `YYYY-MM-DDTHH:MM:SSZ` or `YYYY-MM-DD` 	|
| `PageSize` 	| True 	| This is the number of items you want returned per page. 	|
| `PageIndex` 	| True 	| This is the page you want to start from. 	|
| `Reference` 	| False 	| This is the customer ID, pass this if you want to retrieve bill history for a particular customer ID. 	|