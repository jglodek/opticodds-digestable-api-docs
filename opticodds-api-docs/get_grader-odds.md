# Bet Grader API Documentation

## Overview

### Description
Get the graded result of a bet. This endpoint allows you to retrieve the outcome of a specific bet placed on a sports fixture, providing detailed information about whether the bet was won, lost, refunded, or is still pending.

## Endpoint Information

**Base URL:** `https://api.opticodds.com/api/v3/grader/odds`

**HTTP Method:** GET

## Request Parameters

### Required Parameters

#### `sport`
**Type:** String  
**Description:** The sport of the fixture for which you want to grade the bet. This parameter specifies the sporting event category.

#### `league`
**Type:** String  
**Description:** The league of the fixture. This parameter identifies the specific league or competition within the sport where the fixture takes place.

#### `fixture_id`
**Type:** String  
**Description:** The unique identifier of the fixture that the bet applies to. This ID is used to specify the exact game or match for bet grading purposes.

#### `market`
**Type:** String  
**Description:** The market of the bet you are trying to grade. **Important:** Make sure to pass the market label, not the market ID.

**Examples of correct market labels:**
- `Moneyline` (instead of `moneyline`)
- `Point Spread` (instead of `point_spread`)
- `Total Rounds`
- `Over/Under`

#### `name`
**Type:** String  
**Description:** The specific name of the bet you are trying to grade. This should be the exact bet selection name.

**Examples of bet names:**
- `Buffalo Bills`
- `Over 10.5`
- `Aaron Judge Under 10.5`
- `Under 2.5`

### Optional Parameters

#### `player_id`
**Type:** String  
**Description:** Due to the various naming conventions used by different sportsbooks, player names may not be uniform across platforms. Passing a `player_id` parameter will use the corresponding player identifier if there are issues resolving the `bet_name`. This parameter helps ensure accurate bet grading when player name discrepancies exist between different data sources.

#### `show_live_results`
**Type:** Boolean  
**Description:** Some betting results can be graded before the game is fully completed. Passing this parameter will return the live result at the time the endpoint is called. 

**⚠️ Use with caution:** The default behavior for this endpoint is to wait until the game is completed before returning any results. This default approach accounts for:
- In-game statistical corrections
- Official score changes
- Other stat-related issues that may occur during live gameplay

Setting this parameter to `true` may result in preliminary results that could change before the final game completion.

## Response Format

### Success Response Structure

The API returns a JSON object with the following structure:

```json
{
  "data": {
    "fixture_id": "string",
    "away_team_display": "string",
    "home_team_display": "string", 
    "status": "string",
    "away_score": number,
    "home_score": number,
    "player_score": number|null,
    "market": "string",
    "name": "string",
    "result": "string"
  }
}
```

### Response Fields Description

#### `fixture_id`
**Type:** String  
**Description:** The unique identifier of the fixture, matching the input parameter.

#### `away_team_display`
**Type:** String  
**Description:** The display name of the away team or participant in the fixture.

#### `home_team_display`
**Type:** String  
**Description:** The display name of the home team or participant in the fixture.

#### `status`
**Type:** String  
**Description:** The current status of the fixture (e.g., "Completed", "Live", "Pending").

#### `away_score`
**Type:** Number  
**Description:** The final or current score of the away team.

#### `home_score`
**Type:** Number  
**Description:** The final or current score of the home team.

#### `player_score`
**Type:** Number|Null  
**Description:** The score or statistical value for player-specific bets. Will be `null` for team-based bets.

#### `market`
**Type:** String  
**Description:** The market type of the graded bet, matching the input parameter.

#### `name`
**Type:** String  
**Description:** The specific bet name that was graded, matching the input parameter.

#### `result`
**Type:** String  
**Description:** The outcome of the bet grading process.

### Possible Result Values

The `result` field can contain the following values:

#### `Won`
**Description:** The bet is settled as a win. The bettor's wager was successful and they are entitled to winnings based on the odds.

#### `Lost`
**Description:** The bet is settled as a loss. The bettor's wager was unsuccessful and the stake is forfeited.

#### `Refunded`
**Description:** The bet is settled as a push or refund. This typically occurs when the actual result exactly matches the spread or total, resulting in neither a win nor loss. The bettor receives their original stake back.

#### `Pending`
**Description:** The bet has not yet been confirmed or graded. Reasons for pending status may include:
- The fixture has not been completed
- The results have not been officially confirmed
- Statistical data is still being verified
- There are ongoing reviews of the game results

#### `Half Won`
**Description:** This result applies specifically to Asian handicap markets. In Asian betting markets, it's possible to win half of your bet when the margin falls on a quarter-point spread.

#### `Half Lost`
**Description:** This result applies specifically to Asian handicap markets. In Asian betting markets, it's possible to lose half of your bet when the margin falls on a quarter-point spread.

## Example Request and Response

### Example Request URL
```
https://api.opticodds.com/api/v3/grader/odds?sport=mma&league=ufc&fixture_id=B848DE682885&market=Total%20Rounds&name=Under%202.5
```

### Example Response
```json
{
  "data": {
    "fixture_id": "B848DE682885",
    "away_team_display": "Tracy Cortez",
    "home_team_display": "Rose Namajunas",
    "status": "Completed",
    "away_score": 0,
    "home_score": 1,
    "player_score": null,
    "market": "Total Rounds",
    "name": "Under 2.5",
    "result": "Lost"
  }
}
```

## Error Handling

The API uses structured error codes to indicate different types of failures. All errors are returned as JSON objects with a `message` and `code` field.

### General Game/Tournament Errors (100-109)

#### Code 100: Game Not Found
```json
{"message": "Game not found", "code": 100}
```
**Description:** The specified `fixture_id` does not exist in the system or cannot be located.

#### Code 101: Sport Not Supported
```json
{"message": "Sport not supported", "code": 101}
```
**Description:** The specified `sport` parameter is not supported by the API.

#### Code 102: League Not Supported
```json
{"message": "League not supported", "code": 102}
```
**Description:** The specified `league` parameter is not supported within the given sport.

#### Code 103: Bet Type Not Supported
```json
{"message": "Bet type not supported", "code": 103}
```
**Description:** The specified betting market or bet type is not supported for grading.

#### Code 104: Game Is Still Live
```json
{"message": "Game is still live", "code": 104}
```
**Description:** The game is currently in progress and final results are not yet available for grading.

#### Code 105: Tournament Not Found
```json
{"message": "Tournament not found", "code": 105}
```
**Description:** The specified tournament cannot be located in the system.

#### Code 106: Tournament Is Still Live
```json
{"message": "Tournament is still live", "code": 106}
```
**Description:** The tournament is currently ongoing and final results are not yet available.

#### Code 107: Game Has Not Started
```json
{"message": "Game has not started", "code": 107}
```
**Description:** The specified game has not yet begun, so no results are available for grading.

#### Code 108: Game Has Not Completed
```json
{"message": "Game has not completed", "code": 108}
```
**Description:** The game is not yet finished, and complete results are not available for final grading.

#### Code 109: Game Has Been Canceled
```json
{"message": "Game has been canceled", "code": 109}
```
**Description:** The specified game has been canceled and no results will be available.

### Data and Scoring Errors (201-218)

#### Code 201: Score Data Not Found
```json
{"message": "Score data not found", "code": 201}
```
**Description:** No scoring data is available for the specified fixture.

#### Code 202: Incomplete Score Data
```json
{"message": "Incomplete score data", "code": 202}
```
**Description:** The scoring data for the fixture is incomplete and cannot be used for accurate bet grading.

#### Code 203: Unsupported Bet Period
```json
{"message": "Unsupported bet period", "code": 203}
```
**Description:** The specific time period or segment of the game for this bet type is not supported.

#### Code 204: Unsupported Spread
```json
{"message": "Unsupported spread", "code": 204}
```
**Description:** The point spread value or type specified in the bet is not supported for grading.

#### Code 205: Team Not in Spread
```json
{"message": "Team not in spread", "code": 205}
```
**Description:** The specified team is not found in the available spread betting options for this fixture.

#### Code 206: Unsupported Over/Under
```json
{"message": "Unsupported over/under", "code": 206}
```
**Description:** The over/under total specified in the bet is not supported or cannot be graded.

#### Code 207: Team Not in Over/Under
```json
{"message": "Team not in over/under", "code": 207}
```
**Description:** The specified team is not found in the available over/under betting options.

#### Code 208: Unsupported Both Teams to Score
```json
{"message": "Unsupported both teams to score", "code": 208}
```
**Description:** The "both teams to score" market is not supported for this fixture or sport.

#### Code 209: Unsupported Moneyline
```json
{"message": "Unsupported moneyline", "code": 209}
```
**Description:** The moneyline bet type is not supported for the specified fixture.

#### Code 210: Unsupported Bet Type
```json
{"message": "Unsupported bet type", "code": 210}
```
**Description:** The general bet type specified is not supported by the grading system.

#### Code 211: Unsupported Player Name Format
```json
{"message": "Unsupported player name format", "code": 211}
```
**Description:** The format of the player name provided cannot be processed by the system.

#### Code 212: Unknown Player
```json
{"message": "Unknown player", "code": 212}
```
**Description:** The specified player cannot be identified in the system database.

#### Code 213: Incomplete Player Data
```json
{"message": "Incomplete player data", "code": 213}
```
**Description:** The available player data is insufficient for accurate bet grading.

#### Code 214: Unsupported Player Over/Under
```json
{"message": "Unsupported player over/under", "code": 214}
```
**Description:** The player-specific over/under bet type is not supported for grading.

#### Code 215: Unsupported Go the Distance
```json
{"message": "Unsupported go the distance", "code": 215}
```
**Description:** The "go the distance" bet type (typically used in combat sports) is not supported.

#### Code 216: Unsupported Total Rounds
```json
{"message": "Unsupported total rounds", "code": 216}
```
**Description:** The total rounds bet type is not supported for the specified fixture.

#### Code 217: Tournament Leaderboard Not Found
```json
{"message": "Tournament leaderboard not found", "code": 217}
```
**Description:** The tournament leaderboard data required for bet grading cannot be located.

#### Code 218: Match Ended in Retirement
```json
{"message": "Match ended in retirement", "code": 218}
```
**Description:** The match ended due to a participant's retirement, which may affect bet grading rules.

## Usage Notes

1. **Parameter Encoding:** When making HTTP requests, ensure that parameter values are properly URL-encoded, especially for market names and bet names that contain spaces or special characters.

2. **Case Sensitivity:** Market labels are case-sensitive. Always use the exact market label format as specified in the documentation.

3. **Real-time vs Final Results:** By default, the API waits for game completion before returning results. Use the `show_live_results` parameter only when you specifically need real-time data and understand the risks of potential result changes.

4. **Player Identification:** When dealing with player props, use the `player_id` parameter if you encounter issues with player name resolution due to variations in naming conventions across different sportsbooks.

5. **Error Handling:** Implement proper error handling in your application to gracefully manage the various error codes returned by the API, particularly for common scenarios like games still in progress or unsupported bet types.