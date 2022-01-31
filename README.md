# szamla.guru

Production system URL: https://app.szamla.guru

Test system URL: https://dev.billing.epax.hu


You should replace the following variables in curl commands:
* DOMAIN - you can see 2 URL above
* KEY - you can get here: https://DOMAIN/settings/company/api-key/list


## Get vat types:
```
curl --location --request GET 'https://DOMAIN/api/v1/vat-types' \
--header 'Authorization: Bearer KEY' \
--data-raw ''
```

## Get payment modes
```
curl --location --request GET 'http://DOMAIN/api/v1/payment-modes' \
--header 'Authorization: Bearer KEY' \
--data-raw ''
```

## Get available currencies
```
curl --location --request GET 'http://DOMAIN/api/v1/currencies' \
--header 'Authorization: Bearer KEY' \
--data-raw ''
```

## Store partner data
You can store lot of data from your partner. We created two example for maximum data and for minimum data.

Possible elements for tax_type:
* person (if it is NOT company and has NOT tax number)
* company-hu (if it is hungarian company and has tax number)
* company-eu (if it is europiean company and has tax number)
* company-third (if it is out of europiean company and has tax number)

### Store MAXIMUM partner data
```
curl --location --request POST 'http://DOMAIN/api/v1/partner/store' \
--header 'Authorization: Bearer KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "API TESZT PARTNER",
    "country": "HU",
    "state": null,
    "zip": "6726",
    "city": "Szeged",
    "district": null,
    "street_name": "Alsó kikötő",
    "street_type": "sor",
    "house_number": "11",
    "building": null,
    "staircase": null,
    "level": null,
    "door": null,
    "phone": null,
    "email": null,
    "web": null,
    "bank_number": null,
    "iban_code": null,
    "swift_code": null,
    "tax_type": "person",
    "tax_number": null,
    "tax_group_number": null,
    "tax_communal_number": null,
    "tax_third_state": null,
    "payment_mode": null,
    "payment_deadline_days": null,
    "currency_code": null
}'
```

### Store MINIMUM partner data

```
curl --location --request POST 'http://DOMAIN/api/v1/partner/store' \
--header 'Authorization: Bearer KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "API TESZT PARTNER",
    "country": "HU",
    "zip": "6726",
    "city": "Szeged",
    "street_name": "Alsó kikötő",
    "street_type": "sor",
    "house_number": "11",
    "tax_type": "person"
}'
```

## Get partner data
```
curl --location --request GET 'http://DOMAIN/api/v1/partner/1/get' \
--header 'Authorization: Bearer KEY' \
--data-raw ''
```

## Get all partners
```
curl --location --request GET 'http://DOMAIN/api/v1/partner/get-all' \
--header 'Authorization: Bearer KEY' \
--data-raw ''
```

## Store invoice

Possible elements of payment_mode:
* cash
* transfer
* check
* voucher
* card
* einvoice
* compensation
* cash_on_delivery

### Store MAXIMUM invoice data
```
curl --location --request POST 'http://DOMAIN/api/v1/invoice/store' \
--header 'Authorization: Bearer KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
  "partner_id": 158,
  "invoice_pad_id": 1,
  "payment_mode": "transfer",
  "fulfillment_date": "2021-03-31",
  "payment_date": "2021-03-31",
  "round_to": 1,
  "currency_code": "HUF",
  "currency_exchange": 1,
  "nav_send_type": 1,
  "is_paid": false,
  "items": [
    {
      "name": "Bread",
      "unit_price": 1500,
      "qty": 5,
      "qty_name": "kg",
      "tax": "27%",
      "discount": null,
      "comment": null
    },
    {
      "name": "Egg",
      "unit_price": 50,
      "qty": 12,
      "qty_name": "db",
      "tax": "27%",
      "discount": 10,
      "comment": "Beautiful egg"
    }
  ],
  "comment": "Invoice comment",
  "is_cover_page": 0
}'
```

### Store MINIMUM invoice data
```
curl --location --request POST 'http://DOMAIN/api/v1/invoice/store' \
--header 'Authorization: Bearer KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
  "partner_id": 158,
  "invoice_pad_id": 1,
  "payment_mode": "transfer",
  "fulfillment_date": "2021-03-31",
  "payment_date": "2021-03-31",
  "round_to": 1,
  "currency_code": "HUF",
  "nav_send_type": 1,
  "is_paid": false,
  "items": [
    {
      "name": "Bread",
      "unit_price": 1500,
      "qty": 5,
      "qty_name": "kg",
      "tax": "27%",
      "discount": null,
      "comment": null
    },
    {
      "name": "Egg",
      "unit_price": 50,
      "qty": 12,
      "qty_name": "db",
      "tax": "27%",
      "discount": 10,
      "comment": "Beautiful egg"
    }
  ],
  "comment": "Invoice comment",
  "is_cover_page": 0
}'
```

## Download PDF of invoice
```
curl --location --request GET 'http://DOMAIN/api/v1/invoice/1/download' \
--header 'Authorization: Bearer KEY' \
--data-raw ''
```

## Get all invoice pad
```
curl --location --request GET 'http://DOMAIN/api/v1/invoice-pads/get-all' \
--header 'Authorization: Bearer KEY' \
--data-raw ''
```
