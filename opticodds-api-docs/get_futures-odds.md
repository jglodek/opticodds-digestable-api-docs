# Futures Odds API Documentation

## Endpoint Overview

This API endpoint retrieves a comprehensive list of future odds for a specific combination of sportsbooks, leagues, and betting markets. The odds data relates to specific future events and does not apply to entire tournaments or complete seasons.

**Base URL**: `https://api.opticodds.com/api/v3/futures/odds`

**HTTP Method**: `GET`

## Description

Get a list of future odds for a given combination of sportsbooks, leagues, and markets. These game odds are related to specific events, they do not apply for entire tournaments or entire seasons.

## Required Parameters

You must pass at least one of the following parameters:
- `league`
- `future_id` 
- `future`
- `player_id`
- `team_id`

Additionally, you must specify at least 1 sportsbook and at most 5 sportsbooks.

## Parameter Details

### `future_id`
- **Type**: String
- **Limit**: Up to 5 values per request
- **Description**: Unique identifier for specific futures markets
- **Example**: `type_championship_winner-sport_basketball-league_nba`

### `sportsbook`
- **Type**: String or ID
- **Limit**: 1-5 sportsbooks per request
- **Description**: The sportsbooks that you want odds for. You can pass either the sportsbook ID or the sportsbook name.

### `future`
- **Type**: String or ID
- **Description**: The specific futures markets that you want odds for. You can pass either the future ID or the future name.
- **Example**: `Championship Winner`

### `league`
- **Type**: String
- **Description**: The sports league identifier (e.g., MLB, NBA, NFL)

### `player_id`
- **Type**: String
- **Description**: Unique identifier for a specific player

### `team_id`
- **Type**: String
- **Description**: Unique identifier for a specific team

### `is_main`
- **Type**: Boolean
- **Description**: This parameter indicates whether a line is the "main" or "given" line for a market. For example, the +/- 6 Point Spread and the Over/Under 46.5 Total Points lines are the "main" lines for a given market.

### `odds_format`
- **Type**: String
- **Default**: `AMERICAN`
- **Accepted Values**: 
  - `AMERICAN`
  - `DECIMAL`
  - `PROBABILITY`
  - `MALAY`
  - `HONG_KONG`
  - `INDONESIAN`
- **Description**: Specifies the format for odds display

## Response Structure

The API returns a JSON object with the following structure:

```json
{
  "data": [
    {
      "id": "string",
      "sport": {
        "id": "string",
        "name": "string"
      },
      "league": {
        "id": "string", 
        "name": "string"
      },
      "tournament": null,
      "name": "string",
      "future_type": "string",
      "start_date": "string (ISO 8601)",
      "odds": [
        {
          "id": "string",
          "sportsbook": "string",
          "market": "string",
          "name": "string",
          "price": "number",
          "timestamp": "number",
          "is_main": "boolean",
          "selection": "string",
          "normalized_selection": "string",
          "market_id": "string",
          "selection_line": "string or null",
          "player_id": "string or null",
          "team_id": "string or null",
          "points": "number or null"
        }
      ]
    }
  ]
}
```

## Response Field Descriptions

### Root Level Fields
- **`id`**: Unique identifier for the futures market
- **`sport`**: Object containing sport ID and name
- **`league`**: Object containing league ID and name  
- **`tournament`**: Tournament information (typically null for futures)
- **`name`**: Display name of the futures market
- **`future_type`**: Type of future bet (e.g., "TEAM", "PLAYER", "UNKNOWN")
- **`start_date`**: ISO 8601 formatted date when the future resolves

### Odds Array Fields
- **`id`**: Unique identifier for the specific odds entry
- **`sportsbook`**: Name of the sportsbook providing the odds
- **`market`**: Name of the betting market
- **`name`**: Display name for the selection
- **`price`**: Odds value in the specified format
- **`timestamp`**: Unix timestamp of when odds were last updated
- **`is_main`**: Boolean indicating if this is the main line for the market
- **`selection`**: Human-readable selection name
- **`normalized_selection`**: Normalized version of selection name
- **`market_id`**: Identifier for the market
- **`selection_line`**: Line designation (e.g., "over", "under") or null
- **`player_id`**: Player identifier if applicable, otherwise null
- **`team_id`**: Team identifier if applicable, otherwise null  
- **`points`**: Point value for spread/total bets, otherwise null

## Example Request

```
GET https://api.opticodds.com/api/v3/futures/odds?league=MLB&sportsbook=DraftKings
```

## Example Response

The response contains comprehensive futures betting data for MLB from DraftKings, including various markets such as:

- **Division Winners**: AL Central, AL East, AL West, NL Central, NL East, NL West
- **League Championships**: American League Winner, National League Winner
- **Individual Awards**: MVP, Cy Young Winner, Rookie of the Year for both leagues
- **World Series**: World Series Winner, World Series League Winner
- **Player Props**: Individual player achievements like home run totals

Each market contains multiple betting options with current odds, timestamps, and detailed metadata for accurate odds tracking and comparison.

## Usage Notes

- All timestamps are provided in Unix format for precise time tracking
- Odds are updated in real-time and include timestamp information
- The `is_main` field helps identify the primary betting lines versus alternative lines
- Player and team IDs provide consistent identification across different markets
- Multiple odds formats are supported to accommodate different regional preferences
- Response includes comprehensive metadata for each betting market and selection