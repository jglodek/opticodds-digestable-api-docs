# Player Results - Last X Games API

## Overview

**Endpoint:** `/api/v3/fixtures/player-results/last-x`

**Base URL:** `https://api.opticodds.com`

**Method:** GET

**Description:** Returns a comprehensive list of player performance results for a specified player across their last X number of games played. This endpoint provides detailed statistical breakdowns for individual player performance over a configurable range of recent games.

## Endpoint Details

### Full URL Structure
```
https://api.opticodds.com/api/v3/fixtures/player-results/last-x
```

### HTTP Method
```
GET
```

## Parameters

### Required Parameters

#### `player_id`
- **Type:** String
- **Description:** Unique identifier for the specific player whose results you want to retrieve
- **Format:** Alphanumeric string identifier
- **Example:** `370FCD1B2322`

### Date/Season Parameters (Mutually Exclusive)

**Important Note:** You can use either `earliest_date` OR `season_year` parameters, but not both simultaneously. These parameters are mutually exclusive and cannot be combined in a single API request.

#### `earliest_date`
- **Type:** String (Date)
- **Description:** Specifies the earliest date from which to retrieve player results. This parameter allows you to filter results starting from a specific date and moving forward chronologically.
- **Format:** `YYYY-MM-DD` (ISO 8601 date format)
- **Example:** `2024-03-15`
- **Additional Information:** More detailed functionality information can be found in the API changelog documentation

#### `season_year`
- **Type:** Integer
- **Description:** Specifies the particular season year for which to retrieve player results. This parameter filters results to only include games from the specified season.
- **Format:** 4-digit year
- **Example:** `2024`

### Optional Parameters
For a comprehensive list of all available optional parameters and their detailed specifications, refer to the complete parameter documentation at the bottom of the API documentation page.

## Example Request

### Baseball Example
```
GET https://api.opticodds.com/api/v3/fixtures/player-results/last-x?player_id=370FCD1B2322&season_year=2024
```

## Response Format

The API returns a JSON response with the following structure:

### Response Schema

```json
{
  "data": [
    {
      "sport": {
        "id": "string",
        "name": "string"
      },
      "league": {
        "id": "string",
        "name": "string"
      },
      "player": {
        "id": "string",
        "name": "string",
        "position": "string",
        "number": integer
      },
      "team": {
        "id": "string",
        "name": "string"
      },
      "stats": {
        // Statistical data arrays
      }
    }
  ]
}
```

### Response Fields Breakdown

#### `data` (Array)
The main data container that holds an array of player result objects.

#### `sport` (Object)
Contains sport identification information:
- **`id`** (String): Unique identifier for the sport (e.g., "baseball")
- **`name`** (String): Human-readable name of the sport (e.g., "Baseball")

#### `league` (Object)
Contains league identification information:
- **`id`** (String): Unique identifier for the league (e.g., "mlb")
- **`name`** (String): Human-readable name of the league (e.g., "MLB")

#### `player` (Object)
Contains comprehensive player identification and basic information:
- **`id`** (String): Unique player identifier matching the requested player_id
- **`name`** (String): Full name of the player
- **`position`** (String): Player's primary position (e.g., "SS" for shortstop)
- **`number`** (Integer): Player's jersey number

#### `team` (Object)
Contains team identification information:
- **`id`** (String): Unique team identifier
- **`name`** (String): Full team name

#### `stats` (Object)
Contains detailed statistical performance data. Each statistic is represented as an array where each element corresponds to the player's performance in a specific game, ordered chronologically. The statistical categories include:

##### Offensive Statistics
- **`rbi`** (Array of Integers): Runs Batted In per game
- **`hits`** (Array of Integers): Total hits per game
- **`runs`** (Array of Integers): Runs scored per game
- **`at_bats`** (Array of Integers): Official at-bats per game
- **`doubles`** (Array of Integers): Two-base hits per game
- **`triples`** (Array of Integers): Three-base hits per game
- **`home_runs`** (Array of Integers): Home runs hit per game
- **`total_bases`** (Array of Integers): Total bases achieved per game
- **`stolen_bases`** (Array of Integers): Successfully stolen bases per game
- **`caught_stealing`** (Array of Integers): Times caught stealing per game

##### Batting Discipline Statistics
- **`batting_walks`** (Array of Integers): Walks (bases on balls) per game
- **`batting_strikeouts`** (Array of Integers): Strikeouts while batting per game
- **`batting_hit_by_pitch`** (Array of Integers): Times hit by pitch per game
- **`batting_intentional_walks`** (Array of Integers): Intentional walks per game

##### Plate Appearance Statistics
- **`batting_plate_appearances`** (Array of Integers): Total plate appearances per game
- **`batting_sacrifice_hits`** (Array of Integers): Sacrifice bunts per game
- **`batting_sacrifice_flies`** (Array of Integers): Sacrifice flies per game

##### Batting Contact Statistics
- **`batting_flyballs`** (Array of Integers): Fly balls hit per game
- **`batting_groundballs`** (Array of Integers): Ground balls hit per game
- **`batting_ground_into_double_play`** (Array of Integers): Times grounded into double play per game

##### Game Participation
- **`starter`** (Array of Integers): Binary indicator (1/0) showing if player started the game
- **`batting_picked_off`** (Array of Integers): Times picked off base per game

## Example Response

### Baseball Player Results Example

```json
{
  "data": [
    {
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      },
      "player": {
        "id": "370FCD1B2322",
        "name": "Miguel Rojas",
        "position": "SS",
        "number": 11
      },
      "team": {
        "id": "8E80F9DD4C5E",
        "name": "Los Angeles Dodgers"
      },
      "stats": {
        "rbi": [1, 2, 0, 0, 1],
        "hits": [1, 2, 1, 0, 3],
        "runs": [0, 3, 0, 0, 0],
        "at_bats": [3, 4, 3, 3, 4],
        "doubles": [0, 0, 0, 0, 0],
        "starter": [1, 1, 1, 1, 1],
        "triples": [0, 0, 0, 0, 0],
        "home_runs": [0, 1, 0, 0, 0],
        "total_bases": [1, 5, 1, 0, 3],
        "stolen_bases": [0, 0, 0, 0, 0],
        "batting_walks": [0, 0, 0, 0, 0],
        "caught_stealing": [0, 0, 0, 0, 0],
        "batting_flyballs": [0, 0, 1, 3, 0],
        "batting_picked_off": [0, 0, 0, 0, 0],
        "batting_strikeouts": [0, 1, 0, 0, 0],
        "batting_groundballs": [1, 2, 1, 0, 3],
        "batting_hit_by_pitch": [0, 0, 0, 0, 0],
        "batting_sacrifice_hits": [0, 0, 1, 0, 0],
        "batting_sacrifice_flies": [1, 0, 0, 0, 0],
        "batting_intentional_walks": [0, 0, 0, 0, 0],
        "batting_plate_appearances": [4, 4, 4, 3, 4],
        "batting_ground_into_double_play": [0, 0, 0, 0, 1]
      }
    }
  ]
}
```

### Response Data Interpretation

In the example above, the statistical arrays represent Miguel Rojas's performance across his last 5 games:
- **Game 1:** 1 RBI, 1 hit, 0 runs, 3 at-bats, started the game
- **Game 2:** 2 RBIs, 2 hits, 3 runs, 4 at-bats, 1 home run, started the game
- **Game 3:** 0 RBIs, 1 hit, 0 runs, 3 at-bats, started the game
- **Game 4:** 0 RBIs, 0 hits, 0 runs, 3 at-bats, started the game
- **Game 5:** 1 RBI, 3 hits, 0 runs, 4 at-bats, started the game

Each index position in the statistical arrays corresponds to the same chronological game, allowing for comprehensive analysis of player performance trends across multiple games.

## Important Usage Notes

1. **Parameter Exclusivity:** Remember that `earliest_date` and `season_year` parameters cannot be used together in the same request.

2. **Data Chronology:** Statistical arrays are ordered chronologically, with each array index representing the same game across all statistical categories.

3. **Game Participation:** The `starter` field uses binary values (1 for started, 0 for did not start) to indicate whether the player was in the starting lineup.

4. **Complete Parameter List:** For access to the full comprehensive list of available parameters and their detailed specifications, consult the complete parameter documentation referenced at the bottom of the main API documentation page.