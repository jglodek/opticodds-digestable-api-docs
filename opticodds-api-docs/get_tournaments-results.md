# Tournament Results API Documentation

## Description

Returns tournament results, this can apply at different stages.

## Endpoint

```
GET /api/v3/tournaments/results
```

## Parameters

### Required Parameters

- **tournament_id**: The unique identifier for the tournament

### Optional Parameters

#### stage
Must be one of the following values:
- `rounds` - Returns results for specific rounds
- `playoff` - Returns playoff results
- `summary` - Returns tournament summary with final results

#### round_number
For golf tournaments, this parameter only applies when `stage=rounds`. Must be one of the following values:
- `1` - First round
- `2` - Second round  
- `3` - Third round
- `4` - Fourth round

## Example Request

### Golf Tournament Summary
```
GET https://api.opticodds.com/api/v3/tournaments/results?tournament_id=0D9C9CCC70BF&stage=summary
```

## Response Format

The API returns a comprehensive JSON response containing detailed tournament information and results.

### Response Structure

```json
{
  "data": [
    {
      "id": "string",
      "sport": {
        "id": "string",
        "name": "string"
      },
      "league": {
        "id": "string", 
        "name": "string"
      },
      "tournament": {
        "id": "string",
        "name": "string",
        "start_date": "ISO 8601 datetime string",
        "end_date": "ISO 8601 datetime string",
        "status": "string",
        "season_year": "string",
        "venue_name": "string",
        "venue_location": "string"
      },
      "leaderboard": [
        {
          "tied": "boolean",
          "score": "number or null",
          "rounds": [
            {
              "pars": "number",
              "thru": "number", 
              "score": "number",
              "bogeys": "number",
              "eagles": "number",
              "birdies": "number",
              "strokes": "number",
              "sequence": "number",
              "holes_in_one": "number",
              "other_scores": "number",
              "double_bogeys": "number", 
              "double_eagles": "number",
              "triple_bogeys_or_worse": "number"
            }
          ],
          "playoffs": "null or object",
          "position": "number",
          "player_id": "string",
          "player_name": "string",
          "player_status": "string or null"
        }
      ],
      "round": "null or number"
    }
  ]
}
```

### Field Descriptions

#### Tournament Object
- **id**: Unique tournament identifier
- **name**: Full tournament name
- **start_date**: Tournament start date and time in ISO 8601 format
- **end_date**: Tournament end date and time in ISO 8601 format  
- **status**: Current tournament status (e.g., "completed", "in_progress")
- **season_year**: Year of the tournament season
- **venue_name**: Name of the tournament venue
- **venue_location**: Geographic location of the venue

#### Leaderboard Object
- **tied**: Boolean indicating if the player is tied for their position
- **score**: Player's total tournament score relative to par (null for withdrawn players)
- **position**: Player's finishing position in the tournament
- **player_id**: Unique player identifier
- **player_name**: Full player name
- **player_status**: Player status (e.g., "withdrawn", null for active)
- **playoffs**: Playoff information (null if no playoffs occurred)

#### Round Object (for Golf)
- **pars**: Number of holes completed at par
- **thru**: Number of holes completed in the round
- **score**: Round score relative to par
- **bogeys**: Number of bogeys in the round
- **eagles**: Number of eagles in the round
- **birdies**: Number of birdies in the round
- **strokes**: Total strokes taken in the round
- **sequence**: Round number (1, 2, 3, 4)
- **holes_in_one**: Number of holes-in-one
- **other_scores**: Number of other miscellaneous scores
- **double_bogeys**: Number of double bogeys
- **double_eagles**: Number of double eagles (albatrosses)
- **triple_bogeys_or_worse**: Number of triple bogeys or worse scores

## Example Response

```json
{
  "data": [
    {
      "id": "golf_pga_0d9c9ccc70bf_summary",
      "sport": {
        "id": "golf",
        "name": "Golf"
      },
      "league": {
        "id": "pga", 
        "name": "PGA"
      },
      "tournament": {
        "id": "0D9C9CCC70BF",
        "name": "BMW Championship 2024",
        "start_date": "2024-08-22T00:00:00Z",
        "end_date": "2024-08-26T04:00:00Z", 
        "status": "completed",
        "season_year": "2024",
        "venue_name": "Castle Pines Golf Club",
        "venue_location": "Castle Rock, Colorado, USA"
      },
      "leaderboard": [
        {
          "tied": false,
          "score": -12,
          "rounds": [
            {
              "pars": 12,
              "thru": 18,
              "score": -6,
              "bogeys": 0,
              "eagles": 0, 
              "birdies": 6,
              "strokes": 66,
              "sequence": 1,
              "holes_in_one": 0,
              "other_scores": 0,
              "double_bogeys": 0,
              "double_eagles": 0,
              "triple_bogeys_or_worse": 0
            }
          ],
          "playoffs": null,
          "position": 1,
          "player_id": "B3CB24E6BED3", 
          "player_name": "Keegan Bradley",
          "player_status": null
        }
      ],
      "round": null
    }
  ]
}
```

## Notes

- For withdrawn players, the `score` field will be `null` and `player_status` will be `"withdrawn"`
- The `tied` field indicates whether multiple players share the same position
- Round data provides comprehensive scoring statistics for each round of play
- Tournament status values include "completed", "in_progress", and others depending on current state
- All datetime fields follow ISO 8601 format (YYYY-MM-DDTHH:MM:SSZ)