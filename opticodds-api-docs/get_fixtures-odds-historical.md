# API Documentation: Historical Odds Endpoint

## Description

Get a list of historical odds for a given combination of sportsbooks, fixtures, and markets. These game odds are related to specific events, they do not apply for entire tournaments or entire seasons.

**Note:** This data is available only from the time odds are posted by the sportsbook up until just before the fixture start time. Historical data is retained on a rolling 2-month basis.

## Endpoint

```
GET /api/v3/fixtures/odds/historical
```

## Required Parameters

### fixture_id
- **Type:** String
- **Required:** Yes
- **Description:** This is required and you can only pass a single fixture ID.

### sportsbook
- **Type:** String or Array
- **Required:** Yes  
- **Description:** The sportsbooks that you want odds for. You can pass up to 5 of these per request. You can pass the id or the name.

## Optional Parameters

### market
- **Type:** String
- **Required:** Only when using `include_timeseries`
- **Description:** The markets that you want odds for. You can pass the id or the name.

### is_main
- **Type:** Boolean
- **Default:** false
- **Description:** Passing `is_main=true` will limit the data returned to only return the main lines. Since this is a historical view, the `name` field might not correspond to a name that was returned from the `/fixtures/odds` endpoint since the bet points could change.

### include_timeseries
- **Type:** Boolean
- **Default:** false
- **Description:** For this to work, you will need a separate permission on your key. This will return the odd movements as we detect them. When using this parameter, you must also pass a `market` parameter.

## Response Structure

The API returns a JSON object with the following structure:

```json
{
  "data": [
    {
      "id": "string",
      "game_id": "string", 
      "start_date": "ISO 8601 datetime",
      "home_competitors": [
        {
          "id": "string",
          "name": "string",
          "abbreviation": "string",
          "logo": "URL string"
        }
      ],
      "away_competitors": [
        {
          "id": "string", 
          "name": "string",
          "abbreviation": "string",
          "logo": "URL string"
        }
      ],
      "home_team_display": "string",
      "away_team_display": "string",
      "status": "string",
      "is_live": boolean,
      "sport": {
        "id": "string",
        "name": "string"
      },
      "league": {
        "id": "string", 
        "name": "string"
      },
      "tournament": null,
      "odds": [
        {
          "id": "string",
          "sportsbook": "string",
          "market": "string", 
          "name": "string",
          "is_main": boolean,
          "selection": "string",
          "normalized_selection": "string",
          "market_id": "string",
          "selection_line": "string",
          "player_id": null,
          "team_id": null,
          "deep_link_info": null,
          "entries": [
            {
              "price": number,
              "timestamp": unix_timestamp,
              "points": number,
              "locked": boolean
            }
          ],
          "olv": {
            "price": number,
            "points": number
          },
          "clv": {
            "price": number,
            "points": number
          }
        }
      ]
    }
  ]
}
```

### Response Fields

#### Root Level
- **data**: Array of fixture objects containing historical odds data

#### Fixture Object
- **id**: Unique identifier for the fixture
- **game_id**: Game-specific identifier 
- **start_date**: ISO 8601 formatted start date and time
- **home_competitors**: Array of home team information
- **away_competitors**: Array of away team information  
- **home_team_display**: Display name for home team
- **away_team_display**: Display name for away team
- **status**: Current status of the fixture (e.g., "completed")
- **is_live**: Boolean indicating if the fixture is currently live
- **sport**: Object containing sport ID and name
- **league**: Object containing league ID and name
- **tournament**: Tournament information (null if not applicable)
- **odds**: Array of odds objects for the fixture

#### Odds Object
- **id**: Unique identifier for the odds entry
- **sportsbook**: Name of the sportsbook
- **market**: Market type (e.g., "Total Runs")
- **name**: Specific bet name (e.g., "Over 8.5", "Under 9")
- **is_main**: Boolean indicating if this is a main line
- **selection**: Selection details
- **normalized_selection**: Normalized selection format
- **market_id**: Market identifier
- **selection_line**: Type of selection line (e.g., "over", "under")
- **player_id**: Player identifier (null if not applicable)
- **team_id**: Team identifier (null if not applicable)
- **deep_link_info**: Deep linking information (null if not available)
- **entries**: Array of historical price entries (only populated when `include_timeseries=true`)
- **olv**: Opening Line Value object with price and points
- **clv**: Closing Line Value object with price and points

#### Entries Object (Timeseries Data)
- **price**: The odds price at this timestamp
- **timestamp**: Unix timestamp of when the odds were recorded
- **points**: Point spread or total points for the bet
- **locked**: Boolean indicating if the odds were locked

#### OLV/CLV Objects
- **price**: The odds price (American odds format)
- **points**: Point spread or total points for the bet

## Example Requests

### Basic Request
```
GET /api/v3/fixtures/odds/historical?fixture_id=F075D920FFCA&market=Total%20Runs&sportsbook=BetMGM
```

### Main Lines Only
```  
GET /api/v3/fixtures/odds/historical?fixture_id=F075D920FFCA&market=Total%20Runs&sportsbook=BetMGM&is_main=true
```

### With Timeseries Data
```
GET /api/v3/fixtures/odds/historical?fixture_id=F075D920FFCA&market=Total%20Runs&sportsbook=BetMGM&include_timeseries=true
```

## Important Notes

1. **Parameter Requirements:** You must pass a single `fixture_id` and at least 1 (up to 5) `sportsbook` parameters to this endpoint.

2. **Timeseries Permission:** If you are passing `include_timeseries`, then you must pass a `market` parameter as well. You will also need separate permission on your API key to access timeseries data.

3. **Historical Data Retention:** Historical data is retained on a rolling 2-month basis.

4. **Data Availability:** This data is only available from the time odds are posted by the sportsbook up until just before the fixture start time.

5. **Main Lines Behavior:** When using `is_main=true`, the `name` field might not correspond to a name that was returned from the `/fixtures/odds` endpoint since the bet points could change over time.

6. **Multiple Sportsbooks:** You can request odds from up to 5 different sportsbooks in a single API call.

7. **Market and Sportsbook Identification:** Both market and sportsbook parameters accept either ID or name values for flexibility.