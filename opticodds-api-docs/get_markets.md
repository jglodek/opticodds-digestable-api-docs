# OpticOdds Markets API Documentation

## Endpoint Overview

**Description:** Returns a list of all the markets that are / have been supported by OpticOdds.

**Endpoint URL:** `https://api.opticodds.com/api/v3/markets`

**HTTP Method:** GET

**API Version:** v3

## Parameters

**Specific Parameter Information:**
The endpoint accepts query parameters to filter the market data. For a complete list of all available parameters, users should refer to the full parameter documentation provided at the bottom of the original API documentation page.

**Example Parameter Usage:**
- `sport` - Filter markets by sport (e.g., `sport=aussie_rules`)

## Request Format

**Base URL:** `https://api.opticodds.com/api/v3/markets`

**Example Request URL:** `https://api.opticodds.com/api/v3/markets?sport=aussie_rules`

## Response Format

**Content Type:** JSON

**Response Structure:** The API returns a JSON object containing a `data` array with comprehensive market information.

### Root Response Object

| Field | Type | Description |
|-------|------|-------------|
| `data` | Array | Array of market objects containing detailed market information |

### Market Object Structure

Each market object in the `data` array contains the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | Unique string identifier for the market (e.g., "team_total", "2nd_half_moneyline") |
| `name` | String | Human-readable display name of the market (e.g., "Team Total", "2nd Half Moneyline") |
| `numerical_id` | Integer | Unique numerical identifier for the market |
| `sports` | Array | Array of sport objects indicating which sports support this market |

### Sport Object Structure

Each sport object within a market contains:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | Unique string identifier for the sport (e.g., "aussie_rules") |
| `name` | String | Human-readable display name of the sport (e.g., "Aussie Rules") |
| `leagues` | Array | Array of league objects that support this market within the sport |

### League Object Structure

Each league object within a sport contains:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | Unique string identifier for the league (e.g., "afl") |
| `name` | String | Human-readable display name of the league (e.g., "AFL") |
| `sportsbooks` | Array | Array of sportsbook objects that offer this market for the league |

### Sportsbook Object Structure

Each sportsbook object within a league contains:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | Unique string identifier for the sportsbook (e.g., "bet365", "draftkings", "ladbrokes_australia_") |
| `name` | String | Human-readable display name of the sportsbook (e.g., "bet365", "DraftKings", "Ladbrokes (Australia)") |

## Example Response

**Note:** The following example response is provided to demonstrate the JSON format structure. Actual response data may differ from the example shown.

**Example Request:** `https://api.opticodds.com/api/v3/markets?sport=aussie_rules`

```json
{
  "data": [
    {
      "id": "team_total",
      "name": "Team Total",
      "numerical_id": 1261,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "1xbet",
                  "name": "1XBet"
                },
                {
                  "id": "ladbrokes",
                  "name": "Ladbrokes"
                },
                {
                  "id": "sportsbet",
                  "name": "Sportsbet"
                },
                {
                  "id": "draftkings",
                  "name": "DraftKings"
                },
                {
                  "id": "bet365",
                  "name": "bet365"
                },
                {
                  "id": "dabble_australia_",
                  "name": "Dabble (Australia)"
                },
                {
                  "id": "elite_bet",
                  "name": "Elite Bet"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "2nd_half_moneyline",
      "name": "2nd Half Moneyline",
      "numerical_id": 323,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "leovegas",
                  "name": "LeoVegas"
                },
                {
                  "id": "twinspires",
                  "name": "TwinSpires"
                },
                {
                  "id": "unibet_united_kingdom_",
                  "name": "Unibet (United Kingdom)"
                },
                {
                  "id": "four_winds",
                  "name": "Four Winds"
                },
                {
                  "id": "betrivers",
                  "name": "BetRivers"
                },
                {
                  "id": "ladbrokes_australia_",
                  "name": "Ladbrokes (Australia)"
                },
                {
                  "id": "casumo",
                  "name": "Casumo"
                },
                {
                  "id": "northstar_bets",
                  "name": "NorthStar Bets"
                },
                {
                  "id": "unibet_australia_",
                  "name": "Unibet (Australia)"
                },
                {
                  "id": "bet365",
                  "name": "bet365"
                },
                {
                  "id": "unibet",
                  "name": "Unibet"
                },
                {
                  "id": "betrivers_new_york_",
                  "name": "BetRivers (New York)"
                },
                {
                  "id": "sugarhouse",
                  "name": "SugarHouse"
                },
                {
                  "id": "desert_diamond",
                  "name": "Desert Diamond"
                },
                {
                  "id": "bally_bet",
                  "name": "Bally Bet"
                },
                {
                  "id": "tabtouch",
                  "name": "TABtouch"
                },
                {
                  "id": "neds",
                  "name": "Neds"
                },
                {
                  "id": "1xbet",
                  "name": "1XBet"
                },
                {
                  "id": "betparx",
                  "name": "betPARX"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "first_goal_scorer",
      "name": "First Goal Scorer",
      "numerical_id": 920,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "leovegas",
                  "name": "LeoVegas"
                },
                {
                  "id": "playup_australia_",
                  "name": "PlayUp (Australia)"
                },
                {
                  "id": "unibet_australia_",
                  "name": "Unibet (Australia)"
                },
                {
                  "id": "bet365",
                  "name": "bet365"
                },
                {
                  "id": "twinspires",
                  "name": "TwinSpires"
                },
                {
                  "id": "dabble_australia_",
                  "name": "Dabble (Australia)"
                },
                {
                  "id": "unibet_united_kingdom_",
                  "name": "Unibet (United Kingdom)"
                },
                {
                  "id": "tab",
                  "name": "TAB"
                },
                {
                  "id": "elite_bet",
                  "name": "Elite Bet"
                },
                {
                  "id": "four_winds",
                  "name": "Four Winds"
                },
                {
                  "id": "unibet",
                  "name": "Unibet"
                },
                {
                  "id": "betrivers",
                  "name": "BetRivers"
                },
                {
                  "id": "sugarhouse",
                  "name": "SugarHouse"
                },
                {
                  "id": "picklebet",
                  "name": "Picklebet"
                },
                {
                  "id": "betr_australia_",
                  "name": "betr (Australia)"
                },
                {
                  "id": "desert_diamond",
                  "name": "Desert Diamond"
                },
                {
                  "id": "bet_right",
                  "name": "Bet Right"
                },
                {
                  "id": "bally_bet",
                  "name": "Bally Bet"
                },
                {
                  "id": "pointsbet_australia_",
                  "name": "PointsBet (Australia)"
                },
                {
                  "id": "tabtouch",
                  "name": "TABtouch"
                },
                {
                  "id": "casumo",
                  "name": "Casumo"
                },
                {
                  "id": "draftkings",
                  "name": "DraftKings"
                },
                {
                  "id": "northstar_bets",
                  "name": "NorthStar Bets"
                },
                {
                  "id": "1xbet",
                  "name": "1XBet"
                },
                {
                  "id": "tab_new_zealand_",
                  "name": "TAB (New Zealand)"
                },
                {
                  "id": "betparx",
                  "name": "betPARX"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "2nd_quarter_total_points_odd_even",
      "name": "2nd Quarter Total Points Odd/Even",
      "numerical_id": 479,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "ladbrokes_australia_",
                  "name": "Ladbrokes (Australia)"
                },
                {
                  "id": "neds",
                  "name": "Neds"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "2nd_half_total_points",
      "name": "2nd Half Total Points",
      "numerical_id": 379,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "1xbet",
                  "name": "1XBet"
                },
                {
                  "id": "sportsbet",
                  "name": "Sportsbet"
                },
                {
                  "id": "playup_australia_",
                  "name": "PlayUp (Australia)"
                },
                {
                  "id": "bet365",
                  "name": "bet365"
                },
                {
                  "id": "ladbrokes_australia_",
                  "name": "Ladbrokes (Australia)"
                },
                {
                  "id": "neds",
                  "name": "Neds"
                },
                {
                  "id": "tab_new_zealand_",
                  "name": "TAB (New Zealand)"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "moneyline_3-way",
      "name": "Moneyline 3-Way",
      "numerical_id": 954,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "1xbet",
                  "name": "1XBet"
                },
                {
                  "id": "picklebet",
                  "name": "Picklebet"
                },
                {
                  "id": "dabble_australia_",
                  "name": "Dabble (Australia)"
                },
                {
                  "id": "topsport",
                  "name": "TopSport"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "total_goals_odd_even",
      "name": "Total Goals Odd/Even",
      "numerical_id": 1345,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "bet365",
                  "name": "bet365"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "4th_quarter_moneyline_3-way",
      "name": "4th Quarter Moneyline 3-Way",
      "numerical_id": 685,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "1xbet",
                  "name": "1XBet"
                },
                {
                  "id": "neds",
                  "name": "Neds"
                },
                {
                  "id": "tab_new_zealand_",
                  "name": "TAB (New Zealand)"
                },
                {
                  "id": "ladbrokes_australia_",
                  "name": "Ladbrokes (Australia)"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "1st_half_team_total",
      "name": "1st Half Team Total",
      "numerical_id": 128,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "1xbet",
                  "name": "1XBet"
                },
                {
                  "id": "sportsbet",
                  "name": "Sportsbet"
                },
                {
                  "id": "bet365",
                  "name": "bet365"
                },
                {
                  "id": "dabble_australia_",
                  "name": "Dabble (Australia)"
                },
                {
                  "id": "draftkings",
                  "name": "DraftKings"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "id": "anytime_goal_scorer",
      "name": "Anytime Goal Scorer",
      "numerical_id": 890,
      "sports": [
        {
          "id": "aussie_rules",
          "name": "Aussie Rules",
          "leagues": [
            {
              "id": "afl",
              "name": "AFL",
              "sportsbooks": [
                {
                  "id": "leovegas",
                  "name": "LeoVegas"
                },
                {
                  "id": "unibet_australia_",
                  "name": "Unibet (Australia)"
                },
                {
                  "id": "twinspires",
                  "name": "TwinSpires"
                },
                {
                  "id": "dabble_australia_",
                  "name": "Dabble (Australia)"
                },
                {
                  "id": "unibet_united_kingdom_",
                  "name": "Unibet (United Kingdom)"
                },
                {
                  "id": "elite_bet",
                  "name": "Elite Bet"
                },
                {
                  "id": "four_winds",
                  "name": "Four Winds"
                },
                {
                  "id": "unibet",
                  "name": "Unibet"
                },
                {
                  "id": "betrivers",
                  "name": "BetRivers"
                },
                {
                  "id": "sugarhouse",
                  "name": "SugarHouse"
                },
                {
                  "id": "betr_australia_",
                  "name": "betr (Australia)"
                },
                {
                  "id": "desert_diamond",
                  "name": "Desert Diamond"
                },
                {
                  "id": "bet_right",
                  "name": "Bet Right"
                },
                {
                  "id": "bally_bet",
                  "name": "Bally Bet"
                },
                {
                  "id": "sportsbet",
                  "name": "Sportsbet"
                },
                {
                  "id": "pointsbet_australia_",
                  "name": "PointsBet (Australia)"
                },
                {
                  "id": "tabtouch",
                  "name": "TABtouch"
                },
                {
                  "id": "ladbrokes_australia_",
                  "name": "Ladbrokes (Australia)"
                },
                {
                  "id": "neds",
                  "name": "Neds"
                },
                {
                  "id": "casumo",
                  "name": "Casumo"
                },
                {
                  "id": "draftkings",
                  "name": "DraftKings"
                },
                {
                  "id": "northstar_bets",
                  "name": "NorthStar Bets"
                },
                {
                  "id": "tab_new_zealand_",
                  "name": "TAB (New Zealand)"
                },
                {
                  "id": "betparx",
                  "name": "betPARX"
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

## Market Types Included in Example Response

The example response demonstrates several different types of betting markets that are supported by OpticOdds:

1. **Team Total** - Betting on the total points/score achieved by a specific team
2. **2nd Half Moneyline** - Money line betting specifically for the second half of a game
3. **First Goal Scorer** - Betting on which player will score the first goal in a match
4. **2nd Quarter Total Points Odd/Even** - Betting on whether the total points in the second quarter will be odd or even
5. **2nd Half Total Points** - Betting on the total points scored in the second half
6. **Moneyline 3-Way** - Traditional three-outcome money line betting (Team A wins, Team B wins, Draw)
7. **Total Goals Odd/Even** - Betting on whether the total number of goals will be odd or even
8. **4th Quarter Moneyline 3-Way** - Three-outcome money line betting for the fourth quarter only
9. **1st Half Team Total** - Betting on a specific team's total points in the first half
10. **Anytime Goal Scorer** - Betting on which player will score a goal at any point during the match

## Technical Details

- **Data Format:** JSON
- **Encoding:** UTF-8
- **Response Size:** Variable (depends on filters applied and number of markets returned)
- **Pagination:** Not specified in the provided documentation
- **Rate Limiting:** Not specified in the provided documentation

## Important Notes

1. **Example Data Disclaimer:** The API documentation explicitly states that example responses are provided solely to demonstrate JSON format structure and that actual response data may differ significantly from the examples shown.

2. **Parameter Documentation:** Complete parameter documentation is referenced to be available at the bottom of the original API documentation page, which would contain comprehensive details about all available query parameters and their usage.

3. **Dynamic Data:** Market availability, supported sportsbooks, and league coverage may change over time as OpticOdds adds or removes support for various markets and providers.

4. **Regional Variations:** Some sportsbooks appear with regional indicators in their IDs (e.g., "ladbrokes_australia_", "unibet_united_kingdom_"), suggesting that market availability may vary by geographical region.