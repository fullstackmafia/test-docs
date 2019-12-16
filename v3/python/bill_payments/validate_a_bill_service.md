**Validate a bill service**

You can check the authenticity of a bill service by validating its details such as the serial or registration number attached to the bill. This can be done by making a  `POST`  request to Rave's 
API and specifying the serial number of the bill as a property in the  `service`  object parameter. Below is a code sample that depicts how to do this:

```python

    import requests
    
    url = "https://api.ravepay.co/v2/services/confluence"
    
    querystring =
    
      {
        "secret_key": "YOUR SECRET KEY",
        "service": "bills_validate_CB140_BIL119_1025401152",
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

**Parameters for validating a bill service**

| Parameter 	| Required 	| Description 	|
|-------------------	|-------------------------------------	|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| `secret_key` 	| True 	| This is your merchant secret key, please see our section on [API Keys](https://developer.flutterwave.com/reference-link/api-keys-1) to learn how to retrieve your secret key. 	|
| `service` 	| True 	| This is the bill payment services available please see a list below with explanation of the services.e.g. `fly_buy` , `fly_recurring` 	|
| `service_method` 	| True 	| This is the HTTP Method for the required service. 	|
| `service_version` 	| True 	| This is the version for the APIs . Set to `v1`, when a new version is available you would be able to put your required version. 	|
| `service_channel` 	| True <br><br>`Expected value: rave` 	| This is the channel for the service, always use `rave` as the value. 	|