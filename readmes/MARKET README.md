[![market-workflow-shield]][market-repo]


# Market Item Endpoint

## Overview

This repo contains the market item source code for the [market-item endpoint](https://marketItem-api-endpoint.herokuapp.com), which is meant to gather data from the steam endpoint and handle all the formatting and pagination. It is one of the containers that lay between the [steam endpoint](https://github.com/noahgreff/steam-api-endpoint) and the frontend application.

## Item Object

|name|description|type|default| 
|---:|---|:---:|:---:| 
| **`name`** | The name of the item |*string* | "Unknown" |
| **`appid`** |  The unique game identifier as specified by steam's API |*integer* | 0 |
| **`app_name`** | The name of the game |*integer* | "Unknown" |
| **`app_icon`** | The game's icon url (*https*) |*string* |
| **`item_icon`** | The item's icon url (*https*) | *string* |
| **`volume`** | The volume sold of the item over the last week |*integer* | 0 |
| **`page`** | The current page of the listing |*string* | 1 |
| **`current`** | Displays the current vaule of the item |*float* | 0.0 |
| **`text`** | Displays the current value of the item in text to facilitate usage on the frontend |*string* | "€0.00" |
| **`median`** | The median item listing price |*float* | 0.0 |
| **`lowest`** | The cheapest item sold |*float* | 0.0 |

## Endpoint URIs

* ### **`/item/all`**

##### Description: Getting a game's *tradable* items

> * http verb: *`GET`*
> * response: *JSON*
>
> Returns a paginated listing of [Item](#Item-object) Objects

##### Url Paramaters:

|param|description|type|default| 
|---:|---|:---:|:---:| 
| **`appid`** | The unique game identifier as specified by steam's API |*integer* ||
| **`page`** | The listing page number |*integer* | 1 |
| **`range`** | The range of items to get |*integer* | 10 |

#### Usage

Fetching items from the game *RUST*, with `appid`: **252490**:

```
https://market-api-endpoint.herokuapp.com/item/all/252490
```
Will yeild:
```json
{
    "data": [
        {
            "name": "Urban Afterburn Pump Shotgun",
            "app_name": "Rust",
            "appid": 252490,
            "app_icon": "https://cdn.cloudflare.steamstatic.com/steamcommunity/public/images/apps/252490/820be4782639f9c4b64fa3ca7e6c26a95ae4fd1c.jpg",
            "item_icon": "https://steamcommunity-a.akamaihd.net/economy/image/6TMcQ7eX6E0EZl2byXi7vaVKyDk_zQLX05x6eLCFM9neAckxGDf7qU2e2gu64OnAeQ7835Fe5GPBfCk4nReh8DEiv5dbOa0-q7U0Qfq3P2Ox1KU",
            "volume": 0,
            "page": "https://steamcommunity.com/market/listings/252490/Urban%20Afterburn%20Pump%20Shotgun",
            "pricing": {
                "current": 460,
                "text": "€4.60",
                "median": 0,
                "lowest": 0
            }
        },
        
        { ... }

    ],
    "links": {
        "first": "https://market-api-endpoint.herokuapp.com/item/all/252490?page=1&range=10",
        "last": "https://market-api-endpoint.herokuapp.com/item/all/252490?page=248&range=10",
        "prev": null,
        "next": "https://market-api-endpoint.herokuapp.com/item/all/252490?page=2&range=10"
    },
    "meta": {
        "current_page": 1,
        "last_page": 248,
        "from": 0,
        "to": 10,
        "current_on_page": 10,
        "total": 2480
    }
}
```

[market-workflow-shield]: https://github.com/noahgreff/marketItem-api-endpoint/workflows/Market%20Endpoint%20CI/badge.svg
[market-repo]: https://github.com/noahgreff/marketItem-api-endpoint/
