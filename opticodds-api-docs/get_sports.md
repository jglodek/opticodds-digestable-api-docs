# OpticOdds Sports API Documentation

## API Endpoint: Get Supported Sports

### Description

This API endpoint returns a comprehensive list of all the sports that are currently supported or have been previously supported by the OpticOdds platform. The endpoint provides detailed information about each sport including their unique identifiers, display names, and the main betting markets available for each sport category.

### HTTP Method
`GET`

### Endpoint URL
*[Endpoint URL not specified in the provided documentation]*

### Request Parameters
*[No request parameters specified in the provided documentation]*

### Response Format
The API returns data in JSON format with the following structure:

### Response Schema

#### Root Object
| Field | Type | Description |
|-------|------|-------------|
| `data` | Array | An array containing sport objects with comprehensive information about each supported sport |

#### Sport Object Structure
Each sport object within the `data` array contains the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | The unique string identifier for the sport, used for API calls and internal references |
| `name` | String | The human-readable display name of the sport |
| `main_markets` | Array | An array of market objects representing the primary betting markets available for this sport |

#### Market Object Structure
Each market object within the `main_markets` array contains the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | The unique string identifier for the betting market type |
| `name` | String | The human-readable display name of the betting market |
| `numerical_id` | Integer | The numerical identifier associated with the market for internal system references |

### Example Response

```json
{
  "data": [
    {
      "id": "athletics",
      "name": "Athletics",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        }
      ]
    },
    {
      "id": "aussie_rules",
      "name": "Aussie Rules",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "baseball",
      "name": "Baseball",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "run_line",
          "name": "Run Line",
          "numerical_id": 1245
        },
        {
          "id": "total_runs",
          "name": "Total Runs",
          "numerical_id": 1367
        }
      ]
    },
    {
      "id": "basketball",
      "name": "Basketball",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "boxing",
      "name": "Boxing",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "total_rounds",
          "name": "Total Rounds",
          "numerical_id": 1364
        }
      ]
    },
    {
      "id": "cricket",
      "name": "Cricket",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "total_runs",
          "name": "Total Runs",
          "numerical_id": 1367
        }
      ]
    },
    {
      "id": "cycling",
      "name": "Cycling",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "total_runs",
          "name": "Total Runs",
          "numerical_id": 1367
        }
      ]
    },
    {
      "id": "darts",
      "name": "Darts",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "esports",
      "name": "eSports",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        }
      ]
    },
    {
      "id": "football",
      "name": "Football",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "golf",
      "name": "Golf",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "handicap",
          "name": "Handicap",
          "numerical_id": 936
        }
      ]
    },
    {
      "id": "hockey",
      "name": "Hockey",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "puck_line",
          "name": "Puck Line",
          "numerical_id": 1174
        },
        {
          "id": "total_goals",
          "name": "Total Goals",
          "numerical_id": 1342
        }
      ]
    },
    {
      "id": "lacrosse",
      "name": "Lacrosse",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "mma",
      "name": "MMA",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "total_rounds",
          "name": "Total Rounds",
          "numerical_id": 1364
        }
      ]
    },
    {
      "id": "motorsports",
      "name": "Motorsports",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        }
      ]
    },
    {
      "id": "olympics",
      "name": "Olympics",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        }
      ]
    },
    {
      "id": "politics",
      "name": "Politics",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        }
      ]
    },
    {
      "id": "rugby_league",
      "name": "Rugby League",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "rugby_union",
      "name": "Rugby Union",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "snooker",
      "name": "Snooker",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "soccer",
      "name": "Soccer",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "goal_spread",
          "name": "Goal Spread",
          "numerical_id": 933
        },
        {
          "id": "total_goals",
          "name": "Total Goals",
          "numerical_id": 1342
        }
      ]
    },
    {
      "id": "surfing",
      "name": "Surfing",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "swimming",
      "name": "Swimming",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "point_spread",
          "name": "Point Spread",
          "numerical_id": 1172
        },
        {
          "id": "total_points",
          "name": "Total Points",
          "numerical_id": 1358
        }
      ]
    },
    {
      "id": "table_tennis",
      "name": "Table Tennis",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "game_spread",
          "name": "Game Spread",
          "numerical_id": 929
        },
        {
          "id": "total_games",
          "name": "Total Games",
          "numerical_id": 1339
        }
      ]
    },
    {
      "id": "tennis",
      "name": "Tennis",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "game_spread",
          "name": "Game Spread",
          "numerical_id": 929
        },
        {
          "id": "total_games",
          "name": "Total Games",
          "numerical_id": 1339
        }
      ]
    },
    {
      "id": "volleyball",
      "name": "Volleyball",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "set_handicap",
          "name": "Set Handicap",
          "numerical_id": 1250
        },
        {
          "id": "total_sets",
          "name": "Total Sets",
          "numerical_id": 1374
        }
      ]
    },
    {
      "id": "water_polo",
      "name": "Water Polo",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "goal_spread",
          "name": "Goal Spread",
          "numerical_id": 933
        },
        {
          "id": "total_goals",
          "name": "Total Goals",
          "numerical_id": 1342
        }
      ]
    },
    {
      "id": "wrestling",
      "name": "Wrestling",
      "main_markets": [
        {
          "id": "moneyline",
          "name": "Moneyline",
          "numerical_id": 953
        },
        {
          "id": "total_rounds",
          "name": "Total Rounds",
          "numerical_id": 1364
        }
      ]
    }
  ]
}
```

### Supported Sports Categories

The API returns information for the following comprehensive list of sports categories:

#### Traditional Sports
- **Athletics**: Track and field events with moneyline betting markets
- **Baseball**: American professional baseball with moneyline, run line, and total runs markets
- **Basketball**: Professional and amateur basketball with moneyline, point spread, and total points markets
- **Football**: American football with moneyline, point spread, and total points markets
- **Hockey**: Ice hockey with moneyline, puck line, and total goals markets
- **Soccer**: International football with moneyline, goal spread, and total goals markets

#### Combat Sports
- **Boxing**: Professional boxing matches with moneyline and total rounds markets
- **MMA**: Mixed martial arts with moneyline and total rounds markets
- **Wrestling**: Professional and amateur wrestling with moneyline and total rounds markets

#### Racquet Sports
- **Tennis**: Professional tennis tournaments with moneyline, game spread, and total games markets
- **Table Tennis**: Ping pong competitions with moneyline, game spread, and total games markets
- **Darts**: Professional darts competitions with moneyline, point spread, and total points markets
- **Snooker**: Professional snooker with moneyline, point spread, and total points markets

#### Rugby Sports
- **Rugby League**: Rugby league competitions with moneyline, point spread, and total points markets
- **Rugby Union**: Rugby union matches with moneyline, point spread, and total points markets
- **Aussie Rules**: Australian Football League with moneyline, point spread, and total points markets

#### Niche and Specialty Sports
- **Cricket**: International cricket with moneyline and total runs markets
- **Golf**: Professional golf tournaments with moneyline and handicap markets
- **Cycling**: Competitive cycling events with moneyline and total runs markets
- **Lacrosse**: Professional and collegiate lacrosse with moneyline, point spread, and total points markets
- **Volleyball**: Indoor and beach volleyball with moneyline, set handicap, and total sets markets
- **Water Polo**: Aquatic sport with moneyline, goal spread, and total goals markets
- **Swimming**: Competitive swimming with moneyline, point spread, and total points markets
- **Surfing**: Professional surfing competitions with moneyline, point spread, and total points markets

#### Entertainment and Special Events
- **eSports**: Electronic sports competitions with moneyline markets
- **Olympics**: Olympic games and events with moneyline markets
- **Politics**: Political betting markets with moneyline options
- **Motorsports**: Auto racing events with moneyline markets

### Market Types Explained

The API provides detailed information about various betting market types available across different sports:

#### Primary Market Types
- **Moneyline (ID: moneyline, Numerical ID: 953)**: Straight win/lose bets on the outcome of an event
- **Point Spread (ID: point_spread, Numerical ID: 1172)**: Betting on the margin of victory with a handicap system
- **Total Points (ID: total_points, Numerical ID: 1358)**: Over/under betting on the total combined score

#### Sport-Specific Market Types
- **Run Line (ID: run_line, Numerical ID: 1245)**: Baseball-specific spread betting
- **Total Runs (ID: total_runs, Numerical ID: 1367)**: Over/under betting on total runs scored in baseball and cricket
- **Puck Line (ID: puck_line, Numerical ID: 1174)**: Hockey-specific spread betting
- **Total Goals (ID: total_goals, Numerical ID: 1342)**: Over/under betting on total goals in hockey, soccer, and water polo
- **Goal Spread (ID: goal_spread, Numerical ID: 933)**: Spread betting specific to soccer and water polo
- **Game Spread (ID: game_spread, Numerical ID: 929)**: Spread betting for tennis and table tennis
- **Total Games (ID: total_games, Numerical ID: 1339)**: Over/under betting on total games in tennis and table tennis
- **Set Handicap (ID: set_handicap, Numerical ID: 1250)**: Handicap betting for volleyball sets
- **Total Sets (ID: total_sets, Numerical ID: 1374)**: Over/under betting on total sets in volleyball
- **Total Rounds (ID: total_rounds, Numerical ID: 1364)**: Over/under betting on combat sports rounds
- **Handicap (ID: handicap, Numerical ID: 936)**: General handicap betting, primarily used in golf

### Technical Implementation Details

#### Response Format
- **Content-Type**: application/json
- **Character Encoding**: UTF-8
- **Response Structure**: Single-level JSON object with a "data" array containing sport objects

#### Data Consistency
- All sport IDs use lowercase strings with underscores for multi-word sports
- Market numerical IDs are unique integers used for internal system references
- Market string IDs use lowercase with underscores for consistency

#### Usage Considerations
- The API returns all sports that have been supported, including those that may currently be inactive
- The main_markets array contains the primary betting markets for each sport, but additional markets may be available
- Sport and market IDs should be used for making subsequent API calls to retrieve specific odds or event information

This comprehensive sports listing provides developers with all necessary information to understand the breadth of sports coverage available through the OpticOdds platform and the specific betting markets supported for each sport category.