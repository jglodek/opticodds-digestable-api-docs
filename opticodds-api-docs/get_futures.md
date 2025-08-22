# OpticOdds API - Futures Endpoint

## Endpoint Information

**Base URL:** `https://api.opticodds.com/api/v3/futures`

**HTTP Method:** GET

**Description:** Returns a comprehensive list of all the futures betting markets that are currently supported or have been previously supported by OpticOdds. This endpoint provides detailed information about various future betting opportunities across different sports, leagues, and bet types including championship winners, individual player awards, statistical leaders, and season-long outcomes.

## Request Parameters

The endpoint accepts query parameters to filter the futures results. Based on the example provided:

- **league** (string, optional): Filter futures by specific league identifier (e.g., "NBA")

*Note: For a complete list of all available parameters, please refer to the full parameter documentation at the bottom of the API documentation page.*

## Response Format

The API returns data in JSON format with the following structure:

### Root Response Object

```json
{
  "data": [
    // Array of future objects
  ]
}
```

### Future Object Structure

Each future object in the data array contains the following comprehensive properties:

#### Core Properties

- **id** (string): Unique identifier for the future bet, following the format `type_{future_type}-sport_{sport_id}-league_{league_id}`
  - Example: `"type_championship_winner-sport_basketball-league_nba"`

- **name** (string): Human-readable display name of the future bet
  - Example: `"Championship Winner"`

- **future_type** (string|null): Categorization of the future bet type with the following possible values:
  - `"TEAM"`: Team-based futures (championships, division winners, playoffs)
  - `"PLAYER"`: Individual player awards and statistical achievements
  - `"UNKNOWN"`: Miscellaneous or uncategorized future types
  - `null`: When the future type is not specified or applicable

- **start_date** (string): ISO 8601 formatted timestamp indicating when the future bet becomes active or when the underlying event begins
  - Format: `"YYYY-MM-DDTHH:mm:ss.sssZ"`
  - Example: `"2025-04-13T22:00:00Z"`

#### Sport Information Object

- **sport** (object): Contains sport-specific information
  - **id** (string): Unique identifier for the sport (e.g., `"basketball"`)
  - **name** (string): Display name of the sport (e.g., `"basketball"`)

#### League Information Object

- **league** (object): Contains league-specific information
  - **id** (string): Unique identifier for the league (e.g., `"nba"`)
  - **name** (string): Display name of the league (e.g., `"NBA"`)

#### Tournament Information

- **tournament** (null): Currently returns null for all futures in the provided example, but may contain tournament-specific information for tournament-based futures

## Example Request

```
GET https://api.opticodds.com/api/v3/futures?league=NBA
```

## Example Response

The response includes a comprehensive array of NBA futures covering various categories:

### Championship and Conference Futures
- Championship Winner
- Eastern Conference Winner
- Western Conference Winner
- Championship Winner Conference
- Championship Winner Division

### Division Winners
- Atlantic Division Winner
- Central Division Winner
- Northwest Division Winner
- Pacific Division Winner
- Southeast Division Winner
- Southwest Division Winner

### Player Awards and Statistical Leaders
- MVP Winner
- Rookie Of The Year
- 6th Man Of The Year
- Defensive Player Of The Year Winner
- Most Improved Player
- Clutch Player Of The Year Winner
- NBA Finals MVP
- Coach Of The Year Winner

### Statistical Performance Leaders
- Points Per Game Leader
- Assists Per Game Leader
- Rebounds Per Game Leader
- Steals Per Game Leader
- Blocks Per Game Leader
- Made Threes Per Game Leader

### Season and Playoff Outcomes
- To Make The Playoffs
- To Make The East Play-In 2024
- To Make The West Play-In 2024
- Regular Season Wins

### Special Tournament Futures (NBA Cup 2024)
- NBA Cup Winner 2024
- NBA Cup MVP 2024
- NBA Cup East Group A Winner 2024
- NBA Cup East Group B Winner 2024
- NBA Cup East Group C Winner 2024
- NBA Cup West Group A Winner 2024
- NBA Cup West Group B Winner 2024
- NBA Cup West Group C Winner 2024

## Sample Future Objects

### Team-Based Future Example
```json
{
  "id": "type_championship_winner-sport_basketball-league_nba",
  "sport": {
    "id": "basketball",
    "name": "basketball"
  },
  "league": {
    "id": "nba",
    "name": "NBA"
  },
  "tournament": null,
  "name": "Championship Winner",
  "future_type": "TEAM",
  "start_date": "2025-04-13T22:00:00Z"
}
```

### Player-Based Future Example
```json
{
  "id": "type_mvp_winner-sport_basketball-league_nba",
  "sport": {
    "id": "basketball",
    "name": "basketball"
  },
  "league": {
    "id": "nba",
    "name": "NBA"
  },
  "tournament": null,
  "name": "MVP Winner",
  "future_type": "PLAYER",
  "start_date": "2024-11-19T19:16:12.832Z"
}
```

### Unknown Type Future Example
```json
{
  "id": "type_championship_winner_conference-sport_basketball-league_nba",
  "sport": {
    "id": "basketball",
    "name": "basketball"
  },
  "league": {
    "id": "nba",
    "name": "NBA"
  },
  "tournament": null,
  "name": "Championship Winner Conference",
  "future_type": "UNKNOWN",
  "start_date": "2024-11-19T18:40:21.519Z"
}
```

## Technical Implementation Notes

### Date Format Specifications
- All timestamps are provided in ISO 8601 format with UTC timezone designation
- Start dates may include millisecond precision (e.g., `"2024-11-19T18:40:55.095Z"`)
- Start dates indicate when the future bet becomes active or when the underlying season/event commences

### Future Type Classifications
The `future_type` field serves as a primary categorization mechanism:
- **TEAM futures** typically involve team-based outcomes like championships, division titles, playoff qualification
- **PLAYER futures** focus on individual achievements, awards, and statistical leadership
- **UNKNOWN futures** may represent complex betting markets that don't fit standard team/player classifications
- **null values** indicate futures where type classification is not applicable or not yet determined

### Identifier Structure
The `id` field follows a consistent naming convention that encodes multiple pieces of information:
- Prefix: `type_` followed by the specific future type description
- Sport identifier: `-sport_` followed by the sport ID
- League identifier: `-league_` followed by the league ID

This structured approach enables programmatic parsing and categorization of futures data.