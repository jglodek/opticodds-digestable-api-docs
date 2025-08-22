# Futures Grader API Documentation

## Overview

**Endpoint:** `GET /api/v3/grader/futures`

**Base URL:** `https://api.opticodds.com`

**Description:** Get the graded result of a future bet. This endpoint allows you to retrieve the settlement status and results for future bets placed on sporting events.

**Current Sport Support:** Currently this endpoint only supports `golf` as the sport parameter.

## Request Parameters

### Required Parameters

#### `sport`
- **Type:** String
- **Description:** The sport of the fixture for which you want to grade the bet
- **Current Supported Values:** `golf`
- **Required:** Yes

#### `league`
- **Type:** String  
- **Description:** The league of the fixture for which you want to grade the bet
- **Example:** `PGA`
- **Required:** Yes

#### `tournament_id`
- **Type:** String
- **Description:** The unique identifier of the tournament/fixture that the bet applies to. This is used to specify exactly which tournament or event the bet was placed on.
- **Example:** `0D9C9CCC70BF`
- **Required:** Yes

#### `market`
- **Type:** String (URL encoded)
- **Description:** The specific market type of the bet you are trying to grade. This defines what type of bet was placed within the tournament.
- **Examples:**
  - `BMW Championship 2024 Winner`
  - `BMW Championship 2024 Top 5 Finish`
- **Required:** Yes
- **Note:** When passing this parameter in the URL, ensure it is properly URL encoded (spaces become `%20`)

#### `name`
- **Type:** String
- **Description:** The name of the player or selection that the bet was placed on. This should match the name as it appears in the betting market.
- **Examples:**
  - `Tiger Woods`
  - `Aaron Rai`
  - `Tommy Fleetwood`
- **Required:** Yes

### Optional Parameters

#### `player_id`
- **Type:** String
- **Description:** Sometimes due to the various naming conventions used by different sportsbooks, player names are not uniform across platforms. Passing a `player_id` will use the corresponding player record if there are issues resolving the `name` parameter. This helps ensure accurate bet grading when name variations exist.
- **Required:** No
- **Use Case:** Recommended when dealing with player names that might have variations in spelling, formatting, or when names contain special characters

#### `show_live_results`
- **Type:** Boolean
- **Description:** In some cases, bet results can be graded before the tournament or game is fully completed. Setting this parameter to `true` will return the live result at the time the endpoint is called, rather than waiting for final confirmation.
- **Required:** No
- **Default Behavior:** The endpoint waits until the game/tournament is completed before returning results
- **Caution:** Use this parameter carefully, as the default behavior exists to account for in-game statistical corrections, official result confirmations, or any other result-related issues that might occur during live play

## Response Format

### Success Response Structure

The API returns a JSON response with the following structure:

```json
{
  "data": {
    "tournament_id": "string",
    "tournament_name": "string", 
    "status": "string",
    "market": "string",
    "name": "string",
    "result": "string",
    "dead_heat_reduction": number|null
  }
}
```

### Response Fields

#### `tournament_id`
- **Type:** String
- **Description:** The unique identifier for the tournament, matching the input parameter

#### `tournament_name`
- **Type:** String
- **Description:** The full, human-readable name of the tournament or event

#### `status`
- **Type:** String
- **Description:** The current status of the tournament
- **Possible Values:** `Completed`, `Live`, `Upcoming`, `Cancelled`

#### `market`
- **Type:** String
- **Description:** The betting market type, matching the input parameter

#### `name`
- **Type:** String
- **Description:** The player or selection name that was bet on

#### `result`
- **Type:** String
- **Description:** The final grading result of the bet
- **Possible Values:**
  - `Won` - The bet is settled as a win
  - `Lost` - The bet is settled as a loss  
  - `Refunded` - The bet is settled as a push/refund
  - `Pending` - The bet has not yet been confirmed. This may occur because the fixture has not been completed or the results have not been officially confirmed

#### `dead_heat_reduction`
- **Type:** Number or null
- **Description:** The dead heat reduction factor applied to the bet payout, if applicable. This value represents the divisor used when multiple selections tie for the same position, affecting the payout calculation.
- **Null Value:** When there is no dead heat situation, this field will be `null`
- **Example:** A value of `4` means the payout is divided by 4 due to a 4-way tie
- **Reference:** More detailed information about dead heat reductions can be found in the linked documentation

## Example Requests and Responses

### Example 1: Standard Winner Bet (Lost)

**Request URL:**
```
https://api.opticodds.com/api/v3/grader/futures?sport=golf&league=PGA&tournament_id=0D9C9CCC70BF&market=BMW%20Championship%202024%20Winner&name=Aaron%20Rai
```

**Response:**
```json
{
  "data": {
    "tournament_id": "0D9C9CCC70BF",
    "tournament_name": "BMW Championship 2024",
    "status": "Completed",
    "market": "BMW Championship 2024 Winner",
    "name": "Aaron Rai",
    "result": "Lost",
    "dead_heat_reduction": null
  }
}
```

### Example 2: Top 5 Finish Bet with Dead Heat (Won)

**Request URL:**
```
https://api.opticodds.com/api/v3/grader/futures?sport=golf&league=PGA&tournament_id=0D9C9CCC70BF&market=BMW%20Championship%202024%20Top%205%20Finish&name=Tommy%20Fleetwood
```

**Response:**
```json
{
  "data": {
    "tournament_id": "0D9C9CCC70BF",
    "tournament_name": "BMW Championship 2024", 
    "status": "Completed",
    "market": "BMW Championship 2024 Top 5 Finish",
    "name": "Tommy Fleetwood",
    "result": "Won",
    "dead_heat_reduction": 4
  }
}
```

## Error Handling

### Error Response Format

When an error occurs, the API returns a JSON response with the following structure:

```json
{
  "message": "Error description",
  "code": integer
}
```

### Complete Error Code Reference

#### General Game/Tournament Errors (100-109)

| Code | Message | Description |
|------|---------|-------------|
| 100 | "Game not found" | The specified game or tournament could not be located in the system |
| 101 | "Sport not supported" | The requested sport is not currently supported by this endpoint |
| 102 | "League not supported" | The specified league is not supported for the given sport |
| 103 | "Bet type not supported" | The requested bet type or market is not supported |
| 104 | "Game is still live" | The game/tournament is currently in progress and results are not yet available |
| 105 | "Tournament not found" | The specified tournament ID could not be found |
| 106 | "Tournament is still live" | The tournament is currently ongoing and final results are not available |
| 107 | "Game has not started" | The game or tournament has not yet begun |
| 108 | "Game has not completed" | The game or tournament is not yet finished |
| 109 | "Game has been canceled" | The game or tournament has been officially cancelled |

#### Data and Score Related Errors (201-218)

| Code | Message | Description |
|------|---------|-------------|
| 201 | "Score data not found" | Score or result data is not available for the specified event |
| 202 | "Incomplete score data" | The available score data is incomplete or missing key information |
| 203 | "Unsupported bet period" | The specified betting period is not supported |
| 204 | "Unsupported spread" | The spread bet type is not supported for this event |
| 205 | "Team not in spread" | The specified team is not included in the spread betting options |
| 206 | "Unsupported over/under" | The over/under bet type is not supported for this event |
| 207 | "Team not in over/under" | The specified team is not included in over/under betting options |
| 208 | "Unsupported both teams to score" | The "both teams to score" bet type is not supported |
| 209 | "Unsupported moneyline" | The moneyline bet type is not supported for this event |
| 210 | "Unsupported bet type" | The specified bet type is not supported |
| 211 | "Unsupported player name format" | The player name format provided is not recognized |
| 212 | "Unknown player" | The specified player cannot be found in the system |
| 213 | "Incomplete player data" | Player data is incomplete or missing required information |
| 214 | "Unsupported player over/under" | Player-specific over/under bets are not supported |
| 215 | "Unsupported go the distance" | "Go the distance" bet type is not supported |
| 216 | "Unsupported total rounds" | Total rounds bet type is not supported |
| 217 | "Tournament leaderboard not found" | The tournament leaderboard data is not available |
| 218 | "Match ended in retirement" | The match ended due to a player retirement, affecting bet grading |

## Usage Notes and Best Practices

### Parameter Encoding
- Ensure that all URL parameters are properly encoded, especially the `market` and `name` parameters which may contain spaces and special characters
- Spaces should be encoded as `%20` in the URL

### Dead Heat Situations
- Pay special attention to the `dead_heat_reduction` field when processing winning bets
- A non-null value indicates that the payout should be divided by the specified number due to tied positions
- This is common in golf tournaments where multiple players may tie for finishing positions

### Result Timing
- By default, the API waits for official tournament completion before returning final results
- Use the `show_live_results` parameter cautiously, as live results may change due to official corrections or disqualifications

### Player Name Resolution
- When dealing with player names that may have variations across different sportsbooks, consider using the `player_id` parameter for more reliable matching
- This helps avoid issues with different name spellings, abbreviations, or formatting conventions

### Error Handling
- Implement proper error handling for all possible error codes
- Code ranges 100-109 typically indicate issues with tournament/game identification
- Code ranges 201-218 typically indicate data availability or bet type support issues