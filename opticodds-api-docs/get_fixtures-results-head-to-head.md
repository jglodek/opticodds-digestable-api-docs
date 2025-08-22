# OpticOdds API - Head-to-Head Fixture Results Endpoint

## Endpoint Overview

This API endpoint returns a comprehensive list of fixture results for the last fixtures played between two specified teams, providing detailed head-to-head historical match data with complete game statistics, scores, and metadata.

## Endpoint Details

**HTTP Method:** GET  
**Base URL:** `https://api.opticodds.com/api/v3/fixtures/results/head-to-head`  
**Content Type:** `application/json`

### Required Query Parameters

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `team1_id` | String | Unique identifier for the first team | `5045D954DFF8` |
| `team2_id` | String | Unique identifier for the second team | `98CE61698342` |

### Example Request URL

```
https://api.opticodds.com/api/v3/fixtures/results/head-to-head?team1_id=5045D954DFF8&team2_id=98CE61698342
```

## Response Structure

The API returns a JSON object containing a `data` array with detailed fixture result objects. Each fixture result contains comprehensive information about completed games between the specified teams.

### Root Response Object

| Field | Type | Description |
|-------|------|-------------|
| `data` | Array | Array of fixture result objects containing head-to-head match data |

### Fixture Result Object Structure

Each object in the `data` array contains the following detailed structure:

#### Sport Information

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `sport.id` | String | Unique identifier for the sport | `"baseball"` |
| `sport.name` | String | Display name of the sport | `"Baseball"` |

#### League Information

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `league.id` | String | Unique identifier for the league | `"mlb"` |
| `league.name` | String | Display name of the league | `"MLB"` |

#### Fixture Details

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `fixture.id` | String | Unique identifier for the specific fixture | `"24E371425A5F"` |
| `fixture.game_id` | String | Composite game identifier with team and date information | `"40548-36707-2024-08-28-09"` |
| `fixture.start_date` | String (ISO 8601) | UTC timestamp of when the fixture started | `"2024-08-28T16:35:00Z"` |
| `fixture.home_team_display` | String | Display name for the home team | `"Pittsburgh Pirates"` |
| `fixture.away_team_display` | String | Display name for the away team | `"Chicago Cubs"` |
| `fixture.status` | String | Current status of the fixture | `"completed"` |
| `fixture.is_live` | Boolean | Indicates whether the fixture is currently live | `true`/`false` |

#### Home and Away Competitors

Both `fixture.home_competitors` and `fixture.away_competitors` are arrays containing competitor objects:

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | String | Unique identifier for the team | `"98CE61698342"` |
| `name` | String | Full team name | `"Pittsburgh Pirates"` |
| `abbreviation` | String | Team abbreviation/code | `"PIT"` |
| `logo` | String (URL) | URL to the team's logo image | `"https://a.espncdn.com/i/teamlogos/mlb/500/pit.png"` |

#### Score Information

The `scores` object contains detailed scoring data for both teams:

##### Home and Away Score Objects

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `total` | Integer | Final total score for the team | `10` |
| `aggregate` | Integer/null | Aggregate score (typically null for single games) | `null` |

##### Periods Object

The `periods` object contains period-by-period scoring:

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `period_1` through `period_9` | Integer | Score for each period/inning | `1`, `5`, `0`, etc. |

#### In-Play Game State

The `in_play` object provides real-time or final game state information:

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `period` | String | Current or final period | `"9"` |
| `clock` | String/null | Current clock state | `"Bottom"`/`null` |
| `last_play` | String/null | Description of the last play | `null` |
| `time_min` | Integer/null | Minutes remaining in current period | `null` |
| `time_sec` | Integer/null | Seconds remaining in current period | `null` |
| `balls` | Integer/null | Current ball count (baseball specific) | `0` |
| `outs` | Integer/null | Current out count (baseball specific) | `3` |
| `strikes` | Integer/null | Current strike count (baseball specific) | `0` |
| `runners` | String/null | Current base runner situation | `null` |
| `batter` | String/null | Current batter information | `null` |
| `pitcher` | String/null | Current pitcher information | `null` |
| `possession` | String/null | Team with current possession | `null` |
| `down` | Integer/null | Current down (football specific) | `null` |
| `distance_to_go` | Integer/null | Yards to go for first down (football specific) | `null` |

#### Events Array

| Field | Type | Description |
|-------|------|-------------|
| `events` | Array | Array of game events (typically empty in completed games) |

#### Team Statistics

The `stats` object contains comprehensive statistical data for both home and away teams:

##### Statistics Structure

Each team's statistics are contained in an array with period-specific data:

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `period` | String | Period for which statistics apply | `"all"` |

##### Baseball-Specific Statistics

The `stats` object within each period contains sport-specific metrics:

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `rbi` | Integer | Runs batted in | `9` |
| `hits` | Integer | Total hits | `16` |
| `runs` | Integer | Total runs scored | `10` |
| `at_bats` | Integer | Total at-bats | `41` |
| `total_bases` | Integer | Total bases achieved | `26` |
| `double_plays` | Integer | Double plays executed | `1` |
| `triple_plays` | Integer | Triple plays executed | `0` |
| `batting_walks` | Integer | Walks received while batting | `8` |
| `batting_strikeouts` | Integer | Strikeouts while batting | `14` |
| `runners_left_on_base` | Integer | Runners left on base | `14` |
| `scoring_position_successes` | Integer | Successful at-bats with runners in scoring position | `5` |
| `scoring_position_opportunities` | Integer | Total opportunities with runners in scoring position | `19` |

#### Retirement Information

| Field | Type | Description |
|-------|------|-------------|
| `retirement_info` | Object/null | Information about any player retirements (typically null) |

## Response Behavior

- The API returns fixtures in reverse chronological order (most recent first)
- Each fixture represents a completed game between the two specified teams
- Statistical data is comprehensive and includes both offensive and defensive metrics
- All timestamps are provided in UTC format using ISO 8601 standard
- The endpoint provides historical head-to-head data for analytical purposes

## Data Completeness

The response includes:
- Complete game scores with period-by-period breakdowns
- Comprehensive team statistics for each completed fixture
- Team branding information including logos and official names
- Detailed fixture metadata including unique identifiers and timing information
- Real-time or final game state information
- League and sport categorization for proper data organization

This endpoint is particularly valuable for:
- Historical performance analysis between specific teams
- Head-to-head statistical comparisons
- Trend analysis for betting or analytical purposes
- Sports data aggregation and reporting systems
- Fantasy sports applications requiring detailed historical matchup data