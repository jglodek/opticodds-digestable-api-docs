# Players API Documentation

## Endpoint Overview

**GET** `/api/v3/players`

Get a paginated list of all players from the OpticOdds API. This endpoint provides comprehensive player information including personal details, team affiliations, and physical attributes.

## Description

This endpoint returns a paginated list of all players. The API will return only **active** teams by default, which means that if a player has retired or is not currently on a roster, that player will no longer be active for that specific league.

### Important Notes About Player IDs

Player IDs are unique per league, which means that the same player can have different IDs across different leagues. This is a crucial consideration when working with players who participate in multiple leagues.

**Example: Lionel Messi's Different IDs**
- `C7231134C08F`: USA - Major League Soccer
- `7D915F8BDA8E`: CONMEBOL - Copa America

### Inactive Player Data

If a player is no longer active but you want to retrieve information about them, you can pass the specific player `id` parameter to this endpoint. When a specific ID is provided, the endpoint will return data for inactive players as well.

## Request Parameters

### Required Parameters
You must pass at least one of the following parameters: `sport`, `league`, or `id`.

### Parameter Details

#### `sport`
- **Type**: String
- **Description**: The sport you want to get players for
- **Accepts**: Sport ID or sport name
- **Required**: Yes (if `league` and `id` are not provided)

#### `league` 
- **Type**: String
- **Description**: The league you want to get players for
- **Accepts**: League ID or league name
- **Required**: Yes (if `sport` and `id` are not provided)

#### `id`
- **Type**: String
- **Description**: The specific player ID you want information for
- **Required**: Yes (if `sport` and `league` are not provided)
- **Note**: When provided, this will return data for both active and inactive players

#### `include_statsperform_id`
- **Type**: Boolean
- **Description**: Specify this parameter if you want the StatsPerform IDs to be included as part of the response
- **Required**: No
- **Default**: false

When `include_statsperform_id` is enabled, you will see the StatsPerform ID populated in the `source_ids` field of each player entry:

```json
"source_ids": {
    "statsperform_id": "a2nwp4zx1mzcmk2e4dtcw5h5g"
}
```

## Response Format

The API returns a JSON object with a `data` array containing player objects. Each player object includes comprehensive information about the player.

### Response Structure

```json
{
  "data": [
    {
      // Player objects
    }
  ]
}
```

### Player Object Schema

Each player object in the response contains the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | Unique player identifier for the specific league |
| `name` | String | Full name of the player |
| `position` | String | Player's position (e.g., "QB", "RB", "G", "DT") |
| `number` | Integer | Jersey number |
| `numerical_id` | Integer/null | Numerical identifier (may be null) |
| `is_active` | Boolean | Whether the player is currently active |
| `first_name` | String | Player's first name |
| `last_name` | String | Player's last name |
| `age` | Integer | Player's age |
| `height` | Integer | Player's height in inches |
| `weight` | Integer | Player's weight in pounds |
| `experience` | Integer/null | Years of experience (may be null) |
| `logo` | String | URL to player's logo/image |
| `base_id` | Integer | Base identifier for the player |
| `source_ids` | Object | External source identifiers (includes StatsPerform ID when requested) |
| `sport` | Object | Sport information |
| `league` | Object | League information |
| `team` | Object | Current team information |

### Nested Object Structures

#### Sport Object
```json
"sport": {
  "id": "football",
  "name": "Football", 
  "numerical_id": 9
}
```

#### League Object
```json
"league": {
  "id": "nfl",
  "name": "NFL",
  "numerical_id": 367
}
```

#### Team Object
```json
"team": {
  "id": "132B64CEDAC4",
  "name": "San Francisco 49ers",
  "numerical_id": null
}
```

#### Source IDs Object
```json
"source_ids": {
  "statsperform_id": "a2nwp4zx1mzcmk2e4dtcw5h5g"
}
```

## Example Request

### NFL Players Request
```
GET https://api.opticodds.com/api/v3/players?league=NFL
```

## Example Response

**Note**: This is only used to show an example JSON format. Actual response data may differ from what is shown below.

```json
{
  "data": [
    {
      "id": "58528E9A72E6",
      "name": "Aaron Banks",
      "position": "G",
      "number": 65,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Aaron",
      "last_name": "Banks",
      "age": 27,
      "height": 76,
      "weight": 323,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1559.png",
      "base_id": 1559,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "132B64CEDAC4",
        "name": "San Francisco 49ers",
        "numerical_id": null
      }
    },
    {
      "id": "E1C6CF8263C2",
      "name": "Aaron Brewer",
      "position": "G",
      "number": 55,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Aaron",
      "last_name": "Brewer",
      "age": 27,
      "height": 72,
      "weight": 292,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1560.png",
      "base_id": 1560,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "8380A12E67FE",
        "name": "Miami Dolphins",
        "numerical_id": null
      }
    },
    {
      "id": "26715A178473",
      "name": "Aaron Brewer",
      "position": "LS",
      "number": 46,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Aaron",
      "last_name": "Brewer",
      "age": 34,
      "height": 76,
      "weight": 231,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1561.png",
      "base_id": 1561,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "AF456B375E7E",
        "name": "Arizona Cardinals",
        "numerical_id": null
      }
    },
    {
      "id": "6A8C12F44A16",
      "name": "Aaron Jones",
      "position": "RB",
      "number": 33,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Aaron",
      "last_name": "Jones",
      "age": 30,
      "height": 68,
      "weight": 206,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1564.png",
      "base_id": 1564,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "24E4EA618C5E",
        "name": "Minnesota Vikings",
        "numerical_id": null
      }
    },
    {
      "id": "16E7FD97D946",
      "name": "Aaron Rodgers",
      "position": "QB",
      "number": 8,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Aaron",
      "last_name": "Rodgers",
      "age": 41,
      "height": 73,
      "weight": 222,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1566.png",
      "base_id": 1566,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "032D4F9C6C55",
        "name": "New York Jets",
        "numerical_id": null
      }
    },
    {
      "id": "8C27E3A10D7A",
      "name": "Aaron Shampklin",
      "position": "RB",
      "number": 33,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Aaron",
      "last_name": "Shampklin",
      "age": 25,
      "height": 69,
      "weight": 193,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1567.png",
      "base_id": 1567,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "727B3B3C78E8",
        "name": "Pittsburgh Steelers",
        "numerical_id": null
      }
    },
    {
      "id": "15D6D87D37FB",
      "name": "Aaron Stinnie",
      "position": "G",
      "number": 64,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Aaron",
      "last_name": "Stinnie",
      "age": 30,
      "height": 74,
      "weight": 310,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1568.png",
      "base_id": 1568,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "ACC49FC634EE",
        "name": "New York Giants",
        "numerical_id": null
      }
    },
    {
      "id": "233712626CE6",
      "name": "Abdullah Anderson",
      "position": "DT",
      "number": 94,
      "numerical_id": null,
      "is_active": true,
      "first_name": "Abdullah",
      "last_name": "Anderson",
      "age": 29,
      "height": 75,
      "weight": 292,
      "experience": null,
      "logo": "https://cdn.opticodds.com/player-logos/football/1569.png",
      "base_id": 1569,
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      },
      "team": {
        "id": "24988863B4CB",
        "name": "Tennessee Titans",
        "numerical_id": null
      }
    }
  ]
}
```

## Additional Notes

### Pagination
This endpoint supports pagination to handle large datasets efficiently. The response will include pagination metadata to help navigate through multiple pages of results.

### Data Freshness
Player data is regularly updated to ensure accuracy of roster information, player statistics, and active status.

### Cross-League Player Tracking
When working with players who participate in multiple leagues, always use the appropriate league-specific player ID for accurate data retrieval.

### StatsPerform Integration
When the `include_statsperform_id` parameter is enabled, additional third-party identifiers are included in the response, which can be useful for data integration with other sports data services.