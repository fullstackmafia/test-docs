**Retrieve details of a recurring bill service**

When you purchase a bill service, you have the ability to retrieve its details. This is particularly useful for merchants who want to verify the subscription model of their end users who might have lodged complaints related to a subscription model. Retrieving details of a recurrent bill can be done by making a  `GET`  request to Rave's API and specifying  `fly_recurring`  in the service object parameter. Below is a code sample depicting how to do this:


```python

    import requests
    
    url = "https://api.ravepay.co/v2/services/confluence"
    
    querystring =
    
      {
        "secret_key": "<YOUR SECRET KEY>",
        "service": "fly_recurring",
        "service_method": "get",
        "service_version": "v1",
        "service_channel": "rave"
      },
    
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
            "RecurringPayments": [
                {
                    "Id": 5,
                    "UniqueReference": "+2349082930030",
                    "Amount": 500,
                    "DateStarted": "2018-08-24T05:35:18.587Z",
                    "DateStopped": null,
                    "NextRun": "2018-08-24T06:35:18.587Z",
                    "RecurringType": "Hourly"
                }
            ],
            "Status": "success",
            "Message": "successful",
            "Reference": null
        }
    }

```

**Recurring bill service parameters**

| Parameter 	| Required 	| Description 	|
|-------------------	|-------------------------------------	|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| `secret_key` 	| True 	| This is your merchant secret key, please see our section on [API Keys](https://developer.flutterwave.com/reference-link/api-keys-1) to learn how to retrieve your secret key. 	|
| `service` 	| True 	| This is the bill payment services available please see a list below with explanation of the services.e.g. `fly_buy` , `fly_recurring` 	|
| `service_method` 	| True 	| This is the HTTP Method for the required service. 	|
| `service_version` 	| True 	| This is the version for the APIs . Set to `v1`, when a new version is available you would be able to put your required version. 	|
| `service_channel` 	| True <br>`Expected value: rave` 	| This is the channel for the service, always use `rave` as the value. 	|