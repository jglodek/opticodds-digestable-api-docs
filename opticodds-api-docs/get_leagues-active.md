# OpticOdds API - Active Leagues Endpoint

## Endpoint Overview

**HTTP Method:** GET  
**Endpoint URL:** `https://api.opticodds.com/api/v3/leagues/active`

## Description

This API endpoint returns a comprehensive list of all the leagues that currently have fixtures with odds available. The endpoint provides detailed information about each league including their unique identifiers, associated sports, main betting markets, geographical region information, and other relevant metadata that can be used for subsequent API calls and filtering operations.

## Query Parameters

### Required Parameters
- **sport** (string): Specifies the sport type to filter leagues. Example: `basketball`

## Request Information

### Base URL Structure
```
https://api.opticodds.com/api/v3/leagues/active?sport={sport_type}
```

### Example Request URL
```
https://api.opticodds.com/api/v3/leagues/active?sport=basketball
```

### Supported HTTP Methods
- **GET**: Retrieve active leagues data

### Content-Type
- **Request:** Not applicable (GET request)
- **Response:** `application/json`

## Response Structure

The API returns a JSON object with the following structure:

### Root Response Object
```json
{
  "data": [
    // Array of league objects
  ]
}
```

### League Object Structure

Each league object in the `data` array contains the following fields:

#### Top-level League Properties
- **id** (string): Unique string identifier for the league in lowercase with underscores
  - Format: `{country}_{league_abbreviation}`
  - Example: `"argentina_-_lnb"`, `"australia_-_nbl"`, `"nba"`
  
- **name** (string): Human-readable display name of the league
  - Examples: `"Argentina - LNB"`, `"Australia - NBL"`, `"NBA"`
  
- **numerical_id** (integer): Unique numerical identifier for the league
  - Examples: `14`, `28`, `355`
  
- **region** (string): Geographic region or country where the league operates
  - Format: Uppercase with underscores for multi-word countries
  - Examples: `"ARGENTINA"`, `"AUSTRALIA"`, `"UNITED_STATES"`, `"SOUTH_KOREA"`
  
- **region_code** (string): ISO 3166-1 alpha-3 country code
  - Format: Three-letter uppercase country code
  - Examples: `"ARG"`, `"AUS"`, `"USA"`, `"KOR"`, `"LTU"`

#### Sport Object Structure

Each league contains a nested `sport` object with the following properties:

- **id** (string): Unique string identifier for the sport type
  - Example: `"basketball"`
  
- **name** (string): Human-readable display name of the sport
  - Example: `"Basketball"`
  
- **numerical_id** (integer): Unique numerical identifier for the sport
  - Example: `4`

##### Main Markets Array

The sport object contains a `main_markets` array with betting market information:

**Market Object Properties:**
- **id** (string): Unique string identifier for the betting market type
  - Examples: `"moneyline"`, `"point_spread"`, `"total_points"`
  
- **name** (string): Human-readable display name of the betting market
  - Examples: `"Moneyline"`, `"Point Spread"`, `"Total Points"`
  
- **numerical_id** (integer): Unique numerical identifier for the betting market
  - Examples: `953`, `1172`, `1358`

## Example Response

### Complete Response Structure
```json
{
  "data": [
    {
      "id": "argentina_-_lnb",
      "name": "Argentina - LNB",
      "numerical_id": 14,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "ARGENTINA",
      "region_code": "ARG"
    },
    {
      "id": "australia_-_nbl",
      "name": "Australia - NBL",
      "numerical_id": 28,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "AUSTRALIA",
      "region_code": "AUS"
    },
    {
      "id": "australia_-_wnbl",
      "name": "Australia - WNBL",
      "numerical_id": 39,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "AUSTRALIA",
      "region_code": "AUS"
    },
    {
      "id": "korea_-_kbl",
      "name": "Korea - KBL",
      "numerical_id": 314,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "SOUTH_KOREA",
      "region_code": "KOR"
    },
    {
      "id": "korea_-_wkbl",
      "name": "Korea - WKBL",
      "numerical_id": 316,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "SOUTH_KOREA",
      "region_code": "KOR"
    },
    {
      "id": "lithuania_-_lkl",
      "name": "Lithuania - LKL",
      "numerical_id": 332,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "LITHUANIA",
      "region_code": "LTU"
    },
    {
      "id": "nba",
      "name": "NBA",
      "numerical_id": 355,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "UNITED_STATES",
      "region_code": "USA"
    },
    {
      "id": "ncaab",
      "name": "NCAAB",
      "numerical_id": 356,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "UNITED_STATES",
      "region_code": "USA"
    },
    {
      "id": "ncaaw",
      "name": "NCAAW",
      "numerical_id": 360,
      "sport": {
        "id": "basketball",
        "name": "Basketball",
        "numerical_id": 4,
        "main_markets": [
          {
            "id": "moneyline",
            "name": "Moneyline",
            "numerical_id": 953
          },
          {
            "id": "point_spread",
            "name": "Point Spread",
            "numerical_id": 1172
          },
          {
            "id": "total_points",
            "name": "Total Points",
            "numerical_id": 1358
          }
        ]
      },
      "region": "UNITED_STATES",
      "region_code": "USA"
    }
  ]
}
```

## League Examples from Response

### International Basketball Leagues
- **Argentina - LNB**: Professional basketball league in Argentina
  - ID: `argentina_-_lnb`
  - Numerical ID: `14`
  - Region: `ARGENTINA` (ARG)

- **Australia - NBL**: National Basketball League of Australia
  - ID: `australia_-_nbl`
  - Numerical ID: `28`
  - Region: `AUSTRALIA` (AUS)

- **Australia - WNBL**: Women's National Basketball League of Australia
  - ID: `australia_-_wnbl`
  - Numerical ID: `39`
  - Region: `AUSTRALIA` (AUS)

### Asian Basketball Leagues
- **Korea - KBL**: Korean Basketball League
  - ID: `korea_-_kbl`
  - Numerical ID: `314`
  - Region: `SOUTH_KOREA` (KOR)

- **Korea - WKBL**: Women's Korean Basketball League
  - ID: `korea_-_wkbl`
  - Numerical ID: `316`
  - Region: `SOUTH_KOREA` (KOR)

### European Basketball Leagues
- **Lithuania - LKL**: Lithuanian Basketball League
  - ID: `lithuania_-_lkl`
  - Numerical ID: `332`
  - Region: `LITHUANIA` (LTU)

### North American Basketball Leagues
- **NBA**: National Basketball Association
  - ID: `nba`
  - Numerical ID: `355`
  - Region: `UNITED_STATES` (USA)

- **NCAAB**: National Collegiate Athletic Association Basketball (Men's)
  - ID: `ncaab`
  - Numerical ID: `356`
  - Region: `UNITED_STATES` (USA)

- **NCAAW**: National Collegiate Athletic Association Basketball (Women's)
  - ID: `ncaaw`
  - Numerical ID: `360`
  - Region: `UNITED_STATES` (USA)

## Betting Markets Information

For basketball leagues, the following main betting markets are consistently available:

### Moneyline
- **ID**: `moneyline`
- **Numerical ID**: `953`
- **Description**: Straight bet on which team will win the game

### Point Spread
- **ID**: `point_spread`
- **Numerical ID**: `1172`
- **Description**: Bet on the margin of victory with a handicap applied

### Total Points
- **ID**: `total_points`
- **Numerical ID**: `1358`
- **Description**: Bet on whether the combined score will be over or under a specified total

## Important Notes

### Data Accuracy Disclaimer
The example response provided is used exclusively to demonstrate the JSON format structure and field types. The actual data returned by the API may differ from the examples shown, as league availability, numerical IDs, and other details are subject to change based on current fixture availability and odds data.

### Parameter Requirements
As mentioned in the specific parameter information section, this endpoint requires additional parameters beyond the sport filter. Users should refer to the complete parameter documentation (referenced as available at the bottom of the original page) for full implementation details.

### Dynamic Content
The leagues returned by this endpoint represent only those currently having active fixtures with available odds. This means the response content will vary based on:
- Current sports seasons
- Available betting markets
- Fixture scheduling
- Odds provider availability

### Use Cases
This endpoint is typically used for:
- Populating league selection dropdowns in betting applications
- Filtering available leagues before making fixture requests
- Understanding market availability for specific leagues
- Building dynamic sport and league navigation systems