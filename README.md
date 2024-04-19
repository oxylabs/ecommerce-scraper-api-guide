# E-Commerce Scraper API Quick Start Guide

- [Authentication](#authentication)
- [Integration methods](#integration-methods)
  - [Push-Pull](#push-pull)
  - [Realtime](#realtime)
  - [Proxy Endpoint](#proxy-endpoint)

[![Oxylabs promo code](https://user-images.githubusercontent.com/129506779/250792357-8289e25e-9c36-4dc0-a5e2-2706db797bb5.png)](https://oxylabs.go2cloud.org/aff_c?offer_id=7&aff_id=877&url_id=112)

[![](https://dcbadge.vercel.app/api/server/eWsVUJrnG5)](https://discord.gg/GbxmdGhZjq)


Oxylabs’ [E-Commerce Scraper API](https://oxy.yt/PrOG) is a public data scraper API designed to collect real-time localized data and search information from most e-commerce websites at scale. This data gathering tool serves as a trustworthy solution for gathering public information from even the most complex e-commerce websites. E-Commerce Scraper API perfectly fits for business use cases such as price monitoring, product catalog mapping, competitor analysis. 

This quick start guide explains how the E-Commerce Scraper API works. We’ll also go through the process of getting started using this data gathering tool hassle-free.

For a detailed explanation, see our [blog post](https://oxy.yt/crIT).

## Authentication

E-Commerce Scraper API employs basic HTTP authentication which requires username and password:

```shell

curl --user "USERNAME:PASSWORD" 'https://realtime.oxylabs.io/v1/queries' -H "Content-Type: application/json" -d '{"source": "universal_ecommerce", "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html", "geo_location": "United States", "parse": true, "parser_type": "ecommerce_product"}'

```

## Integration methods

Oxylabs’ E-Commerce Scraper API offers various integration methods.

### Push-Pull

**Example of a single query request:**

```shell
curl --user "USERNAME:PASSWORD" 'https://data.oxylabs.io/v1/queries' -H "Content-Type: application/json" -d '{"source": "universal_ecommerce", "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html", "geo_location": "United States", "parse": true, "parser_type": "ecommerce_product"}'
```

If you are observing low success rates or retrieve empty content, please try using additional `"render":"html"` parameter in your request. More information about render parameter can be found [here](https://developers.oxylabs.io/scraper-apis/getting-started/api-reference/global-parameter-values#render).

**Sample of the initial response output:**

```json
{  
   "created_at":"2019-10-01 00:00:01",   "client_id":1,
   "domain": "com",
  "geo_location": "United States",
  "id": "6849255332305179649",
  "limit": 10,
  "locale": "",
  "pages": 1,
  "parse": true,
  "parser_type": "ecommerce_product",
  "render": "mhtml",
  "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html",
  "query": "",
  "source": "universal",
  "start_page": 1,
  "status": "pending",
  "storage_type": null,
  "storage_url": null,
  "subdomain": "books",
  "content_encoding": "utf-8",
  "updated_at": "2019-10-01 00:00:15",
  "user_agent_type": "desktop",
  "session_info": null,
  "statuses": [],
  "_links": [
    {
      "rel": "self",
      "href": "http://data.oxylabs.io/v1/queries/6849255332305179649",
      "method": "GET"
    },
    {
      "rel": "results",
      "href": "http://data.oxylabs.io/v1/queries/6849255332305179649/results",
      "method": "GET"
    }
  ]
}
```

**Example of how to check job status:**

```shell
curl --user "USERNAME:PASSWORD" 'http://data.oxylabs.io/v1/queries/6849255332305179649'
```

**Example of how to retrieve data:**

```shell
curl --user "USERNAME:PASSWORD" 'http://data.oxylabs.io/v1/queries/6849255332305179649/results'
```

**Sample of the response data output:**

```json
{
    "results": [
        {
            "content": {
                "ids": [],
                "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html",
                "brand": null,
                "image": null,
                "price": 51.77,
                "title": "A Light in the Attic",
                "currency": "£",
                "old_price": null,
                "description": "Product Description. It's hard to imagine a world without A Light in the Attic. This now-classic collection of poetry and drawings from Shel Silverstein celebrates its 20th anniversary with this special edition. Silverstein's humorous and creative verse can amuse the dowdiest of readers. Lemon-faced adults and fidgety kids sit still and read these rhythmic words and laugh and smile and love th It's hard to imagine a world without A Light in the Attic. This now-classic collection of poetry and drawings from Shel Silverstein celebrates its 20th anniversary with this special edition. Silverstein's humorous and creative verse can amuse the dowdiest of readers. Lemon-faced adults and fidgety kids sit still and read these rhythmic words and laugh and smile and love that Silverstein. Need proof of his genius? RockabyeRockabye baby, in the treetopDon't you know a treetopIs no safe place to rock?And who put you up there,And your cradle, too?Baby, I think someone down here'sGot it in for you. Shel, you never sounded so good. ...more. Product Information.",
                "availability": null,
                "parse_status_code": 12000,
                "additional_properties": [
                    {
                        "UPC": "a897fe39b1053632"
                    },
                    {
                        "Product Type": "Books"
                    },
                    {
                        "Price (excl. tax)": "£51.77"
                    },
                    {
                        "Price (incl. tax)": "£51.77"
                    },
                    {
                        "Tax": "£0.00"
                    },
                    {
                        "Availability": "In stock (22 available)"
                    },
                    {
                        "Number of reviews": "0"
                    }
                ]
            },
            "created_at": "2021-10-04 08:49:29",
            "updated_at": "2021-10-04 08:49:41",
            "page": 1,
            "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html",
            "job_id": "6850713463170271233",
            "status_code": 200
        }
    ]
}
```

### Realtime

**Example of a realtime request:**

```shell
curl --user "USERNAME:PASSWORD" 'https://realtime.oxylabs.io/v1/queries' -H "Content-Type: application/json" -d '{"source": "universal_ecommerce", "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html", "geo_location": "United States", "parse": true, "parser_type": "ecommerce_product"}'
```

If you are observing low success rates or retrieve empty content, please try using additional `"render":"html"` parameter in your request. More information about render parameter can be found [here](https://developers.oxylabs.io/scraper-apis/getting-started/api-reference/global-parameter-values#render).

**Example response body that will be returned on open connection:**

```json
{
    "results": [
        {
            "content": {
                "ids": [],
                "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html",
                "brand": null,
                "image": null,
                "price": 51.77,
                "title": "A Light in the Attic",
                "currency": "£",
                "old_price": null,
                "description": "Product Description. It's hard to imagine a world without A Light in the Attic. This now-classic collection of poetry and drawings from Shel Silverstein celebrates its 20th anniversary with this special edition. Silverstein's humorous and creative verse can amuse the dowdiest of readers. Lemon-faced adults and fidgety kids sit still and read these rhythmic words and laugh and smile and love th It's hard to imagine a world without A Light in the Attic. This now-classic collection of poetry and drawings from Shel Silverstein celebrates its 20th anniversary with this special edition. Silverstein's humorous and creative verse can amuse the dowdiest of readers. Lemon-faced adults and fidgety kids sit still and read these rhythmic words and laugh and smile and love that Silverstein. Need proof of his genius? RockabyeRockabye baby, in the treetopDon't you know a treetopIs no safe place to rock?And who put you up there,And your cradle, too?Baby, I think someone down here'sGot it in for you. Shel, you never sounded so good. ...more. Product Information.",
                "availability": null,
                "parse_status_code": 12000,
                "additional_properties": [
                    {
                        "UPC": "a897fe39b1053632"
                    },
                    {
                        "Product Type": "Books"
                    },
                    {
                        "Price (excl. tax)": "£51.77"
                    },
                    {
                        "Price (incl. tax)": "£51.77"
                    },
                    {
                        "Tax": "£0.00"
                    },
                    {
                        "Availability": "In stock (22 available)"
                    },
                    {
                        "Number of reviews": "0"
                    }
                ]
            },
            "created_at": "2021-10-04 08:49:29",
            "updated_at": "2021-10-04 08:49:41",
            "page": 1,
            "url": "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html",
            "job_id": "6850713463170271233",
            "status_code": 200
        }
    ]
}
```

### Proxy Endpoint

**Proxy Endpoint request sample using cURL library:**

```shell
curl -k -x realtime.oxylabs.io:60000 -U USERNAME:PASSWORD -H "X-Oxylabs-Geo-Location: United States" -H "X-Oxylabs-Parse: 1" -H "X-Oxylabs-Parser-Type: ecommerce_product" "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html"
```

If you are observing low success rates or retrieve empty content, please try adding additional `"x-oxylabs-render: html"` header with your request.

If you wish to find out more about E-Commerce Scraper API, see our [blog post](https://oxy.yt/crIT).
