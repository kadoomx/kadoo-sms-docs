![alt text](logo.png)

#Documentación

Documentación de la API de envios masivos Kadoo.

URL Producción: **https://api-sms.kadoo.mx** <br/>
URL Sandbox: **https://api-dev-sms.kadoo.mx**

##Autenticación

POST **/oauth/token**

####Request

|param|value|
|grant_type|client_credentials|
|client_id|**CLIENT_ID**|
|client_secret|**SECRET**|

Los datos de la API se encuentran desde el menú `API Keys`.


####Response

```json
{
    "token_type": "Bearer",
    "expires_in": 1296000,
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImUxMGI2NTQyYTk2NTFmZGRjODZmN2E0MWM4MjM5ZGZhNjVmMTk1YmE3NDVkNjZhYzkwYjk0YzYzZTBmYjZiNGMzNmFjMzUwNjY4ZTQ0MmYwIn0.eyJhdWQiOiI2IiwianRpIjoiZTEwYjY1NDJhOTY1MWZkZGM4NmY3YTQxYzgyMzlkZmE2NWYxOTViYTc0NWQ2NmFjOTBiOTRjNjNlMGZiNmI0YzM2YWMzNTA2NjhlNDQyZjAiLCJpYXQiOjE1Mzg1NDM5MjMsIm5iZiI6MTUzODU0MzkyMywiZXhwIjoxNTM5ODM5OTIzLCJzdWIiOiIiLCJzY29wZXMiOltdfQ.KgDTFBHLOHcnFjBoN4HoH_8M-ykzi5Uj1hWCT64suocHDm_0QA-y4CQzV5CsTiQnDhm8UBEbtgQPw7rkN9F3KcCOfP-vVcVxuhVit01MBtwRPUOY_Mn6SUtTlJUQfIrtIj7Rky4fUq-uwn-2w9i1GNE6cCvOoyps1t4_DeSDFVhT_PqERHsvAg7AKsR6Tc9IXUIXJpsrJ0-x70T6fy3hBy4SP38JA4hda44i7PGCqnmOsQ87EM0ttSGPkFWzxlnlHfzZZBNoT2LWnhYw2LVxAO7sRA-lKIbx6HLeHllO9vPFtIghZn7EkF8iQmP3VBBdxrqA60YBDdSs_mVr8Zn-ARrvDegFS9vnoZTqNIMyxrnHp41DW-9ghtN3Yv2e9H1-5BgbrjAg005Rdr2lRgKGn_ppqxZeIejLxRr1S9OW90Jxfw_i89I6mc6eRDjJqhzh3z9o8mwKDgw9Nni5EfWtDXmLZoe_W3YV3N5rkk7oQ-Tk7JrJ8akCzvL2qvBKlQwjaN70Rktax6Ua5dao4ha5Dqd2P28qaN2ZDNhTc7FaEGlgrcQn2L516Y2qsFP9XlvdnnXQ5U6BohN59GZeiF_KnSi9Vv8vn5IaEpXys2ykfwQ5UiuI1UXU8asA5n-kJsIruVhBOF-F4PT_aacbwee89dNcYrguXgkGciFR9t-gQKo"
}
```

####Response si faltan datos

```json
{
    "error": "invalid_request",
    "message": "The request is missing a required parameter, includes an invalid parameter value, includes a parameter more than once, or is otherwise malformed.",
    "hint": "Check the `client_id` parameter"
}
```

####Response con datos inválidos

````json
{
    "error": "invalid_client",
    "message": "Client authentication failed"
}
````

##Enviar Mensaje

POST **/message**

####Payload

````json
{
	"number": 5512345678,
	"message": "Test Message"
}
````

####Response

````json
{
    "id": "3f8f193e-f31b-44a8-a014-6393a58cbdf7",
    "phone": 5512345678,
    "text": "Test Message",
    "updated_at": "2018-10-03 05:23:56",
    "created_at": "2018-10-03 05:23:56"
}
````

##Ver detalle de envío

GET **/message/{id}**

####Response

````json
{
    "id": "3f8f193e-f31b-44a8-a014-6393a58cbdf7",
    "phone": 5512345678,
    "text": "Test Message",
    "carrier_id": "IUSACELL_MX",
    "created_at": "2018-10-03 05:23:56",
    "updated_at": "2018-10-03 05:25:04",
    "processed_at": "2018-10-03 05:24:01",
    "sent_status": "SENT_SUCCESS",
    "sent_status_code": 2,
    "sent_status_date": "2018-10-03 00:24:01",
    "parts": 1
}
````

##Ver envíos

GET **/message**

**GET Variables**

* **page** (default=1)
* **start** (opcional, 'Y-m-d')
* **end** (opcional, 'Y-m-d')
* **text** (opcional)
* **phone** (opcional, no es necesario que sea completo, puede ser una parte del número nada más)

####Request

```json
{
    "count": 4815,
    "messages": [
        {
            "id": "3f8f193e-f31b-44a8-a014-6393a58cbdf7",
            "phone": 5512345678,
            "text": "Test Message",
            "carrier_id": "IUSACELL_MX",
            "created_at": "2018-10-03 05:23:56",
            "updated_at": "2018-10-03 05:25:04",
            "processed_at": "2018-10-03 05:24:01",
            "sent_status": "SENT_SUCCESS",
            "sent_status_code": 2,
            "sent_status_date": "2018-10-03 00:24:01",
            "parts": 1
        },
        {
            "id": "4708d34e-3447-452f-8ab2-21512d2c86d1",
            "phone": 5512345678,
            "text": "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt expli",
            "carrier_id": "IUSACELL_MX",
            "created_at": "2018-10-03 04:27:56",
            "updated_at": "2018-10-03 04:29:01",
            "processed_at": "2018-10-03 04:28:00",
            "sent_status": "SENT_SUCCESS",
            "sent_status_code": 2,
            "sent_status_date": "2018-10-02 23:28:01",
            "parts": 2
        },
        {
            "id": "a1502f1a-ea47-41f5-bc7e-577d0eec235f",
            "phone": 5512345678,
            "text": "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt expli",
            "carrier_id": "IUSACELL_MX",
            "created_at": "2018-10-03 04:09:40",
            "updated_at": "2018-10-03 04:10:47",
            "processed_at": "2018-10-03 04:09:43",
            "sent_status": "SENT_SUCCESS",
            "sent_status_code": 2,
            "sent_status_date": "2018-10-02 23:09:44",
            "parts": 1
        }...
    ]
}
```