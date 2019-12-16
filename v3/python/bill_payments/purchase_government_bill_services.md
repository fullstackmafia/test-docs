## Purchase government bill services

With Rave, you can handle bills that have to be paid to the government. Examples of such bills include electricity, water or tax bills. Government bills can be processed first by creating an order for the service to be paid for with the  `fly_remita_create-order`  service and then proceeding to fulfil the created order via the  `fly_remita_pay-order`  service. Here's a code sample showing exactly how you can do that:

##  1.  Create an order for the service to be paid for

```python

    import requests
    
    url = "https://api.ravepay.co/v2/services/confluence"
    
    querystring =
    
      {
        "secret_key": "FLWSECK-e6db11d1f8a6208de8cb2f94e293450e-X",
        "service": "fly_remita_create-order",
        "service_method": "post",
        "service_version": "v1",
        "service_channel": "rave",
        "service_payload": {
    
          "billercode": "BIL136",
          "productcode": "OT151",
          "amount": "3500.00",
          "transactionreference": "FLWTTOT1000000092",
          "payer": {
            "name": "emmanuel",
            "email": "emmanuel@x.com",
            "phone": "08060811638"
          },
          "fields": [{
    
            "id": "42107711:42107712",
            "quantity": "1",
            "value": "3500"
          }, {
            "id": "42107710",
            "quantity": "1",
            "value": "t@x.com"
          }]
        }
    
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

If your request is successful, you'll get a response that contains the newly created order's reference number:

```python

    {
        "status": "success",
        "message": "SERVICE-RESPONSE",
        "data": {
            "data": {
                "amount": "3785.25",
                "fee": "26.25",
                "response_code": "00",
                "response_message": "Order processed successfully",
                "transaction_reference": "FLWTTOT10000060",
                "order_reference": "8aeeb7be-5e30-4638-8d31-1b3ba15c2a03",
                "transaction_date": "2019-10-18T14:35:25611",
                "total_amount": "3811.5"
            },
            "description": "successful",
            "status": "success"
        }
    }

```

## 2.  Pay for the newly created order

After creating the order, the next step is to pay for the order. This can be done through the  `fly_remita_pay-order`  service. Here's a code sample depicting how to do that:

```python

import requests

url = "https://api.ravepay.co/v2/services/confluence"

querystring = {
    "secret_key": "YOUR API KEY",
    "service": "fly_remita_pay-order",
    "service_method": "post",
    "service_version": "v1",
    "service_channel": "rave",
    "service_payload": {
      "orderreference": "47e02fb6-a32d-41f8-9f03-6c7b0da54d7b",
      "paymentreference": "FLWTTOT1000000092",
      "amount": "3811.5"
    }

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

Should your request be successful, you'll receive a response similar to the one below:

```python

    {
        "status": "success",
        "message": "SERVICE-RESPONSE",
        "data": {
            "data": {
                "amount": "3785.25",
                "response_code": "00",
                "response_message": "Transaction Successful",
                "order_reference": "47e02fb6-a32d-41f8-9f03-6c7b0da54d7b",
                "total_amount": "3811.5",
                "meta": {
                    "rrr": "310007778124"
                },
                "fee": "26.25",
                "payment_reference": "FLWTTOT1000000092",
                "flutter_reference": "BP15714063417857459"
            },
            "message": "",
            "status": "success"
        }
    }

```

## Parameters

| Parameter 	| Required 	| Description 	|
|-------------------	|----------	|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| `secret_key` 	| True 	| This is your merchant secret key, please see our section on [API Keys](https://developer.flutterwave.com/reference-link/api-keys-1) to learn how to retrieve your secret key. 	|
| `service` 	| True 	| This is the bill payment services available please see a list below with explanation of the services. e.g. `fly_buy` , `fly_recurring` 	|
| `service_method` 	| True 	| This is the HTTP Method for the required service. 	|
| `service_version` 	| True 	| This is the version for the APIs. Set to `v1`, when a new version is available you would be able to put your required version. 	|
| `service_channel` 	| True 	| This is the channel for the service, always use `rave` as the value. 	|
| `service_payload` 	| False 	| This is the request to be sent for the service. 	|
