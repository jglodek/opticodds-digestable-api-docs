# OpticOdds API - Markets Settleable Endpoint

## API Endpoint Overview

This endpoint returns a comprehensive list of all markets that can have settlement functionality available for specified leagues within the OpticOdds API system.

## Base Endpoint Information

**HTTP Method:** GET  
**Base URL:** `https://api.opticodds.com/api/v3/markets/settleable`  
**API Version:** v3

## Functionality Description

The Markets Settleable endpoint serves as a comprehensive resource for retrieving all available betting market types that support settlement operations for any given league or leagues. This endpoint is particularly valuable for developers and integrators who need to understand which betting markets can be settled within their applications, allowing for proper bet resolution and payout calculations.

The endpoint accepts league parameters and returns detailed information about each available market, including both human-readable names and numerical identifiers that can be used in subsequent API calls. This functionality is essential for building comprehensive sports betting applications that need to handle multiple market types across different sports and leagues.

## Query Parameters

### Required Parameters
- **league**: The league identifier for which to retrieve settleable markets
  - **Type:** String
  - **Example:** `NBA`
  - **Description:** Specifies the sports league for which to return available settleable markets

### Parameter Usage Notes
The documentation indicates that for a complete list of all available parameters, users should scroll to the bottom of the original documentation page. This suggests additional optional parameters may be available for filtering, sorting, or modifying the response format.

## Response Structure

### Root Response Object
The API returns a JSON object with the following top-level structure:

```json
{
  "data": [
    // Array of league objects containing market information
  ]
}
```

### League Object Structure
Each element in the `data` array contains detailed league information:

```json
{
  "league": {
    "id": "string",           // League identifier (lowercase)
    "name": "string",         // Full league name
    "numerical_id": integer   // Numerical league identifier
  },
  "markets": [
    // Array of market objects
  ]
}
```

### Market Object Structure
Each market object within the `markets` array contains:

```json
{
  "id": "string",           // Unique market identifier (snake_case)
  "name": "string",         // Human-readable market name
  "numerical_id": integer   // Numerical market identifier
}
```

## Example Request

```
GET https://api.opticodds.com/api/v3/markets/settleable?league=NBA
```

## Detailed Example Response

The following example demonstrates the comprehensive response structure when requesting NBA league markets:

```json
{
  "data": [
    {
      "league": {
        "id": "nba",
        "name": "NBA",
        "numerical_id": 355
      },
      "markets": [
        {
          "id": "1st_3_quarters_moneyline",
          "name": "1st 3 Quarters Moneyline",
          "numerical_id": 43
        },
        {
          "id": "1st_3_quarters_moneyline_3-way",
          "name": "1st 3 Quarters Moneyline 3-Way",
          "numerical_id": 44
        },
        {
          "id": "1st_3_quarters_point_spread",
          "name": "1st 3 Quarters Point Spread",
          "numerical_id": 45
        }
        // ... additional markets continue
      ]
    }
  ]
}
```

## Comprehensive Market Types Available

The NBA example response includes an extensive variety of market types, demonstrating the depth of betting options available through the OpticOdds platform:

### Game Period Markets
- **First Three Quarters:** Moneyline, 3-way moneyline, point spread, total points
- **Halves (1st/2nd):** Moneyline, 3-way moneyline, point spread, team totals, total points, correct score, double chance, draw no bet
- **Quarters (1st/2nd/3rd/4th):** Moneyline, 3-way moneyline, point spread, team totals, total points, including overtime variations for 4th quarter

### Full Game Markets
- **Primary Markets:** Moneyline, 3-way moneyline, point spread, team totals, total points
- **Alternative Markets:** Correct score, double chance, draw no bet, halftime/fulltime combinations
- **Special Markets:** First team to score, overtime occurrence

### Player Proposition Markets
The API supports extensive player-specific betting markets including:
- **Scoring:** Points, field goals made/attempted, free throws made/attempted, three-pointers attempted, two-pointers made/attempted
- **Rebounding:** Total rebounds, offensive rebounds, defensive rebounds
- **Playmaking:** Assists, turnovers
- **Defense:** Steals, blocks, personal fouls
- **Combination Stats:** Points + assists, points + rebounds, points + rebounds + assists, rebounds + assists, steals + blocks
- **Achievement Markets:** Double-double, triple-double

### Team Statistics Markets
- **Team Totals:** Points, assists, rebounds, steals, blocks, made three-pointers
- **Special Team Markets:** Consecutive points, odd/even scoring variations

### Market Variations and Modifiers
Many markets include additional variations such as:
- **3-way betting:** Including tie/draw options
- **Odd/Even:** For various statistical categories
- **Overtime inclusion:** Specific markets that include or exclude overtime periods
- **Regulation time:** Markets that settle on regulation time only

## Technical Implementation Considerations

### Numerical IDs vs String IDs
The API provides both string-based identifiers (human-readable) and numerical identifiers for each market. This dual-identifier system allows for:
- **String IDs:** Better readability and easier debugging during development
- **Numerical IDs:** More efficient storage and processing in database systems and API calls

### Market Availability
The markets returned by this endpoint represent all possible markets that **can** have settlement available for the specified league. This doesn't guarantee that every market will be available for every game, as market availability can depend on various factors including:
- Sportsbook coverage
- Game importance and popularity
- Data availability for settlement
- League-specific betting regulations

### Integration Workflow
A typical integration workflow would involve:
1. Calling this endpoint to understand available markets for a league
2. Using the returned market IDs in subsequent API calls to retrieve odds, place bets, or check settlement status
3. Implementing proper error handling for markets that may not be available for specific games

## Data Freshness and Accuracy

### Example Response Disclaimer
The documentation explicitly states that the example JSON response is "ONLY USED TO SHOW AN EXAMPLE JSON FORMAT, DATA CAN BE DIFFERENT FROM ACTUAL RESPONSE." This indicates that:
- The actual markets available may vary over time
- New markets may be added to the platform
- Some markets may be deprecated or temporarily unavailable
- Real-world responses should always be validated against current API responses

### Best Practices for Implementation
- Implement dynamic market handling rather than hardcoding market lists
- Regularly refresh market availability data
- Handle cases where expected markets may not be available
- Use both string and numerical identifiers for robust market identification
- Implement proper error handling for deprecated or unavailable markets

This comprehensive endpoint serves as the foundation for understanding betting market availability within the OpticOdds ecosystem, enabling developers to build robust, feature-rich sports betting applications that can handle the full spectrum of available betting options.