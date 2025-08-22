# OpticOdds API v3 - Get Fixture Odds

## Description

Get a list of odds for a given combination of fixtures, and markets. These odds are related to specific events, they do not apply for entire tournaments or entire seasons.

## Endpoint

**GET** `https://api.opticodds.com/api/v3/copilot/fixtures/odds`

## Specific Parameter Information

For a full list of parameters, scroll to the bottom of this page.

**Important**: You must pass at least one of the following parameters (`fixture_id`, `team_id`, `player_id`) and at most 5.

### Required Parameters (at least one)

#### `fixture_id`
- **Type**: String
- **Description**: Can pass up to 5 of these per request
- **Maximum**: 5 fixture IDs per request
- **Example**: `032B6289DB25`

#### `team_id`
- **Type**: String
- **Description**: Team identifier for filtering odds
- **Maximum**: 5 team IDs per request

#### `player_id`
- **Type**: String
- **Description**: Player identifier for filtering odds
- **Maximum**: 5 player IDs per request

### Optional Parameters

#### `market`
- **Type**: String
- **Description**: The markets that you want odds for. You can pass the id or the name
- **Examples**: `point_spread`, `Point Spread`, `total_points`, `moneyline`

#### `is_main`
- **Type**: Boolean
- **Description**: This parameter indicates whether a line is the "main" or "given" line for a market. For example, the +/- 6 Point Spread and the Over/Under 46.5 Total Points lines are the "main" lines for the DraftKings game
- **Values**: `true`, `false`

#### `odds_format`
- **Type**: String
- **Description**: The format for displaying odds values
- **Default**: `AMERICAN`
- **Accepted Values**:
  - `AMERICAN`
  - `DECIMAL`
  - `PROBABILITY`
  - `MALAY`
  - `HONG_KONG`
  - `INDONESIAN`

## Example Request

```
GET https://api.opticodds.com/api/v3/copilot/fixtures/odds?fixture_id=032B6289DB25
```

## Response Format

The API returns a JSON object with a `data` array containing fixture information and associated odds.

### Response Structure

```json
{
  "data": [
    {
      "id": "string",
      "game_id": "string", 
      "start_date": "ISO 8601 datetime",
      "home_competitors": [competitor_object],
      "away_competitors": [competitor_object],
      "home_team_display": "string",
      "away_team_display": "string",
      "status": "string",
      "is_live": boolean,
      "sport": sport_object,
      "league": league_object,
      "tournament": tournament_object_or_null,
      "odds": [odds_object]
    }
  ]
}
```

### Response Field Descriptions

#### Root Level Fields

- **`id`**: Unique identifier for the fixture (string)
- **`game_id`**: Game identifier in format "number-number-number-number" (string)
- **`start_date`**: ISO 8601 formatted datetime string indicating when the fixture starts
- **`home_competitors`**: Array of competitor objects representing the home team(s)
- **`away_competitors`**: Array of competitor objects representing the away team(s)
- **`home_team_display`**: Display name for the home team (string)
- **`away_team_display`**: Display name for the away team (string)
- **`status`**: Current status of the fixture (string, e.g., "unplayed", "live", "completed")
- **`is_live`**: Boolean indicating if the fixture is currently live
- **`sport`**: Object containing sport information
- **`league`**: Object containing league information
- **`tournament`**: Object containing tournament information, or null if not applicable
- **`odds`**: Array of odds objects containing all betting lines for this fixture

#### Competitor Object Structure

```json
{
  "id": "string",
  "name": "string",
  "abbreviation": "string",
  "logo": "string (URL)"
}
```

- **`id`**: Unique identifier for the competitor
- **`name`**: Full name of the competitor/team
- **`abbreviation`**: Abbreviated name/code for the competitor
- **`logo`**: URL to the competitor's logo image

#### Sport Object Structure

```json
{
  "id": "string",
  "name": "string"
}
```

- **`id`**: Unique identifier for the sport (e.g., "football")
- **`name`**: Display name for the sport (e.g., "Football")

#### League Object Structure

```json
{
  "id": "string",
  "name": "string"
}
```

- **`id`**: Unique identifier for the league (e.g., "nfl")
- **`name`**: Display name for the league (e.g., "NFL")

#### Odds Object Structure

```json
{
  "id": "string",
  "version_id": integer,
  "version": "string",
  "odd_id": "string",
  "market": "string",
  "name": "string",
  "is_main": boolean,
  "selection": "string",
  "normalized_selection": "string",
  "market_id": "string",
  "price": number,
  "timestamp": number,
  "grouping_key": "string",
  "points": number_or_null,
  "selection_line": any_or_null,
  "player_id": string_or_null,
  "team_id": string_or_null
}
```

#### Odds Field Descriptions

- **`id`**: Unique identifier for this specific odds entry, format: "version_id:version_id:fixture_id:market_id:selection_identifier"
- **`version_id`**: Version identifier for the odds (integer, -1 for default)
- **`version`**: Version name (string, "default" for main version)
- **`odd_id`**: Shorter odds identifier without version prefix
- **`market`**: Human-readable market name (e.g., "Point Spread", "Total Points")
- **`name`**: Full descriptive name of the betting option (e.g., "Los Angeles Rams +2.5")
- **`is_main`**: Boolean indicating if this is the main/featured line for the market
- **`selection`**: The entity being bet on (team name, player name, etc.)
- **`normalized_selection`**: Lowercase, underscore-separated version of the selection for programmatic use
- **`market_id`**: Machine-readable market identifier (e.g., "point_spread", "total_points")
- **`price`**: The odds value in the requested format (default American format, negative/positive integers)
- **`timestamp`**: Unix timestamp with decimal precision indicating when these odds were last updated
- **`grouping_key`**: Key used to group related odds together (format: "version:line_value")
- **`points`**: Point spread or total points value (number), null for markets without point values
- **`selection_line`**: Additional line information specific to the selection, null if not applicable
- **`player_id`**: Unique identifier for the player if this is a player-specific bet, null otherwise
- **`team_id`**: Unique identifier for the team associated with this selection, null if not team-specific

## Example Response

```json
{
  "data": [
    {
      "id": "032B6289DB25",
      "game_id": "78014-37797-24-43",
      "start_date": "2024-10-25T00:15:00Z",
      "home_competitors": [
        {
          "id": "13AD4FDBEBA8",
          "name": "Los Angeles Rams",
          "abbreviation": "LAR",
          "logo": "https://cdn.opticodds.com/team-logos/football/99.png"
        }
      ],
      "away_competitors": [
        {
          "id": "24E4EA618C5E",
          "name": "Minnesota Vikings",
          "abbreviation": "MIN",
          "logo": "https://cdn.opticodds.com/team-logos/football/101.png"
        }
      ],
      "home_team_display": "Los Angeles Rams",
      "away_team_display": "Minnesota Vikings",
      "status": "unplayed",
      "is_live": false,
      "sport": {
        "id": "football",
        "name": "Football"
      },
      "league": {
        "id": "nfl",
        "name": "NFL"
      },
      "tournament": null,
      "odds": [
        {
          "id": "1:-1:032B6289DB25:point_spread:los_angeles_rams_+2_5",
          "version_id": -1,
          "version": "default",
          "odd_id": "032B6289DB25:point_spread:los_angeles_rams_+2_5",
          "market": "Point Spread",
          "name": "Los Angeles Rams +2.5",
          "is_main": true,
          "selection": "Los Angeles Rams",
          "normalized_selection": "los_angeles_rams",
          "market_id": "point_spread",
          "price": -101,
          "timestamp": 1729714816.49106,
          "grouping_key": "default:2.5",
          "points": 2.5,
          "selection_line": null,
          "player_id": null,
          "team_id": "13AD4FDBEBA8"
        },
        {
          "id": "1:-1:032B6289DB25:point_spread:minnesota_vikings_-2_5",
          "version_id": -1,
          "version": "default",
          "odd_id": "032B6289DB25:point_spread:minnesota_vikings_-2_5",
          "market": "Point Spread",
          "name": "Minnesota Vikings -2.5",
          "is_main": true,
          "selection": "Minnesota Vikings",
          "normalized_selection": "minnesota_vikings",
          "market_id": "point_spread",
          "price": -118,
          "timestamp": 1729714816.49106,
          "grouping_key": "default:2.5",
          "points": -2.5,
          "selection_line": null,
          "player_id": null,
          "team_id": "24E4EA618C5E"
        }
      ]
    }
  ]
}
```

## Usage Notes

- The endpoint supports querying odds for multiple fixtures, teams, or players simultaneously (up to 5 of each type per request)
- Odds are returned in real-time and include timestamp information for tracking when they were last updated
- The `is_main` parameter is useful for filtering to only the primary betting lines for each market
- Point spread values are positive for underdogs and negative for favorites
- The `grouping_key` field helps identify related betting options that should be displayed together
- Logo URLs are provided for team branding in client applications
- All datetime values are in UTC timezone using ISO 8601 format
- Price values in American format use negative numbers for favorites and positive for underdogs