# Injuries API Endpoint

## Description

Get a list of currently active injuries.

**Supported leagues:** NFL, NBA, NHL, MLB, NCAAF, & NCAAB.

## Specific Parameter Information

For a full list of parameters, scroll to the bottom of this page.

**You must pass at least one sport and/or league.**

### Parameters

#### `sport`
The sport you want data for. You can pass the id or the name.

#### `league`
The league you want data for. You can pass the id or the name.

#### `team_id`
The team_ids you want data for.

## Example Responses

### URL
```
https://api.opticodds.com/api/v3/injuries?league=MLB
```

### JSON Response

```typescript
{
  "data": [
    {
      "id": "baseball:mlb:C46FD84D48DF",
      "player": {
        "id": "C46FD84D48DF",
        "name": "Shane Baz",
        "position": "SP",
        "number": 11
      },
      "team": {
        "id": "FE07CF8C473A",
        "name": "Tampa Bay Rays"
      },
      "status": "Day-To-Day",
      "type": "Illness",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:3A458DB8B92B",
      "player": {
        "id": "3A458DB8B92B",
        "name": "Wilmer Flores",
        "position": "1B",
        "number": 41
      },
      "team": {
        "id": "806CF8213D38",
        "name": "San Francisco Giants"
      },
      "status": "60-Day IL",
      "type": "Knee",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:D28676DC6373",
      "player": {
        "id": "D28676DC6373",
        "name": "Byron Buxton",
        "position": "CF",
        "number": 25
      },
      "team": {
        "id": "E8C4E6927B2D",
        "name": "Minnesota Twins"
      },
      "status": "10-Day IL",
      "type": "Hip",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:FBFEEA82AD5C",
      "player": {
        "id": "FBFEEA82AD5C",
        "name": "Hunter Harvey",
        "position": "RP",
        "number": 56
      },
      "team": {
        "id": "E970E2EDDCAE",
        "name": "Kansas City Royals"
      },
      "status": "15-Day IL",
      "type": "Back",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:DA5567D161A5",
      "player": {
        "id": "DA5567D161A5",
        "name": "Josh Sborz",
        "position": "RP",
        "number": 66
      },
      "team": {
        "id": "B85216061897",
        "name": "Texas Rangers"
      },
      "status": "15-Day IL",
      "type": "Shoulder",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:3E128388B174",
      "player": {
        "id": "3E128388B174",
        "name": "Jacob Hurtubise",
        "position": "LF",
        "number": 26
      },
      "team": {
        "id": "F30D0B9894E1",
        "name": "Cincinnati Reds"
      },
      "status": "7-Day IL",
      "type": "Undisclosed",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:46298CDFE8A2",
      "player": {
        "id": "46298CDFE8A2",
        "name": "Zack Littell",
        "position": "SP",
        "number": 52
      },
      "team": {
        "id": "FE07CF8C473A",
        "name": "Tampa Bay Rays"
      },
      "status": "15-Day IL",
      "type": "Shoulder",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:B7E156010093",
      "player": {
        "id": "B7E156010093",
        "name": "Steven Wilson",
        "position": "RP",
        "number": 36
      },
      "team": {
        "id": "97700EF0AC9B",
        "name": "Chicago White Sox"
      },
      "status": "15-Day IL",
      "type": "Back",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    },
    {
      "id": "baseball:mlb:E3676F73BC15",
      "player": {
        "id": "E3676F73BC15",
        "name": "Joey Bart",
        "position": "C",
        "number": 14
      },
      "team": {
        "id": "98CE61698342",
        "name": "Pittsburgh Pirates"
      },
      "status": "10-Day IL",
      "type": "Hamstring",
      "sport": {
        "id": "baseball",
        "name": "Baseball"
      },
      "league": {
        "id": "mlb",
        "name": "MLB"
      }
    }
    // ... additional injury records continue with same structure
  ]
}
```

## Response Structure

Each injury record in the `data` array contains the following fields:

### Root Level Fields
- **`id`** (string): Unique identifier for the injury record in format `sport:league:playerID`
- **`status`** (string): Current injury status (e.g., "Day-To-Day", "10-Day IL", "15-Day IL", "60-Day IL", "Out", "Paternity", "Suspension")
- **`type`** (string): Type/description of the injury or reason for absence (e.g., "Illness", "Knee", "Hip", "Back", "Personal", "Suspension")

### Nested Objects

#### `player` Object
- **`id`** (string): Unique player identifier
- **`name`** (string): Player's full name
- **`position`** (string | null): Player's position abbreviation (e.g., "SP", "RP", "CF", "1B", "SS", "C")
- **`number`** (number | null): Player's jersey number

#### `team` Object
- **`id`** (string): Unique team identifier
- **`name`** (string): Full team name

#### `sport` Object
- **`id`** (string): Sport identifier (e.g., "baseball")
- **`name`** (string): Sport display name (e.g., "Baseball")

#### `league` Object
- **`id`** (string): League identifier (e.g., "mlb")
- **`name`** (string): League display name (e.g., "MLB")

## Status Types

The API returns various injury statuses including:
- **Day-To-Day**: Short-term injury, status evaluated daily
- **7-Day IL**: Injured List for 7 days (minor league)
- **10-Day IL**: Injured List for minimum 10 days
- **15-Day IL**: Injured List for minimum 15 days
- **60-Day IL**: Injured List for minimum 60 days
- **Out**: General absence status
- **Paternity**: Paternity leave
- **Suspension**: Player suspended

## Injury Types

Common injury types include:
- Physical injuries: "Knee", "Hip", "Back", "Shoulder", "Elbow", "Hamstring", "Wrist", "Ankle", "Oblique", "Finger", "Hand", "Foot", "Calf", "Biceps", "Lat", "Forearm", "Thigh", etc.
- Other reasons: "Illness", "Personal", "Suspension", "Undisclosed"