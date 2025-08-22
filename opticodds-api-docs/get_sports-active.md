# API Documentation - Get Sports with Available Fixtures

## Description

This API endpoint returns a comprehensive list of all the sports that currently have fixtures with odds available. The endpoint provides detailed information about each sport including unique identifiers, display names, and the main betting markets available for each sport. This is particularly useful for understanding which sports are currently active and what types of betting opportunities are available for each sport category.

The response includes both string-based and numerical identifiers for each sport, allowing for flexible integration with different systems that may use either identifier format. Additionally, the endpoint provides information about the primary betting markets available for each sport, including market identifiers and display names, which can be used to understand the betting options available for each sport type.

## Response Structure

The API returns a JSON object containing a `data` array that holds comprehensive information about each available sport. Each sport object in the array contains detailed information about the sport itself as well as its associated betting markets.

### Root Response Object

| Field | Type | Description |
|-------|------|-------------|
| `data` | Array | An array containing sport objects that represent all sports currently having fixtures with available odds |

### Sport Object Structure

Each sport object within the `data` array contains the following comprehensive information:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | A unique string identifier for the sport, typically using lowercase letters and underscores for separation (e.g., "aussie_rules", "baseball", "basketball") |
| `name` | String | The human-readable display name of the sport as it should appear in user interfaces (e.g., "Aussie Rules", "Baseball", "Basketball") |
| `numerical_id` | Number | A unique numerical identifier assigned to the sport for systems that prefer or require integer-based identification |
| `main_markets` | Array | An array of market objects representing the primary betting markets available for this specific sport |

### Market Object Structure

Each market object within the `main_markets` array contains detailed information about betting markets:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | A unique string identifier for the betting market type (e.g., "moneyline", "point_spread", "total_points", "run_line", "total_runs") |
| `name` | String | The human-readable display name of the betting market as it should appear in user interfaces (e.g., "Moneyline", "Point Spread", "Total Points") |
| `numerical_id` | Number | A unique numerical identifier assigned to the betting market for systems that prefer or require integer-based identification |

## Example Response

**Important Note:** The following example is provided solely to demonstrate the JSON response format structure. The actual data returned by the API may differ significantly from this example, including different sports, different market configurations, and different numerical identifiers based on current fixture availability and system configuration.

```json
{
  "data": [
    {
      "id": "aussie_rules",
      "name": "Aussie Rules",
      "numerical_id": 2,
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
      "numerical_id": 3,
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
      "numerical_id": 4,
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
    }
  ]
}
```

## Market Types Explanation

Based on the example response, several common betting market types are represented:

### Moneyline Markets
- **Description**: Straight win/lose bets where you pick which team or participant will win the event outright
- **Availability**: Available across multiple sports as shown in the example (Aussie Rules, Baseball, Basketball)
- **Numerical ID**: 953 in the example (may vary in actual responses)

### Point Spread Markets
- **Description**: Betting on the margin of victory, where points are added or subtracted from the final score
- **Availability**: Common in sports like Aussie Rules and Basketball
- **Numerical ID**: 1172 in the example (may vary in actual responses)

### Total Points/Runs Markets
- **Description**: Over/under betting on the total combined score of both teams
- **Sport-Specific Variations**: 
  - "Total Points" for sports like Aussie Rules and Basketball
  - "Total Runs" for Baseball
- **Numerical IDs**: 1358 for Total Points, 1367 for Total Runs in the example (may vary in actual responses)

### Run Line Markets
- **Description**: Baseball-specific point spread betting, typically involving a 1.5 run spread
- **Availability**: Specific to Baseball as shown in the example
- **Numerical ID**: 1245 in the example (may vary in actual responses)

## Data Considerations

### Dynamic Nature of Data
The data returned by this endpoint is dynamic and reflects the current state of available fixtures and odds. Sports and their associated markets may appear or disappear from the response based on:
- Seasonal availability of sports
- Current fixture schedules
- Availability of odds from bookmakers
- System maintenance and updates

### Identifier Usage
The endpoint provides both string and numerical identifiers for maximum flexibility:
- **String IDs**: Recommended for human-readable applications and debugging
- **Numerical IDs**: Suitable for systems requiring integer-based identification or database optimization

### Market Availability
The `main_markets` array represents the primary betting markets available for each sport, but additional markets may be available through other API endpoints. The markets shown represent the most commonly used betting types for each sport category.