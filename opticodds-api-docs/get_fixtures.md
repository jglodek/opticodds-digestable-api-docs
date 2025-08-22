# Get Fixtures API Endpoint

## Overview

The Get Fixtures API endpoint provides a comprehensive, paginated list of all fixtures within the OpticOdds platform. This endpoint supports extensive retrieval capabilities, accommodating all fixtures from historical data that may or may not have ever had associated odds, as well as all fixtures that are scheduled for future events.

**Base URL:** `https://api.opticodds.com/api/v3/fixtures`

**HTTP Method:** `GET`

**Default Behavior:** If no date parameters (`start_date`, `start_date_before`, `start_date_after`) are provided, the endpoint automatically defaults to returning fixtures from 3 days ago.

## Endpoint Description

This endpoint delivers a complete fixture management solution, enabling users to retrieve detailed information about sports fixtures across various time periods and filtering criteria. The API supports both historical and future fixtures, providing comprehensive data that includes team information, scheduling details, venue information, scores, lineups, and various metadata associated with each fixture.

The endpoint implements intelligent date handling, ensuring that users always receive relevant fixture data even when specific date parameters are not provided. This makes it particularly useful for applications that need to display recent fixture information by default.

For detailed information about fixture status values and their meanings throughout the fixture lifecycle, users are directed to consult the Fixtures Lifecycle Documentation, which provides comprehensive explanations of various status states and their implications.

## Required Parameters

**Important:** You must pass at least one of the following parameters to successfully query the endpoint:

- `sport` - The sport identifier (ID or name)
- `league` - The league identifier (ID or name)  
- `id` - Specific fixture ID
- `team_id` - Specific team identifier

## Parameter Details

### Core Filtering Parameters

#### `sport`
- **Type:** String
- **Description:** Specifies the sport you want to retrieve fixtures for
- **Format:** Can accept either the sport ID or the sport name
- **Required:** One of `sport`, `league`, `id`, or `team_id` must be provided
- **Example:** `sport=football` or `sport=9`

#### `league`  
- **Type:** String
- **Description:** Specifies the league you want to retrieve fixtures for
- **Format:** Can accept either the league ID or the league name
- **Required:** One of `sport`, `league`, `id`, or `team_id` must be provided
- **Example:** `league=NFL` or `league=england_-_premier_league`

#### `id`
- **Type:** String
- **Description:** Specific fixture ID for retrieving individual fixture data
- **Required:** One of `sport`, `league`, `id`, or `team_id` must be provided

#### `team_id`
- **Type:** String  
- **Description:** Specific team identifier for retrieving fixtures involving a particular team
- **Required:** One of `sport`, `league`, `id`, or `team_id` must be provided

### Date Filtering Parameters

#### `start_date_after`
- **Type:** String (ISO 8601 DateTime)
- **Description:** Retrieve all fixtures that start after the specified date and time
- **Format:** ISO 8601 datetime format (YYYY-MM-DDTHH:MM:SSZ) recommended for optimal results
- **Alternative Format:** YYYY-MM-DD (defaults to anything starting after the completion of the specified date)
- **Example:** `start_date_after=2024-10-21T00:00:00Z` or `start_date_after=2024-10-21`
- **Default Behavior:** When no date parameters are provided, defaults to 3 days ago

#### `start_date_before`
- **Type:** String (ISO 8601 DateTime)
- **Description:** Retrieve all fixtures that start before the specified date and time
- **Format:** ISO 8601 datetime format (YYYY-MM-DDTHH:MM:SSZ) recommended for optimal results
- **Example:** `start_date_before=2024-10-21T23:59:59Z`

#### `start_date`
- **Type:** String (ISO 8601 DateTime)
- **Description:** Retrieve all fixtures that start on a specific date
- **Format:** ISO 8601 datetime format (YYYY-MM-DDTHH:MM:SSZ) recommended for optimal results
- **Alternative Format:** YYYY-MM-DD (returns games that start on that date in EST timezone)
- **Example:** `start_date=2024-10-21T00:00:00Z` or `start_date=2024-10-21`

### Enhanced Data Parameters

#### `include_starting_lineups`
- **Type:** Boolean
- **Default:** `false`
- **Description:** Controls whether starting lineup information is included in the response
- **Supported Leagues:** Available for various leagues that the platform supports
- **Impact:** When enabled, the `lineups` object in the response will contain detailed player information for both home and away teams
- **Example:** `include_starting_lineups=true`

#### `include_statsperform_id`
- **Type:** Boolean
- **Default:** `false`
- **Description:** Controls whether StatsPerform IDs are included in the response data
- **Implementation:** When enabled, StatsPerform IDs are populated in the `source_ids` field of each fixture entry
- **Response Structure:** 
  ```json
  "source_ids": {
    "statsperform_id": "a2nwp4zx1mzcmk2e4dtcw5h5g"
  }
  ```
- **Example:** `include_statsperform_id=true`

## Response Structure

The API returns a comprehensive JSON response containing detailed fixture information structured as follows:

### Root Response Object
- **`data`** (Array): Array of fixture objects containing all requested fixture information
- **`page`** (Integer): Current page number in the paginated response
- **`total_pages`** (Integer): Total number of pages available for the query

### Fixture Object Structure

Each fixture object in the `data` array contains the following comprehensive information:

#### Core Identification Fields
- **`id`** (String): Unique fixture identifier
- **`numerical_id`** (Integer): Numerical fixture identifier  
- **`game_id`** (String): Internal game identification string

#### Scheduling Information
- **`start_date`** (String): ISO 8601 formatted start date and time
- **`status`** (String): Current fixture status (e.g., "unplayed", "completed", "cancelled", "live")
- **`is_live`** (Boolean): Indicates whether the fixture is currently in progress

#### Team Information
- **`home_competitors`** (Array): Array containing home team details
  - **`id`** (String): Team identifier
  - **`name`** (String): Full team name
  - **`numerical_id`** (Integer): Numerical team identifier (may be null)
  - **`abbreviation`** (String): Team abbreviation
  - **`logo`** (String): URL to team logo image

- **`away_competitors`** (Array): Array containing away team details (same structure as home_competitors)

- **`home_team_display`** (String): Display name for home team
- **`away_team_display`** (String): Display name for away team

#### League and Sport Classification
- **`sport`** (Object): Sport classification information
  - **`id`** (String): Sport identifier
  - **`name`** (String): Sport name
  - **`numerical_id`** (Integer): Numerical sport identifier

- **`league`** (Object): League classification information
  - **`id`** (String): League identifier  
  - **`name`** (String): League name
  - **`numerical_id`** (Integer): Numerical league identifier

#### Team-Specific Metadata
- **`home_starter`** (String/null): Starting pitcher or key player for home team
- **`home_record`** (String/null): Home team's current record
- **`home_seed`** (Integer/null): Home team's tournament seed
- **`home_rotation_number`** (Integer/null): Betting rotation number for home team

- **`away_starter`** (String/null): Starting pitcher or key player for away team
- **`away_record`** (String/null): Away team's current record  
- **`away_seed`** (Integer/null): Away team's tournament seed
- **`away_rotation_number`** (Integer/null): Betting rotation number for away team

#### Tournament and Competition Information
- **`tournament`** (String/null): Tournament name if applicable
- **`tournament_stage`** (String/null): Current tournament stage

#### Venue Information
- **`venue_name`** (String/null): Name of the venue where the fixture is played
- **`venue_location`** (String/null): Geographic location of the venue
- **`venue_neutral`** (Boolean): Indicates if the venue is neutral (not home for either team)

#### Media and Broadcasting
- **`broadcast`** (String/null): Broadcasting information and networks

#### Betting and Odds Information
- **`has_odds`** (Boolean): Indicates whether odds are available for this fixture

#### Results and Scoring (for completed fixtures)
- **`result`** (Object/null): Contains scoring and result information when available
  - **`scores`** (Object): Detailed scoring information
    - **`home`** (Object): Home team scoring
      - **`total`** (Integer): Total final score
      - **`periods`** (Object): Period-by-period scoring breakdown
      - **`aggregate`** (Integer/null): Aggregate score for multi-leg competitions
    - **`away`** (Object): Away team scoring (same structure as home)
  - **`in_play_data`** (Object): Live game information
    - **`period`** (String): Current period/quarter
    - **`clock`** (String/null): Game clock information
    - **`last_play`** (String/null): Description of last significant play

#### Player Lineup Information
- **`lineups`** (Object): Player lineup information (when `include_starting_lineups=true`)
  - **`home`** (Array): Array of home team player objects
  - **`away`** (Array): Array of away team player objects

Each player object contains:
- **`player_id`** (String): Unique player identifier
- **`player_name`** (String): Player's full name
- **`player_team`** (String): Team identifier the player belongs to
- **`player_position`** (String): Player's position
- **`player_batting_throwing`** (String/null): Batting/throwing preference (relevant for baseball)
- **`is_substitute`** (Boolean): Indicates if player is a substitute

#### Season and Scheduling Context
- **`season_type`** (String): Type of season (e.g., "Regular Season", "Playoffs")
- **`season_year`** (String): Season year
- **`season_week`** (String/null): Week number within the season

#### Environmental Conditions
- **`weather`** (String/null): Weather conditions description
- **`weather_temp`** (String/null): Temperature information

#### External Data Integration
- **`source_ids`** (Object): External system identifiers (when `include_statsperform_id=true`)
  - **`statsperform_id`** (String): StatsPerform system identifier

## Example API Calls

### NFL Fixtures Example
**URL:** `https://api.opticodds.com/api/v3/fixtures?league=NFL`

This example demonstrates retrieving NFL fixtures, showing various fixture statuses including cancelled, unplayed, and completed games with comprehensive metadata.

### Premier League with Lineups Example  
**URL:** `https://api.opticodds.com/api/v3/fixtures?league=England%20-%20Premier%20League&start_date_after=2025-01-14&start_date_before=2025-01-15&include_starting_lineups=True`

This example shows Premier League fixtures with detailed starting lineup information, demonstrating the enhanced data available when `include_starting_lineups=true`.

## Usage Notes

1. **Date Parameter Flexibility:** The API accepts both full ISO 8601 datetime strings and simplified YYYY-MM-DD date formats, with intelligent defaults applied for optimal usability.

2. **Pagination Support:** All responses include pagination information (`page` and `total_pages`) to help manage large result sets effectively.

3. **Status Lifecycle:** Fixture status values follow a comprehensive lifecycle from scheduling through completion. Refer to the Fixtures Lifecycle Documentation for detailed explanations.

4. **Historical and Future Data:** The endpoint supports both historical fixture retrieval and future fixture scheduling information, making it suitable for comprehensive sports data applications.

5. **League and Sport Flexibility:** Both league and sport parameters accept either ID or name formats, providing flexibility in query construction.

6. **Optional Enhanced Data:** Lineup and StatsPerform ID inclusion are optional features that can be enabled based on specific application requirements, allowing for optimized response sizes when enhanced data is not needed.