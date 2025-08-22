# OpticOdds Copilot Parlay Odds API Documentation

## Endpoint Overview

**Endpoint:** `/api/v3/copilot/parlay/odds`  
**Method:** `GET`  
**Base URL:** `https://api.opticodds.com`  
**Full URL:** `https://api.opticodds.com/api/v3/copilot/parlay/odds`

## Description

This API endpoint retrieves the calculated price for a parlay containing the requested bets. The endpoint is specifically designed to handle complex parlay calculations and takes into account Same Game Parlays (SGPs) as well as traditional cross-game parlays. The pricing mechanism considers the correlation between different bets within the same game and provides accurate odds calculation for the combined parlay wager.

The endpoint processes multiple copilot odd identifiers and returns the individual leg prices along with the combined parlay price, allowing users to understand both the component pricing and the final parlay valuation.

## Parameters

### Query Parameters

#### `id` (Required, Multiple)
- **Type:** String
- **Description:** The unique identifiers of the copilot odds that you want included in the parlay price calculation
- **Format:** Colon-separated string containing multiple components
- **Multiple Values:** Yes - you can include multiple `id` parameters in a single request to build a multi-leg parlay
- **Example Values:**
  - `2:-1:nba:9818DC020C5E:moneyline:atlanta_hawks`
  - `2:-1:nba:9818DC020C5E:player_points:aaron_nesmith_under_12_5`

**ID Format Breakdown:**
The copilot odd ID follows a structured format with colon-separated components:
- **Component 1:** Numeric identifier (e.g., `2`)
- **Component 2:** Numeric value, often negative (e.g., `-1`)
- **Component 3:** League/sport identifier (e.g., `nba`)
- **Component 4:** Alphanumeric game/event identifier (e.g., `9818DC020C5E`)
- **Component 5:** Bet type identifier (e.g., `moneyline`, `player_points`)
- **Component 6:** Specific bet selection (e.g., `atlanta_hawks`, `aaron_nesmith_under_12_5`)

## Request Example

### HTTP Request
```http
GET /api/v3/copilot/parlay/odds?id=2:-1:nba:9818DC020C5E:moneyline:atlanta_hawks&id=2:-1:nba:9818DC020C5E:player_points:aaron_nesmith_under_12_5 HTTP/1.1
Host: api.opticodds.com
```

### Full URL Example
```
https://api.opticodds.com/api/v3/copilot/parlay/odds?id=2:-1:nba:9818DC020C5E:moneyline:atlanta_hawks&id=2:-1:nba:9818DC020C5E:player_points:aaron_nesmith_under_12_5
```

## Response Format

### Response Structure

The API returns a JSON response with a nested data structure containing comprehensive parlay information.

### Success Response Schema

```json
{
    "data": {
        "error": null,
        "missing_entries": null,
        "legs": [
            {
                "id": "string",
                "price": number
            }
        ],
        "price": number
    }
}
```

### Response Fields Description

#### Root Level
- **`data`** (Object): The main container object for all response data

#### Data Object Properties
- **`error`** (null | String): Error message if any issues occurred during processing, otherwise null for successful requests
- **`missing_entries`** (null | Array): Contains information about any requested bet IDs that could not be found or processed, otherwise null if all entries were successfully located
- **`legs`** (Array of Objects): An array containing detailed information about each individual bet leg included in the parlay
- **`price`** (Number): The final calculated price for the entire parlay combination, represented as a decimal number

#### Legs Array Object Properties
Each object in the `legs` array contains:
- **`id`** (String): The exact copilot odd identifier that was requested, matching the input parameter
- **`price`** (Number): The individual price/odds for this specific bet leg, represented as a decimal number (can be positive or negative based on standard American odds format)

### Example Response

```json
{
    "data": {
        "error": null,
        "missing_entries": null,
        "legs": [
            {
                "id": "2:-1:nba:9818DC020C5E:moneyline:atlanta_hawks",
                "price": 135.0
            },
            {
                "id": "2:-1:nba:9818DC020C5E:player_points:aaron_nesmith_under_12_5",
                "price": -114.0
            }
        ],
        "price": 278.0
    }
}
```

### Response Interpretation

In the example response above:
- **First Leg:** Atlanta Hawks moneyline bet with odds of +135 (indicating an underdog position)
- **Second Leg:** Aaron Nesmith under 12.5 points with odds of -114 (indicating a slight favorite)
- **Combined Parlay Price:** +278, meaning a successful parlay would pay out at +278 odds

The parlay price calculation takes into account the correlation between bets (especially important for Same Game Parlays) and provides the true odds for the combined wager rather than a simple multiplication of individual odds.

## Error Handling

### Potential Error Scenarios

1. **Invalid ID Format:** If the provided copilot odd ID doesn't match the expected format
2. **Missing Entries:** When requested bet IDs cannot be found in the system
3. **Calculation Errors:** Issues during parlay price computation
4. **System Errors:** General API or server-side issues

### Error Response Format

When errors occur, the response will include details in the `error` field of the data object, and missing or invalid entries may be listed in the `missing_entries` array.

## Usage Notes

- **Same Game Parlays (SGPs):** The endpoint automatically detects and properly prices bets from the same game, applying appropriate correlation adjustments
- **Cross-Game Parlays:** Bets from different games are combined using standard parlay calculations
- **Multiple Legs:** You can include as many legs as needed by adding multiple `id` parameters to the query string
- **Price Format:** All prices are returned in American odds format (positive numbers for underdogs, negative for favorites)
- **Real-time Pricing:** Prices reflect current market conditions and may change based on betting activity and line movements