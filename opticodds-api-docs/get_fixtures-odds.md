# OpticOdds API v3 - Fixtures Odds Endpoint

## Overview

This endpoint provides access to odds and limits data for a comprehensive combination of sportsbooks, fixtures, and markets. The API specifically targets game odds that are directly related to individual events and does not encompass odds for entire tournaments or complete seasons.

**Important Note on Data Availability**: The API exclusively returns odds that are currently available in the market. If a particular odd is not included in the response, it should be considered suspended for all practical purposes.

## API Endpoint Details

### Base URL
```
GET /api/v3/fixtures/odds
```

### Full Example URL
```
https://api.opticodds.com/api/v3/fixtures/odds?&sportsbook=Pinnacle&fixture_id=BCE4E01B8D3D
```

## Required Parameter Constraints

### Mandatory Parameter Requirements
The API enforces strict parameter validation requirements that must be satisfied for successful requests:

**Primary Entity Selection** (At least one required):
- `fixture_id` - Specific fixture identifier
- `team_id` - Team-based identifier  
- `player_id` - Individual player identifier

**Sportsbook Selection** (Required):
- Must specify at least **1** sportsbook
- Maximum limit of **5** sportsbooks per request

## Detailed Parameter Specifications

### `fixture_id` Parameter
- **Type**: String identifier
- **Limit**: Maximum of 5 fixture IDs can be passed per individual request
- **Purpose**: Targets specific game/match events for odds retrieval

### `sportsbook` Parameter
- **Type**: String (accepts both ID and name formats)
- **Limit**: 1-5 sportsbooks per request (inclusive range)
- **Purpose**: Specifies which sportsbooks to retrieve odds from
- **Input Format**: Accepts either the sportsbook's unique identifier or the sportsbook's display name

### `market` Parameter
- **Type**: String (accepts both ID and name formats)
- **Purpose**: Filters odds by specific betting markets
- **Input Format**: Accepts either the market's unique identifier or the market's display name
- **Flexibility**: Multiple markets can be specified to narrow down results

### `is_main` Parameter
- **Type**: Boolean
- **Purpose**: Indicates whether a betting line represents the "main" or "given" line for a specific market
- **Functionality**: Distinguishes primary lines from alternative lines
- **Example Context**: In a football game, the +/- 6 Point Spread and Over/Under 46.5 Total Points would be considered "main" lines, while alternative spreads or totals would not have this designation

### `odds_format` Parameter
- **Type**: String (enumerated values)
- **Default Value**: `AMERICAN`
- **Accepted Values**:
  - `AMERICAN` - Standard American format (e.g., +150, -110)
  - `DECIMAL` - European decimal format (e.g., 1.91, 2.50)
  - `PROBABILITY` - Percentage probability format
  - `MALAY` - Malaysian odds format
  - `HONG_KONG` - Hong Kong odds format  
  - `INDONESIAN` - Indonesian odds format

## Deep Link Integration

### Permission-Based Feature
Access to deep link information is controlled through API key permissions. Users with appropriate permissions will see additional deep link data in their responses.

### Deep Link Structure
When deep link permissions are enabled and data is available, each odd object will contain a `deep_link` field with platform-specific URLs:

```json
{
  "deep_link": {
    "ios": "https://sportsbook.caesars.com/addToBetslip?marketId=42.441564663&selectionId=29170",
    "android": "caesarssportsbook://account.sportsbook.caesars.com/sportsbook/addToBetslip?marketId=42.441564663&selectionId=29170",
    "desktop": "https://sportsbook.caesars.com/addToBetslip?marketId=42.441564663&selectionId=29170"
  }
}
```

### Deep Link Availability
- **Available**: When permissions are enabled and sportsbook provides deep link data
- **Unavailable**: Returns `null` when data is not available or permissions are not granted

## Response Structure and Data Schema

### Root Response Object
```json
{
  "data": [
    // Array of fixture objects with comprehensive odds data
  ]
}
```

### Fixture Object Structure
Each fixture in the response contains the following comprehensive data structure:

#### Core Fixture Information
- **`id`**: Unique fixture identifier (String)
- **`game_id`**: Game-specific identifier with format pattern (String)
- **`start_date`**: ISO 8601 formatted start date/time (String)
- **`status`**: Current status of the fixture (e.g., "unplayed", "live", "finished")
- **`is_live`**: Boolean indicator for live/in-progress games

#### Team/Competitor Information
- **`home_competitors`**: Array containing home team details
- **`away_competitors`**: Array containing away team details
- **`home_team_display`**: Formatted home team name for display
- **`away_team_display`**: Formatted away team name for display

#### Competitor Object Structure
```json
{
  "id": "4F11A5896C24",
  "name": "Houston Astros", 
  "abbreviation": "HOU",
  "logo": "https://a.espncdn.com/i/teamlogos/mlb/500/hou.png"
}
```

#### Sports Classification
- **`sport`**: Object containing sport ID and name
- **`league`**: Object containing league ID and name  
- **`tournament`**: Tournament information (null if not applicable)

#### Odds Array Structure
The `odds` array contains detailed betting information for each available market and selection:

##### Individual Odds Object Properties
- **`id`**: Unique identifier for the specific odds entry
- **`sportsbook`**: Name of the sportsbook providing the odds
- **`market`**: Market type (e.g., "Moneyline", "Run Line", "Total Runs")
- **`name`**: Human-readable name for the betting option
- **`is_main`**: Boolean indicating if this is the main line for the market
- **`selection`**: The specific selection being bet on
- **`normalized_selection`**: Standardized version of the selection name
- **`market_id`**: Standardized market identifier
- **`selection_line`**: Line type for over/under bets (e.g., "over", "under")
- **`player_id`**: Player identifier (null if not player-specific)
- **`team_id`**: Team identifier (null if not team-specific)
- **`price`**: The odds value in the specified format
- **`timestamp`**: Unix timestamp of when odds were last updated
- **`grouping_key`**: Key used for grouping related odds
- **`points`**: Point spread or total points value
- **`deep_link`**: Deep link object (null if not available)
- **`limits`**: Betting limits object

##### Limits Object Structure
```json
{
  "limits": {
    "max": 500
  }
}
```

## Complete Example Response

```json
{
  "data": [
    {
      "id": "BCE4E01B8D3D",
      "game_id": "60486-35183-2024-08-29-17",
      "start_date": "2024-08-30T00:10:00Z",
      "home_competitors": [
        {
          "id": "4F11A5896C24",
          "name": "Houston Astros",
          "abbreviation": "HOU",
          "logo": "https://a.espncdn.com/i/teamlogos/mlb/500/hou.png"
        }
      ],
      "away_competitors": [
        {
          "id": "E970E2EDDCAE",
          "name": "Kansas City Royals",
          "abbreviation": "KAN",
          "logo": "https://a.espncdn.com/i/teamlogos/mlb/500/kc.png"
        }
      ],
      "home_team_display": "Houston Astros",
      "away_team_display": "Kansas City Royals",
      "status": "unplayed",
      "is_live": false,
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      },
      "tournament": null,
      "odds": [
        {
          "id": "60486-35183-2024-08-29-17:pinnacle:moneyline:houston_astros",
          "sportsbook": "Pinnacle",
          "market": "Moneyline",
          "name": "Houston Astros",
          "is_main": true,
          "selection": "Houston Astros",
          "normalized_selection": "houston_astros",
          "market_id": "moneyline",
          "selection_line": null,
          "player_id": null,
          "team_id": "4F11A5896C24",
          "price": -156,
          "timestamp": 1724865905.59815,
          "grouping_key": "default",
          "points": null,
          "deep_link": null,
          "limits": {
            "max": 500
          }
        },
        {
          "id": "60486-35183-2024-08-29-17:pinnacle:moneyline:kansas_city_royals",
          "sportsbook": "Pinnacle",
          "market": "Moneyline",
          "name": "Kansas City Royals",
          "is_main": true,
          "selection": "Kansas City Royals",
          "normalized_selection": "kansas_city_royals",
          "market_id": "moneyline",
          "selection_line": null,
          "player_id": null,
          "team_id": "E970E2EDDCAE",
          "price": 132,
          "timestamp": 1724865905.59815,
          "grouping_key": "default",
          "points": null,
          "deep_link": null,
          "limits": {
            "max": 500
          }
        },
        {
          "id": "60486-35183-2024-08-29-17:pinnacle:run_line:houston_astros_-1_5",
          "sportsbook": "Pinnacle",
          "market": "Run Line",
          "name": "Houston Astros -1.5",
          "is_main": true,
          "selection": "Houston Astros",
          "normalized_selection": "houston_astros",
          "market_id": "run_line",
          "selection_line": null,
          "player_id": null,
          "team_id": "4F11A5896C24",
          "price": 140,
          "timestamp": 1724865905.59815,
          "grouping_key": "default:-1.5",
          "points": -1.5,
          "deep_link": null,
          "limits": null
        },
        {
          "id": "60486-35183-2024-08-29-17:pinnacle:run_line:kansas_city_royals_+1_5",
          "sportsbook": "Pinnacle",
          "market": "Run Line",
          "name": "Kansas City Royals +1.5",
          "is_main": true,
          "selection": "Kansas City Royals",
          "normalized_selection": "kansas_city_royals",
          "market_id": "run_line",
          "selection_line": null,
          "player_id": null,
          "team_id": "E970E2EDDCAE",
          "price": -170,
          "timestamp": 1724865905.59815,
          "grouping_key": "default:-1.5",
          "points": 1.5,
          "deep_link": null,
          "limits": {
            "max": 500
          }
        },
        {
          "id": "60486-35183-2024-08-29-17:pinnacle:total_runs:over_8",
          "sportsbook": "Pinnacle",
          "market": "Total Runs",
          "name": "Over 8",
          "is_main": true,
          "selection": "",
          "normalized_selection": "",
          "market_id": "total_runs",
          "selection_line": "over",
          "player_id": null,
          "team_id": null,
          "price": -110,
          "timestamp": 1724865905.59815,
          "grouping_key": "default:8.0",
          "points": 8,
          "deep_link": null,
          "limits": null
        },
        {
          "id": "60486-35183-2024-08-29-17:pinnacle:total_runs:under_8",
          "sportsbook": "Pinnacle",
          "market": "Total Runs",
          "name": "Under 8",
          "is_main": true,
          "selection": "",
          "normalized_selection": "",
          "market_id": "total_runs",
          "selection_line": "under",
          "player_id": null,
          "team_id": null,
          "price": -110,
          "timestamp": 1724865905.59815,
          "grouping_key": "default:8.0",
          "points": 8,
          "deep_link": null,
          "limits": {
            "max": 500
          }
        }
      ]
    }
  ]
}
```

## Implementation Notes

### Data Freshness and Availability
- Odds data is updated in real-time based on sportsbook availability
- Suspended or unavailable odds are excluded from the response
- Timestamp fields indicate when each odd was last updated

### Market Types Covered
The API supports various market types including but not limited to:
- **Moneyline**: Straight win/loss betting
- **Run Line/Point Spread**: Handicap betting with point spreads
- **Total Runs/Over-Under**: Total points/runs betting
- **Player Props**: Individual player performance betting
- **Team Props**: Team-specific performance betting

### Rate Limiting and Usage Considerations
- Multiple fixture IDs can be requested simultaneously (up to 5)
- Multiple sportsbooks can be queried in a single request (up to 5)
- Response size varies based on the number of available markets and odds

### Error Handling
- Invalid parameter combinations will result in appropriate error responses
- Missing required parameters will trigger validation errors
- Requests exceeding limits (5 fixtures, 5 sportsbooks) will be rejected

This comprehensive API endpoint serves as the primary interface for accessing real-time sports betting odds data across multiple sportsbooks and markets, providing developers with the detailed information necessary for building sophisticated sports betting applications and analysis tools.