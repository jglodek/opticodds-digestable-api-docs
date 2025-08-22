# Teams API Endpoint Documentation

## Overview

This API endpoint provides access to a paginated list of all teams within specified sports and leagues. The endpoint is designed to return comprehensive team information with detailed metadata and identification systems.

## Description

Get a paginated list of all teams. This endpoint will return only **active** teams, so if a team got relegated between seasons, that team will no longer be active for that league.

Team IDs are unique per league, this means that the same team can have different IDs across leagues. For example, **Manchester City FC** has the following IDs:
- `578E2130DC1B`: UEFA - Champions League
- `E69E55FFCF65`: England - Premier League

The `base_id` provides a way to link the same team across leagues, for some sports like **tennis** where we use different providers across leagues this might not be 100% reliable.

If a team is no longer active but you want to get information about it, you can pass in the `id` to this endpoint and it will return data for inactive teams.

## Endpoint URL

```
GET https://api.opticodds.com/api/v3/teams
```

## Required Parameters

**You must pass at least one of the following parameters: `sport`, `league`, or `id`.**

## Parameters

### Core Parameters

#### `sport`
**Type:** String  
**Required:** Conditional (must provide either `sport`, `league`, or `id`)  
**Description:** The sport you want to get fixtures for. You can pass either the sport ID or the sport name.  
**Example:** `football`, `basketball`, `soccer`

#### `league`
**Type:** String  
**Required:** Conditional (must provide either `sport`, `league`, or `id`)  
**Description:** The league you want to get fixtures for. You can pass either the league ID or the league name.  
**Example:** `NFL`, `NBA`, `Premier League`

#### `id`
**Type:** String  
**Required:** Conditional (must provide either `sport`, `league`, or `id`)  
**Description:** The unique identifier of the team you want information for. This parameter allows you to retrieve information about specific teams, including inactive teams.  
**Example:** `AF456B375E7E`

### Optional Parameters

#### `include_statsperform_id`
**Type:** Boolean  
**Required:** No  
**Description:** Specify this parameter if you want the **StatsPerform** IDs to be included as part of the response. If this parameter is enabled, you will see the StatsPerform ID populated in the `source_ids` field of the team entry.

When enabled, the response will include:
```json
"source_ids": {
    "statsperform_id": "a2nwp4zx1mzcmk2e4dtcw5h5g"
}
```

## Response Format

The API returns a JSON response containing a `data` array with team objects. Each team object contains comprehensive information about the team including identification, branding, organizational structure, and league associations.

### Response Structure

```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "numerical_id": null | number,
      "is_active": boolean,
      "city": "string",
      "mascot": "string",
      "nickname": "string",
      "abbreviation": "string",
      "division": "string",
      "conference": "string",
      "base_id": number,
      "logo": "string (URL)",
      "source_ids": {
        "statsperform_id": "string" (optional)
      },
      "sport": {
        "id": "string",
        "name": "string",
        "numerical_id": number
      },
      "league": {
        "id": "string",
        "name": "string",
        "numerical_id": number
      }
    }
  ]
}
```

### Response Fields Description

#### Team-Level Fields

- **`id`** (string): Unique identifier for the team within the specific league
- **`name`** (string): Full official name of the team
- **`numerical_id`** (null | number): Alternative numerical identifier for the team, may be null
- **`is_active`** (boolean): Indicates whether the team is currently active in the league
- **`city`** (string): The city or region the team represents
- **`mascot`** (string): The team's mascot name
- **`nickname`** (string): Common nickname or shortened name for the team
- **`abbreviation`** (string): Standard abbreviation used for the team (typically 2-4 characters)
- **`division`** (string): The division within the league that the team belongs to
- **`conference`** (string): The conference within the league that the team belongs to
- **`base_id`** (number): Universal identifier used to link the same team across different leagues
- **`logo`** (string): URL pointing to the team's official logo image hosted on the OpticOdds CDN
- **`source_ids`** (object): Container for external system identifiers
  - **`statsperform_id`** (string, optional): StatsPerform system identifier, only present when `include_statsperform_id` parameter is enabled

#### Sport Object Fields

- **`sport.id`** (string): Unique identifier for the sport
- **`sport.name`** (string): Display name of the sport
- **`sport.numerical_id`** (number): Numerical identifier for the sport

#### League Object Fields

- **`league.id`** (string): Unique identifier for the league
- **`league.name`** (string): Display name of the league
- **`league.numerical_id`** (number): Numerical identifier for the league

## Example Usage

### Example Request - Get NFL Teams

**URL:** `https://api.opticodds.com/api/v3/teams?league=NFL`

**Method:** GET

### Example Response - NFL Teams

```json
{
  "data": [
    {
      "id": "AF456B375E7E",
      "name": "Arizona Cardinals",
      "numerical_id": null,
      "is_active": true,
      "city": "Arizona",
      "mascot": "Cardinals",
      "nickname": "Cardinals",
      "abbreviation": "ARI",
      "division": "West",
      "conference": "NFC",
      "base_id": 81,
      "logo": "https://cdn.opticodds.com/team-logos/football/81.png",
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      }
    },
    {
      "id": "348C1EE88C42",
      "name": "Atlanta Falcons",
      "numerical_id": null,
      "is_active": true,
      "city": "Atlanta",
      "mascot": "Falcons",
      "nickname": "Falcons",
      "abbreviation": "ATL",
      "division": "South",
      "conference": "NFC",
      "base_id": 82,
      "logo": "https://cdn.opticodds.com/team-logos/football/82.png",
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      }
    },
    {
      "id": "766A226BC204",
      "name": "Baltimore Ravens",
      "numerical_id": null,
      "is_active": true,
      "city": "Baltimore",
      "mascot": "Ravens",
      "nickname": "Ravens",
      "abbreviation": "BAL",
      "division": "North",
      "conference": "AFC",
      "base_id": 83,
      "logo": "https://cdn.opticodds.com/team-logos/football/83.png",
      "source_ids": {},
      "sport": {
        "id": "football",
        "name": "Football",
        "numerical_id": 9
      },
      "league": {
        "id": "nfl",
        "name": "NFL",
        "numerical_id": 367
      }
    }
  ]
}
```

## Important Notes

### Team ID Uniqueness
Team IDs are unique per league, meaning the same physical team will have different IDs when participating in different leagues. The `base_id` field serves as a cross-league identifier to link the same team across different competitions.

### Active vs Inactive Teams
By default, this endpoint returns only active teams. Teams that have been relegated, disbanded, or are otherwise inactive will not appear in the standard response. To retrieve information about inactive teams, you must specifically request them using their `id` parameter.

### StatsPerform Integration
The optional `include_statsperform_id` parameter enables integration with StatsPerform data systems. When enabled, the `source_ids` object will contain the corresponding StatsPerform identifier for enhanced data correlation and third-party integrations.

### League-Specific Data Reliability
For sports like tennis where multiple data providers are used across different leagues, the `base_id` linking mechanism might not be 100% reliable. In such cases, additional verification may be required when correlating teams across leagues.

### Pagination
This endpoint returns paginated results. For complete parameter documentation including pagination controls, refer to the full parameter list at the bottom of the original documentation page.

**Note:** The example response format shown is for demonstration purposes only. Actual API responses may contain different data values while maintaining the same structural format.