# API Documentation: Fixtures Results

## Overview

This API endpoint provides comprehensive fixture results data, including real-time scores, team statistics, and live game state information such as balls, strikes, and outs count. The endpoint delivers detailed information about sports fixtures across various leagues and competitions.

## Endpoint Details

**Base URL:** `https://api.opticodds.com/api/v3/fixtures/results`

**HTTP Method:** GET

**Content Type:** application/json

## Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `fixture_id` | string | Yes | Unique identifier for the specific fixture/game for which results are requested |

## Response Structure

The API returns a JSON response with the following comprehensive structure:

### Root Response Object

```json
{
  "data": [
    // Array of fixture result objects
  ]
}
```

### Fixture Result Object

Each fixture result object contains the following detailed information:

#### Sport Information
- **sport**: Object containing sport identification details
  - **id**: String - Unique identifier for the sport (e.g., "baseball")
  - **name**: String - Human-readable name of the sport (e.g., "Baseball")

#### League Information
- **league**: Object containing league identification details
  - **id**: String - Unique identifier for the league (e.g., "mlb")
  - **name**: String - Human-readable name of the league (e.g., "MLB")

#### Fixture Details
- **fixture**: Comprehensive object containing all fixture-related information
  - **id**: String - Unique fixture identifier (e.g., "439A1AC1DBDB")
  - **game_id**: String - Alternative game identifier with detailed format (e.g., "40644-60486-2024-10-01-11")
  - **start_date**: String - ISO 8601 formatted datetime of fixture start (e.g., "2024-10-01T18:32:00Z")
  - **home_competitors**: Array of objects representing home team(s)
    - **id**: String - Unique team identifier
    - **name**: String - Full team name
    - **abbreviation**: String - Team abbreviation code
    - **logo**: String - URL to team logo image
  - **away_competitors**: Array of objects representing away team(s)
    - **id**: String - Unique team identifier
    - **name**: String - Full team name
    - **abbreviation**: String - Team abbreviation code
    - **logo**: String - URL to team logo image
  - **home_team_display**: String - Display name for home team
  - **away_team_display**: String - Display name for away team
  - **status**: String - Current fixture status (e.g., "live", "completed", "scheduled")
  - **is_live**: Boolean - Indicates whether the fixture is currently in progress

#### Scoring Information
- **scores**: Detailed scoring breakdown for both teams
  - **home**: Home team scoring details
    - **total**: Integer - Current total score for home team
    - **periods**: Object containing period-by-period scoring breakdown
      - **period_1** through **period_n**: Integer values for each period/inning
    - **aggregate**: Nullable field for aggregate scoring information
  - **away**: Away team scoring details
    - **total**: Integer - Current total score for away team
    - **periods**: Object containing period-by-period scoring breakdown
      - **period_1** through **period_n**: Integer values for each period/inning
    - **aggregate**: Nullable field for aggregate scoring information

#### Live Game State Information
- **in_play**: Real-time game state data (when fixture is live)
  - **period**: String - Current period/inning number
  - **clock**: String - Current position in period (e.g., "Top", "Bottom")
  - **last_play**: Nullable string - Description of most recent play
  - **time_min**: Nullable integer - Minutes remaining (sport-dependent)
  - **time_sec**: Nullable integer - Seconds remaining (sport-dependent)
  - **balls**: Integer - Current ball count (baseball-specific)
  - **outs**: Integer - Current out count (baseball-specific)
  - **strikes**: Integer - Current strike count (baseball-specific)
  - **runners**: Object containing base runner information (baseball-specific)
    - **first**: Nullable object - Player on first base
    - **second**: Nullable object - Player on second base
    - **third**: Nullable object - Player on third base
    - Each runner object contains:
      - **player_id**: String - Unique player identifier
      - **player_name**: String - Player's full name
      - **team_id**: String - Player's team identifier
  - **batter**: Object containing current batter information
    - **player_id**: String - Unique player identifier
    - **player_name**: String - Player's full name
    - **team_id**: String - Player's team identifier
  - **pitcher**: Nullable object - Current pitcher information
  - **possession**: Nullable field - Team possession information (sport-dependent)
  - **down**: Nullable field - Down count (American football specific)
  - **distance_to_go**: Nullable field - Yards to go (American football specific)
  - **field_position**: Nullable field - Field position information (sport-dependent)

#### Game Events
- **events**: Array of game event objects (currently empty in example but structured for event data)

#### Team Statistics
- **stats**: Comprehensive statistical breakdown for both teams
  - **home**: Array of statistical periods for home team
    - **period**: String - Statistical period identifier (e.g., "all" for complete game)
    - **stats**: Object containing detailed statistical metrics
      - **rbi**: Integer - Runs batted in (baseball)
      - **hits**: Integer - Total hits
      - **runs**: Integer - Total runs scored
      - **at_bats**: Integer - Total at-bats
      - **total_bases**: Integer - Total bases achieved
      - **double_plays**: Integer - Double plays completed
      - **triple_plays**: Integer - Triple plays completed
      - **batting_walks**: Integer - Walks received while batting
      - **batting_strikeouts**: Integer - Strikeouts while batting
      - **runners_left_on_base**: Integer - Runners left stranded on bases
      - **scoring_position_successes**: Integer - Successful hits with runners in scoring position
      - **scoring_position_opportunities**: Integer - Total opportunities with runners in scoring position
  - **away**: Array of statistical periods for away team (same structure as home team)

#### Additional Information
- **extra**: Object containing supplementary fixture information
  - **decision**: Nullable field - Game decision information
  - **decision_method**: Nullable field - Method by which game decision was reached

- **retirement_info**: Nullable field - Information about any player or team retirements affecting the fixture

## Example Request

```
GET https://api.opticodds.com/api/v3/fixtures/results?fixture_id=439A1AC1DBDB
```

## Example Response

The API returns a comprehensive JSON response containing all the detailed information outlined above. The example shows a live baseball game between the Houston Astros (home) and Detroit Tigers (away), with the Tigers leading 3-0 in the top of the 7th inning. The response includes complete scoring breakdowns by inning, current game state with ball/strike/out counts, base runner positions, current batter information, and comprehensive team statistics including hits, runs, RBIs, and various other baseball-specific metrics.

## Response Format

- **Content-Type**: application/json
- **Character Encoding**: UTF-8
- **Date Format**: ISO 8601 (YYYY-MM-DDTHH:MM:SSZ)

## Use Cases

This endpoint is particularly useful for:
- Live sports tracking applications
- Sports betting platforms requiring real-time game state
- Fantasy sports platforms needing current player and team performance data
- Sports news and media applications
- Statistical analysis and reporting systems
- Mobile applications providing live sports updates

The comprehensive nature of the response makes it suitable for applications requiring detailed, real-time sports data with both current game state and historical statistical context.