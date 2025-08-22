# API Documentation: Fixture Player Results

## Endpoint Overview

This API endpoint returns comprehensive fixture player results, including all available player statistics for a specific game. For some leagues, this endpoint provides real-time live player results as the game progresses. 

**Important Note:** If a player does not appear in the results, it is safe to assume they did not play any minutes in the game.

## HTTP Request

**URL:** `https://api.opticodds.com/api/v3/fixtures/player-results`

**Method:** GET

**Query Parameters:**
- `fixture_id` (required): The unique identifier for the fixture/game

## Example Request

```
GET https://api.opticodds.com/api/v3/fixtures/player-results?fixture_id=24E371425A5F
```

## Response Structure

The API returns a JSON response with the following comprehensive structure:

### Root Level
- `data` (array): Contains fixture player results data

### Data Object Structure

#### Sport Information
- `sport` (object): Sport identification details
  - `id` (string): Sport identifier (e.g., "baseball")
  - `name` (string): Human-readable sport name (e.g., "Baseball")

#### League Information
- `league` (object): League identification details
  - `id` (string): League identifier (e.g., "mlb")
  - `name` (string): Human-readable league name (e.g., "MLB")

#### Fixture Information
- `fixture` (object): Complete fixture/game details
  - `id` (string): Unique fixture identifier
  - `game_id` (string): Alternative game identifier in format "team1-team2-date-sequence"
  - `start_date` (string): Game start time in ISO 8601 format (UTC)
  - `home_competitors` (array): Home team information
    - `id` (string): Team unique identifier
    - `name` (string): Full team name
    - `abbreviation` (string): Team abbreviation
    - `logo` (string): URL to team logo image
  - `away_competitors` (array): Away team information (same structure as home_competitors)
  - `home_team_display` (string): Display name for home team
  - `away_team_display` (string): Display name for away team
  - `status` (string): Current game status (e.g., "live", "completed", "scheduled")
  - `is_live` (boolean): Indicates if the game is currently in progress

#### Player Results
- `results` (array): Array of player performance data

##### Individual Player Result Structure
- `player` (object): Player identification information
  - `id` (string): Unique player identifier
  - `name` (string): Player's full name
  - `position` (string): Player's position (e.g., "SS", "RP", "LF", "C", "1B", etc.)
  - `number` (integer): Player's jersey number

- `team` (object): Team association
  - `id` (string): Team unique identifier
  - `name` (string): Full team name

- `status` (string): Player's current status in the game (e.g., "live")

- `stats` (array): Statistical performance data
  - `period` (string): Time period for statistics (typically "all" for complete game stats)
  - `stats` (object): Comprehensive statistical breakdown

##### Baseball Statistics Structure

The statistics object contains extensive baseball performance metrics:

**Batting Statistics:**
- `rbi` (integer): Runs Batted In
- `hits` (integer): Total hits
- `runs` (integer): Runs scored
- `at_bats` (integer): Official at-bats
- `doubles` (integer): Double hits
- `triples` (integer): Triple hits
- `home_runs` (integer): Home runs
- `total_bases` (integer): Total bases achieved
- `stolen_bases` (integer): Successful stolen bases
- `batting_walks` (integer): Base on balls (walks)
- `caught_stealing` (integer): Times caught stealing
- `batting_picked_off` (integer): Times picked off base
- `batting_strikeouts` (integer): Strikeouts as batter
- `batting_hit_by_pitch` (integer): Times hit by pitch
- `batting_sacrifice_hits` (integer): Sacrifice hits (bunts)
- `batting_sacrifice_flies` (integer): Sacrifice flies
- `batting_intentional_walks` (integer): Intentional walks received
- `batting_plate_appearances` (integer): Total plate appearances
- `batting_ground_into_double_play` (integer): Grounded into double plays
- `starter` (integer): Indicates if player was in starting lineup (1 = starter, 0 = substitute)

**Pitching Statistics:**
- `strikeouts` (integer): Batters struck out
- `earned_runs` (integer): Earned runs allowed
- `pitch_count` (integer): Total pitches thrown
- `hits_allowed` (integer): Hits allowed
- `runs_allowed` (integer): Total runs allowed
- `save_pitcher` (integer): Save credited (1 = yes, 0 = no)
- `batters_faced` (integer): Total batters faced
- `complete_game` (integer): Complete game pitched (1 = yes, 0 = no)
- `losing_pitcher` (integer): Loss credited (1 = yes, 0 = no)
- `winning_pitcher` (integer): Win credited (1 = yes, 0 = no)
- `pitching_balks` (integer): Balks committed
- `pitching_balls` (integer): Ball pitches thrown
- `pitching_walks` (integer): Walks issued
- `doubles_allowed` (integer): Double hits allowed
- `triples_allowed` (integer): Triple hits allowed
- `home_runs_allowed` (integer): Home runs allowed
- `holding_pitcher` (integer): Hold credited (1 = yes, 0 = no)
- `innings_pitched` (number): Innings pitched (can include fractional innings like 1.1, 2.2)
- `opponent_at_bats` (integer): Opponent official at-bats
- `pitching_shutout` (integer): Shutout pitched (1 = yes, 0 = no)
- `pitching_strikes` (integer): Strike pitches thrown
- `pitching_pickoffs` (integer): Successful pickoffs
- `blown_save_pitcher` (integer): Blown save (1 = yes, 0 = no)
- `pitching_no_hitter` (integer): No-hitter pitched (1 = yes, 0 = no)
- `pitching_hit_batsmen` (integer): Batters hit by pitch
- `stolen_bases_allowed` (integer): Stolen bases allowed
- `pitching_perfect_game` (integer): Perfect game pitched (1 = yes, 0 = no)
- `pitching_wild_pitches` (integer): Wild pitches thrown
- `sacrifice_hits_allowed` (integer): Sacrifice hits allowed
- `sacrifice_flies_allowed` (integer): Sacrifice flies allowed
- `batting_flyballs_allowed` (integer): Fly balls allowed
- `pitching_intentional_walks` (integer): Intentional walks issued
- `batting_groundballs_allowed` (integer): Ground balls allowed
- `ground_into_double_play_allowed` (integer): Ground ball double plays allowed

## Example Response

### Baseball Game Example

The following example shows a comprehensive response for a live MLB game between the Pittsburgh Pirates and Chicago Cubs:

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
      "fixture": {
        "id": "24E371425A5F",
        "game_id": "40548-36707-2024-08-28-09",
        "start_date": "2024-08-28T16:35:00Z",
        "home_competitors": [
          {
            "id": "98CE61698342",
            "name": "Pittsburgh Pirates",
            "abbreviation": "PIT",
            "logo": "https://a.espncdn.com/i/teamlogos/mlb/500/pit.png"
          }
        ],
        "away_competitors": [
          {
            "id": "5045D954DFF8",
            "name": "Chicago Cubs",
            "abbreviation": "CHC",
            "logo": "https://a.espncdn.com/i/teamlogos/mlb/500/chc.png"
          }
        ],
        "home_team_display": "Pittsburgh Pirates",
        "away_team_display": "Chicago Cubs",
        "status": "live",
        "is_live": true
      },
      "results": [
        {
          "player": {
            "id": "2E6E5540E308",
            "name": "Alika Williams",
            "position": "SS",
            "number": 25
          },
          "team": {
            "id": "98CE61698342",
            "name": "Pittsburgh Pirates"
          },
          "status": "live",
          "stats": [
            {
              "period": "all",
              "stats": {
                "rbi": 1,
                "hits": 1,
                "runs": 0,
                "at_bats": 4,
                "doubles": 0,
                "starter": 1,
                "triples": 0,
                "home_runs": 0,
                "total_bases": 1,
                "stolen_bases": 0,
                "batting_walks": 0,
                "caught_stealing": 0,
                "batting_picked_off": 0,
                "batting_strikeouts": 2,
                "batting_hit_by_pitch": 0,
                "batting_sacrifice_hits": 1,
                "batting_sacrifice_flies": 0,
                "batting_intentional_walks": 0,
                "batting_plate_appearances": 5,
                "batting_ground_into_double_play": 0
              }
            }
          ]
        },
        {
          "player": {
            "id": "B528EEE48AF1",
            "name": "Aroldis Chapman",
            "position": "RP",
            "number": 45
          },
          "team": {
            "id": "98CE61698342",
            "name": "Pittsburgh Pirates"
          },
          "status": "live",
          "stats": [
            {
              "period": "all",
              "stats": {
                "starter": 0,
                "strikeouts": 1,
                "earned_runs": 3,
                "pitch_count": 27,
                "hits_allowed": 3,
                "runs_allowed": 3,
                "save_pitcher": 0,
                "batters_faced": 7,
                "complete_game": 0,
                "losing_pitcher": 0,
                "pitching_balks": 0,
                "pitching_balls": 8,
                "pitching_walks": 1,
                "doubles_allowed": 1,
                "holding_pitcher": 0,
                "innings_pitched": 1,
                "triples_allowed": 0,
                "winning_pitcher": 0,
                "opponent_at_bats": 6,
                "pitching_shutout": 0,
                "pitching_strikes": 19,
                "home_runs_allowed": 0,
                "pitching_pickoffs": 0,
                "blown_save_pitcher": 0,
                "pitching_no_hitter": 0,
                "pitching_hit_batsmen": 0,
                "stolen_bases_allowed": 1,
                "pitching_perfect_game": 0,
                "pitching_wild_pitches": 0,
                "sacrifice_hits_allowed": 0,
                "sacrifice_flies_allowed": 0,
                "batting_flyballs_allowed": 1,
                "pitching_intentional_walks": 0,
                "batting_groundballs_allowed": 3,
                "ground_into_double_play_allowed": 0
              }
            }
          ]
        }
      ]
    }
  ]
}
```

## Key Features and Capabilities

### Real-Time Data
- Provides live player statistics during ongoing games
- Updates player performance metrics in real-time
- Includes current game status and live indicators

### Comprehensive Statistics
- Complete batting performance metrics for position players
- Detailed pitching statistics for all pitchers used in the game
- Historical and cumulative statistics for the entire game period

### Player Information
- Complete player identification with names, positions, and jersey numbers
- Team association and affiliation details
- Starter vs. substitute designation

### Flexible Data Structure
- Supports multiple sports and leagues through consistent API structure
- Extensible statistics framework for different sport types
- Consistent response format across all supported competitions

### Data Reliability
- Clear indication when players did not participate (absence from results)
- Accurate real-time updates for live games
- Comprehensive historical data for completed games

This endpoint serves as a comprehensive source for detailed player-level performance data, making it ideal for fantasy sports applications, statistical analysis, live game tracking, and sports data visualization platforms.