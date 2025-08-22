# Sportsbooks Last Polled API Endpoint

## Overview

This API endpoint returns a comprehensive list of the last time the system checked for odds updates from various sportsbooks. This endpoint provides crucial timing information that is distinct from the `timestamp` field found on the `/fixtures/odds` endpoint.

## Important Distinction

The timestamps returned by this endpoint represent when the system last received at least one valid odd from each sportsbook for the specified parameters. This is fundamentally different from the `/fixtures/odds` endpoint, which only updates when the system detects an actual change in price or points. The sportsbooks last-polled endpoint provides visibility into the polling frequency and recency of data collection attempts, regardless of whether odds values changed.

## Endpoint Details

**Base URL:** `https://api.opticodds.com/api/v3/sportsbooks/last-polled`

**HTTP Method:** GET

**Content Type:** application/json

## Required Parameters

You must provide at least one of the following required parameters:

### league (Required if fixture_id not provided)
- **Type:** String
- **Description:** The league for which you want to retrieve sportsbook last polling information
- **Format:** You can pass either the league ID or the league name
- **Examples:** 
  - `league=nfl`
  - `league=NFL`

### fixture_id (Required if league not provided)
- **Type:** String
- **Description:** The unique identifier of the specific fixture you want information for
- **Limit:** You can pass up to 5 fixture IDs per request
- **Format:** Alphanumeric string identifier
- **Example:** `fixture_id=5EBE447F80C5`

## Optional Parameters

### sportsbook
- **Type:** String
- **Description:** Limits results to specific sportsbooks
- **Format:** You can pass either the sportsbook ID or the sportsbook name
- **Limit:** You can pass up to 5 sportsbooks per request
- **Examples:**
  - `sportsbook=draftkings`
  - `sportsbook=DraftKings`
  - `sportsbook=bet365,pinnacle,bovada` (multiple sportsbooks)

## Response Structure

The API returns a JSON object with the following structure:

### Root Object
```json
{
  "data": [
    // Array of polling information objects
  ]
}
```

### Data Array Elements
Each element in the data array contains:

#### league (Object)
- **id** (String): The unique identifier for the league
- **name** (String): The human-readable name of the league

#### fixture_id (String or null)
- When querying by league: Returns `null`
- When querying by fixture_id: Returns the specific fixture identifier

#### sportsbooks (Array)
An array of sportsbook objects, each containing:
- **id** (String): The unique identifier for the sportsbook
- **name** (String): The human-readable name of the sportsbook
- **timestamp** (Integer): Unix timestamp representing the last time the system successfully retrieved at least one valid odd from this sportsbook

## Example Requests and Responses

### Example 1: All Sportsbooks for NFL League

**Request URL:**
```
https://api.opticodds.com/api/v3/sportsbooks/last-polled?league=NFL
```

**Response:**
```json
{
  "data": [
    {
      "league": {
        "id": "nfl",
        "name": "NFL"
      },
      "fixture_id": null,
      "sportsbooks": [
        {
          "id": "prophet_x",
          "name": "Prophet X",
          "timestamp": 1726232938
        },
        {
          "id": "betonline",
          "name": "BetOnline",
          "timestamp": 1726242194
        },
        {
          "id": "1xbet",
          "name": "1XBet",
          "timestamp": 1726242165
        },
        {
          "id": "hotstreak",
          "name": "HotStreak",
          "timestamp": 1726242200
        },
        {
          "id": "caesars_tennessee_",
          "name": "Caesars (Tennessee)",
          "timestamp": 1726242180
        },
        {
          "id": "parlayplay",
          "name": "ParlayPlay",
          "timestamp": 1726242197
        },
        {
          "id": "prizepicks",
          "name": "PrizePicks",
          "timestamp": 1726242185
        },
        {
          "id": "prizepicks_5_or_6_pick_flex_",
          "name": "PrizePicks (5 or 6 Pick Flex)",
          "timestamp": 1726242185
        },
        {
          "id": "underdog_fantasy_3_or_5_pick_",
          "name": "Underdog Fantasy (3 or 5 Pick)",
          "timestamp": 1726242198
        },
        {
          "id": "underdog_fantasy_6_pick_",
          "name": "Underdog Fantasy (6 Pick)",
          "timestamp": 1726242198
        },
        {
          "id": "underdog_fantasy",
          "name": "Underdog Fantasy",
          "timestamp": 1726242198
        },
        {
          "id": "bally_bet",
          "name": "Bally Bet",
          "timestamp": 1726242194
        },
        {
          "id": "betr_australia_",
          "name": "betr (Australia)",
          "timestamp": 1726242198
        },
        {
          "id": "betr",
          "name": "Betr",
          "timestamp": 1726242194
        },
        {
          "id": "bet365",
          "name": "bet365",
          "timestamp": 1726242196
        },
        {
          "id": "betr_picks_boosted_",
          "name": "Betr Picks (BOOSTED)",
          "timestamp": 1726242194
        },
        {
          "id": "betr_picks_all_",
          "name": "Betr Picks (All)",
          "timestamp": 1726242194
        },
        {
          "id": "betr_picks",
          "name": "Betr Picks",
          "timestamp": 1726242194
        },
        {
          "id": "hard_rock",
          "name": "Hard Rock",
          "timestamp": 1726242201
        },
        {
          "id": "action_24_7",
          "name": "Action 24/7",
          "timestamp": 1726242193
        },
        {
          "id": "thrillzz",
          "name": "Thrillzz",
          "timestamp": 1726242196
        },
        {
          "id": "betdsi",
          "name": "BetDSI",
          "timestamp": 1726242198
        },
        {
          "id": "bet99",
          "name": "BET99",
          "timestamp": 1726242196
        },
        {
          "id": "betanysports",
          "name": "BetAnySports",
          "timestamp": 1726242195
        },
        {
          "id": "wind_creek",
          "name": "Wind Creek",
          "timestamp": 1726242198
        },
        {
          "id": "betfred",
          "name": "Betfred",
          "timestamp": 1726242198
        },
        {
          "id": "betmgm",
          "name": "BetMGM",
          "timestamp": 1726242198
        },
        {
          "id": "bwin",
          "name": "bwin",
          "timestamp": 1726242198
        },
        {
          "id": "partypoker",
          "name": "partypoker",
          "timestamp": 1726242198
        },
        {
          "id": "borgata",
          "name": "Borgata",
          "timestamp": 1726242198
        },
        {
          "id": "betano",
          "name": "Betano",
          "timestamp": 1726242193
        },
        {
          "id": "juicebet",
          "name": "JuiceBet",
          "timestamp": 1726242199
        },
        {
          "id": "betplay",
          "name": "Betplay",
          "timestamp": 1726242199
        },
        {
          "id": "betrivers_new_york_",
          "name": "BetRivers (New York)",
          "timestamp": 1726242200
        },
        {
          "id": "betsafe",
          "name": "Betsafe",
          "timestamp": 1726242200
        },
        {
          "id": "leovegas",
          "name": "LeoVegas",
          "timestamp": 1726242194
        },
        {
          "id": "desert_diamond",
          "name": "Desert Diamond",
          "timestamp": 1726242194
        },
        {
          "id": "twinspires",
          "name": "TwinSpires",
          "timestamp": 1726242194
        },
        {
          "id": "four_winds",
          "name": "Four Winds",
          "timestamp": 1726242194
        },
        {
          "id": "sugarhouse",
          "name": "SugarHouse",
          "timestamp": 1726242194
        },
        {
          "id": "betrivers",
          "name": "BetRivers",
          "timestamp": 1726242194
        },
        {
          "id": "betparx",
          "name": "betPARX",
          "timestamp": 1726242194
        },
        {
          "id": "betvictor",
          "name": "BetVictor",
          "timestamp": 1726242189
        },
        {
          "id": "betsson",
          "name": "Betsson",
          "timestamp": 1726242191
        },
        {
          "id": "bovada",
          "name": "Bovada",
          "timestamp": 1726242197
        },
        {
          "id": "bodog",
          "name": "Bodog",
          "timestamp": 1726242197
        },
        {
          "id": "boom_fantasy_5_pick_insured_",
          "name": "Boom Fantasy (5 Pick Insured)",
          "timestamp": 1726242197
        },
        {
          "id": "betdex",
          "name": "BetDEX",
          "timestamp": 1726242194
        },
        {
          "id": "casumo",
          "name": "Casumo",
          "timestamp": 1726242193
        },
        {
          "id": "bookmaker",
          "name": "BookMaker",
          "timestamp": 1726242179
        },
        {
          "id": "draftkings",
          "name": "DraftKings",
          "timestamp": 1726242186
        },
        {
          "id": "crab_sports",
          "name": "Crab Sports",
          "timestamp": 1726242197
        },
        {
          "id": "dabble_3_or_5_pick_",
          "name": "Dabble (3 or 5 Pick)",
          "timestamp": 1726242196
        },
        {
          "id": "circa_vegas",
          "name": "Circa Vegas",
          "timestamp": 1726242200
        },
        {
          "id": "circa_sports",
          "name": "Circa Sports",
          "timestamp": 1726242200
        },
        {
          "id": "dafabet",
          "name": "Dafabet",
          "timestamp": 1726242194
        },
        {
          "id": "betus",
          "name": "BetUS",
          "timestamp": 1726242195
        },
        {
          "id": "draftkings_pick_6_",
          "name": "DraftKings (Pick 6)",
          "timestamp": 1726242201
        },
        {
          "id": "fliff",
          "name": "Fliff",
          "timestamp": 1726242195
        },
        {
          "id": "firekeepers",
          "name": "FireKeepers",
          "timestamp": 1726242200
        },
        {
          "id": "fanatics",
          "name": "Fanatics",
          "timestamp": 1726242189
        },
        {
          "id": "betwhale",
          "name": "betwhale",
          "timestamp": 1726242198
        },
        {
          "id": "ggbet",
          "name": "GGBet",
          "timestamp": 1726242198
        },
        {
          "id": "northstar_bets",
          "name": "NorthStar Bets",
          "timestamp": 1726242197
        },
        {
          "id": "xbet",
          "name": "Xbet",
          "timestamp": 1726242190
        },
        {
          "id": "mybookie",
          "name": "MyBookie",
          "timestamp": 1726242190
        },
        {
          "id": "ladbrokes_australia_",
          "name": "Ladbrokes (Australia)",
          "timestamp": 1726242190
        },
        {
          "id": "neds",
          "name": "Neds",
          "timestamp": 1726242190
        },
        {
          "id": "novig",
          "name": "Novig",
          "timestamp": 1726242194
        },
        {
          "id": "pinnacle",
          "name": "Pinnacle",
          "timestamp": 1726242197
        },
        {
          "id": "pinny",
          "name": "Pinny",
          "timestamp": 1726242197
        },
        {
          "id": "pointsbet_australia_",
          "name": "PointsBet (Australia)",
          "timestamp": 1726242194
        },
        {
          "id": "proline",
          "name": "Proline",
          "timestamp": 1726242190
        },
        {
          "id": "play_alberta",
          "name": "Play Alberta",
          "timestamp": 1726242191
        },
        {
          "id": "rebet",
          "name": "Rebet",
          "timestamp": 1726242200
        },
        {
          "id": "sleeper",
          "name": "Sleeper",
          "timestamp": 1726242190
        },
        {
          "id": "playnow",
          "name": "PlayNow",
          "timestamp": 1726242183
        },
        {
          "id": "sporttrade_colorado_",
          "name": "Sporttrade (Colorado)",
          "timestamp": 1726242187
        },
        {
          "id": "sporttrade",
          "name": "Sporttrade",
          "timestamp": 1726242200
        },
        {
          "id": "sx_bet",
          "name": "SX Bet",
          "timestamp": 1726242198
        },
        {
          "id": "tab",
          "name": "TAB",
          "timestamp": 1726242193
        },
        {
          "id": "tabtouch",
          "name": "TABtouch",
          "timestamp": 1726242194
        },
        {
          "id": "espn_bet",
          "name": "ESPN BET",
          "timestamp": 1726242192
        },
        {
          "id": "thescore",
          "name": "theScore",
          "timestamp": 1726242192
        },
        {
          "id": "tonybet",
          "name": "TonyBet",
          "timestamp": 1726242194
        },
        {
          "id": "underdog_sportsbook",
          "name": "Underdog Sportsbook",
          "timestamp": 1726242199
        },
        {
          "id": "unibet_australia_",
          "name": "Unibet (Australia)",
          "timestamp": 1726242199
        },
        {
          "id": "unibet",
          "name": "Unibet",
          "timestamp": 1726242195
        },
        {
          "id": "caesars_illinois_",
          "name": "Caesars (Illinois)",
          "timestamp": 1726242192
        },
        {
          "id": "caesars_ontario_",
          "name": "Caesars (Ontario)",
          "timestamp": 1726242195
        },
        {
          "id": "unibet_united_kingdom_",
          "name": "Unibet (United Kingdom)",
          "timestamp": 1726242200
        },
        {
          "id": "vivid_picks_4_pick_",
          "name": "Vivid Picks (4 Pick)",
          "timestamp": 1726242196
        },
        {
          "id": "vivid_picks",
          "name": "Vivid Picks",
          "timestamp": 1726242196
        },
        {
          "id": "caesars",
          "name": "Caesars",
          "timestamp": 1726242190
        },
        {
          "id": "william_hill",
          "name": "William Hill",
          "timestamp": 1726242190
        },
        {
          "id": "sportsbet",
          "name": "Sportsbet",
          "timestamp": 1726242172
        },
        {
          "id": "bc_game",
          "name": "BC.GAME",
          "timestamp": 1726239738
        }
      ]
    }
  ]
}
```

### Example 2: DraftKings Only for a Specific Fixture

**Request URL:**
```
https://api.opticodds.com/api/v3/sportsbooks/last-polled?fixture_id=5EBE447F80C5&sportsbook=DraftKings
```

**Response:**
```json
{
  "data": [
    {
      "league": {
        "id": "nfl",
        "name": "NFL"
      },
      "fixture_id": "5EBE447F80C5",
      "sportsbooks": [
        {
          "id": "draftkings",
          "name": "DraftKings",
          "timestamp": 1726242427
        }
      ]
    }
  ]
}
```

## Supported Sportsbooks

The API supports a comprehensive list of major sportsbooks, including but not limited to:

### Traditional Sportsbooks
- bet365
- DraftKings
- BetMGM
- Caesars
- FanDuel (Fanatics)
- BetRivers
- Pinnacle
- Bovada
- BetUS
- MyBookie

### Fantasy Sports Platforms
- PrizePicks
- Underdog Fantasy
- Sleeper
- DraftKings (Pick 6)

### Regional and International Sportsbooks
- bet365
- Unibet (multiple regions)
- Betsson
- LeoVegas
- Sportsbet (Australia)
- TAB
- Neds

### Specialty and Emerging Platforms
- Novig
- Fliff
- Thrillzz
- Rebet

## Technical Considerations

### Timestamp Format
All timestamps are provided as Unix timestamps (seconds since January 1, 1970, UTC). These can be easily converted to human-readable dates in your preferred programming language.

### Rate Limiting
Please be aware of any rate limiting policies that may apply to your API key tier. Check your account dashboard for specific limits.

### Data Freshness
The timestamps indicate when the system last successfully retrieved odds data, not when the odds themselves were last updated by the sportsbook. This distinction is crucial for understanding data recency and system health monitoring.

### Error Handling
Implement proper error handling for cases where:
- No data is available for the specified parameters
- Invalid league or fixture IDs are provided
- Sportsbook identifiers are not recognized
- Network timeouts or API errors occur

This endpoint is particularly valuable for monitoring data collection health, understanding polling frequencies, and ensuring your applications have visibility into the recency of available odds data from various sources.