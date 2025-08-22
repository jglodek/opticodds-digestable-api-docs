# OpticOdds API - Active Markets Endpoint

## Overview

**Endpoint:** `/api/v3/markets/active`

**Description:** Returns a comprehensive list of all the markets that are currently available for the given fixture and/or sportsbook that are passed as parameters to the API endpoint.

## Endpoint Details

### HTTP Method
`GET`

### Base URL
`https://api.opticodds.com`

### Full Endpoint URL
`https://api.opticodds.com/api/v3/markets/active`

### Purpose and Functionality
This endpoint provides developers with access to real-time market availability data for sports betting. It returns all active betting markets that are currently offered by a specified sportsbook for a particular fixture. The endpoint is designed to help applications determine which betting options are available at any given moment, allowing for dynamic market discovery and integration into betting platforms or analytical tools.

## Query Parameters

### Available Parameters
- **`sportsbook`** - Specifies the sportsbook provider to query for available markets
- **`fixture_id`** - Identifies the specific sporting event/fixture to retrieve markets for

### Parameter Information Reference
For a complete and detailed list of all available parameters, their data types, validation rules, and usage examples, refer to the comprehensive parameter documentation located at the bottom of the API documentation page.

## Example Implementation

### Sample Request URL
```
https://api.opticodds.com/api/v3/markets/active?sportsbook=DraftKings&fixture_id=F5B0AE11A95E
```

### Request Breakdown
- **Base URL:** `https://api.opticodds.com/api/v3/markets/active`
- **Sportsbook Parameter:** `sportsbook=DraftKings`
- **Fixture Parameter:** `fixture_id=F5B0AE11A95E`
- **Query Separator:** `&` (ampersand between parameters)

## Response Format

### Content Type
`application/json`

### Response Structure
The API returns a JSON object containing a `data` array with market information objects.

### Individual Market Object Properties
Each market object in the response contains the following properties:

- **`id`** (string): A unique string identifier for the market type, using snake_case formatting
- **`name`** (string): The human-readable display name for the market
- **`numerical_id`** (integer): A unique numerical identifier for the market type

## Complete Example Response

```json
{
  "data": [
    {
      "id": "1st_half_moneyline",
      "name": "1st Half Moneyline",
      "numerical_id": 83
    },
    {
      "id": "1st_half_point_spread",
      "name": "1st Half Point Spread",
      "numerical_id": 105
    },
    {
      "id": "1st_half_team_total",
      "name": "1st Half Team Total",
      "numerical_id": 128
    },
    {
      "id": "1st_half_total_points",
      "name": "1st Half Total Points",
      "numerical_id": 152
    },
    {
      "id": "1st_half_total_points_odd_even",
      "name": "1st Half Total Points Odd/Even",
      "numerical_id": 153
    },
    {
      "id": "1st_quarter_moneyline",
      "name": "1st Quarter Moneyline",
      "numerical_id": 246
    },
    {
      "id": "1st_quarter_point_spread",
      "name": "1st Quarter Point Spread",
      "numerical_id": 256
    },
    {
      "id": "1st_quarter_team_total",
      "name": "1st Quarter Team Total",
      "numerical_id": 267
    },
    {
      "id": "1st_quarter_total_points",
      "name": "1st Quarter Total Points",
      "numerical_id": 276
    },
    {
      "id": "2nd_half_moneyline",
      "name": "2nd Half Moneyline",
      "numerical_id": 323
    },
    {
      "id": "2nd_half_point_spread",
      "name": "2nd Half Point Spread",
      "numerical_id": 336
    },
    {
      "id": "2nd_half_team_total",
      "name": "2nd Half Team Total",
      "numerical_id": 359
    },
    {
      "id": "2nd_half_total_points",
      "name": "2nd Half Total Points",
      "numerical_id": 379
    },
    {
      "id": "2nd_quarter_moneyline",
      "name": "2nd Quarter Moneyline",
      "numerical_id": 455
    },
    {
      "id": "2nd_quarter_moneyline_3-way",
      "name": "2nd Quarter Moneyline 3-Way",
      "numerical_id": 456
    },
    {
      "id": "2nd_quarter_point_spread",
      "name": "2nd Quarter Point Spread",
      "numerical_id": 458
    },
    {
      "id": "2nd_quarter_team_total",
      "name": "2nd Quarter Team Total",
      "numerical_id": 469
    },
    {
      "id": "2nd_quarter_total_points",
      "name": "2nd Quarter Total Points",
      "numerical_id": 478
    },
    {
      "id": "3rd_quarter_moneyline",
      "name": "3rd Quarter Moneyline",
      "numerical_id": 578
    },
    {
      "id": "3rd_quarter_point_spread",
      "name": "3rd Quarter Point Spread",
      "numerical_id": 581
    },
    {
      "id": "3rd_quarter_team_total",
      "name": "3rd Quarter Team Total",
      "numerical_id": 592
    },
    {
      "id": "3rd_quarter_total_points",
      "name": "3rd Quarter Total Points",
      "numerical_id": 601
    },
    {
      "id": "4th_quarter_moneyline",
      "name": "4th Quarter Moneyline",
      "numerical_id": 684
    },
    {
      "id": "4th_quarter_point_spread",
      "name": "4th Quarter Point Spread",
      "numerical_id": 691
    },
    {
      "id": "4th_quarter_team_total",
      "name": "4th Quarter Team Total",
      "numerical_id": 703
    },
    {
      "id": "4th_quarter_total_points",
      "name": "4th Quarter Total Points",
      "numerical_id": 712
    },
    {
      "id": "first_basket_including_ft",
      "name": "First Basket Including FT",
      "numerical_id": 918
    },
    {
      "id": "halftime_fulltime",
      "name": "Halftime / Fulltime",
      "numerical_id": 935
    },
    {
      "id": "moneyline",
      "name": "Moneyline",
      "numerical_id": 953
    },
    {
      "id": "player_assists",
      "name": "Player Assists",
      "numerical_id": 966
    },
    {
      "id": "player_blocks",
      "name": "Player Blocks",
      "numerical_id": 984
    },
    {
      "id": "player_double_double",
      "name": "Player Double Double",
      "numerical_id": 998
    },
    {
      "id": "player_made_threes",
      "name": "Player Made Threes",
      "numerical_id": 1061
    },
    {
      "id": "player_points",
      "name": "Player Points",
      "numerical_id": 1095
    },
    {
      "id": "player_points_+_assists",
      "name": "Player Points + Assists",
      "numerical_id": 1096
    },
    {
      "id": "player_points_+_rebounds",
      "name": "Player Points + Rebounds",
      "numerical_id": 1097
    },
    {
      "id": "player_points_+_rebounds_+_assists",
      "name": "Player Points + Rebounds + Assists",
      "numerical_id": 1098
    },
    {
      "id": "player_rebounds",
      "name": "Player Rebounds",
      "numerical_id": 1103
    },
    {
      "id": "player_rebounds_+_assists",
      "name": "Player Rebounds + Assists",
      "numerical_id": 1104
    },
    {
      "id": "player_steals",
      "name": "Player Steals",
      "numerical_id": 1145
    },
    {
      "id": "player_triple_double",
      "name": "Player Triple Double",
      "numerical_id": 1166
    },
    {
      "id": "player_turnovers",
      "name": "Player Turnovers",
      "numerical_id": 1168
    },
    {
      "id": "point_spread",
      "name": "Point Spread",
      "numerical_id": 1172
    },
    {
      "id": "team_total",
      "name": "Team Total",
      "numerical_id": 1261
    },
    {
      "id": "team_total_odd_even",
      "name": "Team Total Odd/Even",
      "numerical_id": 1283
    },
    {
      "id": "total_points",
      "name": "Total Points",
      "numerical_id": 1358
    },
    {
      "id": "total_points_odd_even",
      "name": "Total Points Odd/Even",
      "numerical_id": 1359
    },
    {
      "id": "will_there_be_overtime",
      "name": "Will There Be Overtime",
      "numerical_id": 1401
    }
  ]
}
```

## Available Market Types

### Game Period Markets
The response includes various markets organized by game periods:

**First Half Markets:**
- 1st Half Moneyline (ID: 83)
- 1st Half Point Spread (ID: 105)
- 1st Half Team Total (ID: 128)
- 1st Half Total Points (ID: 152)
- 1st Half Total Points Odd/Even (ID: 153)

**Quarter-Specific Markets:**
- 1st Quarter Moneyline (ID: 246)
- 1st Quarter Point Spread (ID: 256)
- 1st Quarter Team Total (ID: 267)
- 1st Quarter Total Points (ID: 276)
- 2nd Quarter Moneyline (ID: 455)
- 2nd Quarter Moneyline 3-Way (ID: 456)
- 2nd Quarter Point Spread (ID: 458)
- 2nd Quarter Team Total (ID: 469)
- 2nd Quarter Total Points (ID: 478)
- 3rd Quarter Moneyline (ID: 578)
- 3rd Quarter Point Spread (ID: 581)
- 3rd Quarter Team Total (ID: 592)
- 3rd Quarter Total Points (ID: 601)
- 4th Quarter Moneyline (ID: 684)
- 4th Quarter Point Spread (ID: 691)
- 4th Quarter Team Total (ID: 703)
- 4th Quarter Total Points (ID: 712)

**Second Half Markets:**
- 2nd Half Moneyline (ID: 323)
- 2nd Half Point Spread (ID: 336)
- 2nd Half Team Total (ID: 359)
- 2nd Half Total Points (ID: 379)

### Full Game Markets
**Primary Markets:**
- Moneyline (ID: 953)
- Point Spread (ID: 1172)
- Total Points (ID: 1358)
- Total Points Odd/Even (ID: 1359)

**Team-Specific Markets:**
- Team Total (ID: 1261)
- Team Total Odd/Even (ID: 1283)

**Special Game Markets:**
- First Basket Including FT (ID: 918)
- Halftime / Fulltime (ID: 935)
- Will There Be Overtime (ID: 1401)

### Player Prop Markets
**Individual Player Statistics:**
- Player Points (ID: 1095)
- Player Rebounds (ID: 1103)
- Player Assists (ID: 966)
- Player Steals (ID: 1145)
- Player Blocks (ID: 984)
- Player Made Threes (ID: 1061)
- Player Turnovers (ID: 1168)

**Combination Player Props:**
- Player Points + Assists (ID: 1096)
- Player Points + Rebounds (ID: 1097)
- Player Points + Rebounds + Assists (ID: 1098)
- Player Rebounds + Assists (ID: 1104)

**Achievement-Based Player Props:**
- Player Double Double (ID: 998)
- Player Triple Double (ID: 1166)

## Important Notes

### Data Variability Disclaimer
**IMPORTANT:** The example responses provided in this documentation are solely intended to demonstrate the JSON format structure and field names returned by the API. The actual data content, including available markets, numerical IDs, and market names, may differ significantly from the examples shown depending on:

- The specific sportsbook queried
- The particular fixture or sporting event
- The current time and market availability
- Regional restrictions or regulations
- Sportsbook-specific market offerings

### Dynamic Market Availability
Markets returned by this endpoint are dynamic and change in real-time based on:
- Sportsbook operational status
- Game timing and live betting availability  
- Regulatory requirements
- Market suspension due to injuries or other events
- Sportsbook's individual market offering policies

### Integration Considerations
When integrating this endpoint into applications:
- Implement proper error handling for cases where no markets are available
- Cache market data appropriately but refresh regularly to maintain accuracy
- Handle cases where previously available markets become unavailable
- Consider implementing fallback logic for essential market types

## Technical Implementation Support

### Available Code Examples
The API documentation provides implementation examples in multiple programming languages:
- Shell/cURL commands
- Node.js/JavaScript
- Ruby
- PHP  
- Python

### Interactive Testing
A "Try It!" interactive testing interface is available within the API documentation to allow developers to test the endpoint with various parameter combinations and observe real-time responses before implementing in their applications.