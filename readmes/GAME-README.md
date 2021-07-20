[![game-workflow-shield]][game-repo]


# Game Endpoint

## Overview

This repo contains the game source code for the [game endpoint](https://game-api-endpoint.herokuapp.com), which is meant to gather data from the steam endpoint and handle all the formatting and pagination. It is one of the containers that lay between the [steam endpoint](https://github.com/noahgreff/game-api-endpoint) and the frontend application.

## Game Object

### Personal Game Object

|name|description|type|default| 
|---:|---|:---:|:---:| 
| **`name`** | The name of the game |*string* | "Unknown" |
| **`appid`** |  The unique game identifier as specified by steam's API |*integer* | 0 |
| **`total`** | The total amount of hours spent within the game |*integer* | 0 |
| **`text`** | The total amount of time spent within the game as text format described in minutes, hours, days, ..., decades ;) |*string* | "< 1 Hour" |
| **`recent:total`** | The total amount of time spent playing in hours within the last two weeks | *integer* | 0 |
| **`recent:text`** | The total amount of time spent playing in hours within the last two weeks as text |*string* | 0 | "< 1 Hour" |
| **`logo`** | The url of the logo/icon of the game as seen in the library or in the taskbar (*https*) |*string* |
| **`banner`** | The url of the banner of the game (*https*) |*string* |

### Public Game Object

|name|description|type|default| 
|---:|---|:---:|:---:| 
| **`name`** | The name of the game |*string* | "Unknown" |
| **`appid`** |  The unique game identifier as specified by steam's API |*integer* | 0 |
| **`banner`** | The banner of the game (*https*) |*float* |
| **`background`** | The background layer image used by Steam on the store (*https*) |*string* |
| **`description`** | The description of the game (shortened) | *string* | "N/A" |
| **`publishers`** | The publishers of the game |*string[]* | "N/A" |
| **`price_text`** | The price of the game as text |*string* | "Free" |
| **`platform`** | The platform the current game version supports |*string[]* |
| **`likes`** | The total amount of like the game's store page has |*integer* | 0 |

## Endpoint URIs

* ### **`/game/owned`**

##### Description: Getting a steam user's owned games.

> * http verb: *`GET`*
> * response: *JSON*
>
> Returns a paginated listing of [Game (Personal)](#game-object) Objects

##### Url Paramaters:

|param|description|type|default| 
|---:|---|:---:|:---:| 
| **`steamid`** | The unique base64 id attributed to each Steam user |*integer* |
| **`ftp`** | Includes the list of free games the user owns. By default, Steam considers that every user already owns every free games on the platform. |*boolean* | false |

#### Usage

Fetching games from *me* (repo owner), with `steamid`: **76561198272843849**:

```
https://game-api-endpoint.herokuapp.com/game/owned/76561198272843849
```
Will yeild:
```json
{
    "total": 32,
    "playtime": {
        "total": 3493,
        "text": "5 Months"
    },
    "games": [
        {
            "name": "Rust",
            "appid": 252490,
            "playtime": {
                "total": 1940,
                "text": "3 Months",
                "recent": {
                    "total": 0,
                    "text": "< 1 Hour"
                }
            },
            "logo": "https://steamcdn-a.akamaihd.net/steamcommunity/public/images/apps/252490/820be4782639f9c4b64fa3ca7e6c26a95ae4fd1c.jpg",
            "banner": "https://steamcdn-a.akamaihd.net/steam/apps/252490/capsule_184x69.jpg"
        },

        { ... }
    ]
}
```

</br>

* ### **`/game/recent`**

##### Description: Getting a steam user's recently played games.

> * http verb: *`GET`*
> * response: *JSON*
>
> Returns a paginated listing of [Game (Personal)](#game-object) Objects

##### Url Paramaters:

|param|description|type|default| 
|---:|---|:---:|:---:| 
| **`steamid`** | The unique base64 id attributed to each Steam user |*integer* |

#### Usage

Fetching games from *me* (repo owner), with `steamid`: **76561198272843849**:

```
https://game-api-endpoint.herokuapp.com/game/recent/76561198272843849
```
Will yeild:
```json
{
    "total": 32,
    "playtime": {
        "total": 3493,
        "text": "5 Months"
    },
    "games": [
        {
            "name": "Phasmophobia",
            "appid": 739630,
            "playtime": {
                "total": 43,
                "text": "2 Days",
                "recent": {
                    "total": 2,
                    "text": "2 Hours"
                }
            },
            "logo": "https://steamcdn-a.akamaihd.net/steamcommunity/public/images/apps/739630/125673b382059f666ec81477173380a76e1df0be.jpg",
            "banner": "https://steamcdn-a.akamaihd.net/steam/apps/739630/capsule_184x69.jpg"
        }
        
        { ... }
    ]
}
```

</br>

* ### **`/game/info`**

##### Description: Getting a specific game's information from Steam

> * http verb: *`GET`*
> * response: *JSON*
>
> Returns a paginated listing of [Game (Public)](#game-object) Objects

##### Url Paramaters:

|param|description|type|default| 
|---:|---|:---:|:---:| 
| **`appid`** |  Search by the unique game identifier as specified by steam's API |*integer* | 0 |

#### Usage

Fetching game information from *PHASMOPHOBIA*, with `appid`: **739630**:

```
http://game-api-endpoint.herokuapp.com/game/info/739630
```
Will yeild:
```json
{
    "name": "Phasmophobia",
    "appid": 739630,
    "banner": "https://steamcdn-a.akamaihd.net/steam/apps/739630/header.jpg?t=1609602804",
    "background": "https://steamcdn-a.akamaihd.net/steam/apps/739630/page_bg_generated_v6b.jpg?t=1609602804",
    "description": "Phasmophobia is a 4 player online co-op psychological horror. Paranormal activity is on the rise and it’s up to you and your team to use all the ghost hunting equipment at your disposal in order to gather as much evidence as you can.",
    "publishers": ["Kinetic Games"],
    "price_text": "€11.59",
    "platforms": {
        "windows": true,
        "mac": false,
        "linux": false
    },
    "likes": 170231
}
```


[game-workflow-shield]: https://github.com/noahgreff/game-api-endpoint/workflows/Game%20Endpoint%20CI/badge.svg
[game-repo]: https://github.com/noahgreff/game-api-endpoint/
