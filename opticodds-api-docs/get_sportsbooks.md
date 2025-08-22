# OpticOdds Sportsbooks API v3

## Endpoint Overview

The OpticOdds Sportsbooks API v3 provides comprehensive access to a complete list of all sportsbooks that are currently supported or have been previously supported by the OpticOdds platform. This endpoint serves as a central directory for sportsbook information and their current operational status.

## Endpoint Details

### Base URL
```
GET https://api.opticodds.com/api/v3/sportsbooks
```

### HTTP Method
`GET`

### Authentication
This endpoint appears to be publicly accessible and does not require authentication parameters based on the provided information.

### Request Parameters
This endpoint does not require any query parameters or request body parameters.

## Response Structure

### Response Format
The API returns data in JSON format with the following structure:

```json
{
  "data": [
    // Array of sportsbook objects
  ]
}
```

### Sportsbook Object Properties

Each sportsbook object in the response contains the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | Unique identifier for the sportsbook, used for API references |
| `name` | String | Display name of the sportsbook |
| `logo` | String | URL to the sportsbook's logo image hosted on OpticOdds CDN |
| `is_onshore` | Boolean | Indicates whether the sportsbook operates onshore (within regulated jurisdictions) |
| `is_active` | Boolean | **Critical field** - Indicates whether the sportsbook currently has odds available and is actively supported |

### Key Field Explanation

The `is_active` field is particularly important as mentioned in the description. This boolean value allows developers to:
- Filter for currently active sportsbooks (`is_active: true`)
- Identify deprecated or discontinued sportsbooks (`is_active: false`)
- Determine which sportsbooks are likely to have current odds data available

## Sportsbook Categories

The response includes various types of sportsbooks:

### Traditional Sportsbooks
- Major operators like DraftKings, BetMGM, Caesars, FanDuel (ESPN BET)
- Regional operators with state-specific variants (e.g., "Caesars (Colorado)", "BetRivers (New York)")
- International operators like bet365, Betway, William Hill

### Fantasy Sports Platforms
- Daily Fantasy Sports (DFS) platforms like PrizePicks, Underdog Fantasy
- Pick-style games with specific variants (e.g., "PrizePicks (5 or 6 Pick Flex)")

### Exchange and Alternative Betting
- Betting exchanges like Betfair Exchange
- Peer-to-peer betting platforms
- Specialized betting platforms

### Geographic Variants
Many sportsbooks have location-specific implementations:
- State-specific variants (e.g., "Hard Rock (Arizona)", "Caesars (Nevada)")
- Country-specific variants (e.g., "TAB (New Zealand)", "Unibet (Australia)")
- Regional regulatory compliance versions

## Response Data Examples

### Active Sportsbook Example
```json
{
  "id": "draftkings",
  "name": "DraftKings",
  "logo": "https://cdn.opticodds.com/sportsbook-logos/draftkings.jpg",
  "is_onshore": true,
  "is_active": true
}
```

### Inactive Sportsbook Example
```json
{
  "id": "fox_bet",
  "name": "FOX Bet",
  "logo": "https://cdn.opticodds.com/sportsbook-logos/foxbet.jpg",
  "is_onshore": true,
  "is_active": false
}
```

### Offshore Sportsbook Example
```json
{
  "id": "pinnacle",
  "name": "Pinnacle",
  "logo": "https://cdn.opticodds.com/sportsbook-logos/pinnacle.jpg",
  "is_onshore": false,
  "is_active": true
}
```

## Implementation Notes

### Status Filtering
Developers should implement filtering based on the `is_active` field:
- Use `is_active: true` sportsbooks for current odds requests
- `is_active: false` sportsbooks may represent discontinued services or temporarily unavailable operators

### Logo Assets
All logo URLs point to the OpticOdds CDN (`https://cdn.opticodds.com/sportsbook-logos/`) and are provided in JPG, PNG, or JPEG formats. These are optimized for web display and can be used directly in applications.

### ID Usage
The `id` field values are used throughout other OpticOdds API endpoints to specify which sportsbook's odds you want to retrieve. These IDs are:
- URL-safe and lowercase
- Use underscores for spaces
- Include descriptive suffixes for variants (e.g., `_canada_`, `_ohio_`)

### Regulatory Considerations
The `is_onshore` field helps identify:
- **Onshore** (`true`): Licensed and regulated within specific jurisdictions
- **Offshore** (`false`): Operating outside traditional regulatory frameworks

## Rate Limiting and Usage

Based on the endpoint structure, this appears to be a reference endpoint that would typically have:
- Lower rate limits due to relatively static data
- Caching recommended for client applications
- Updates reflecting new sportsbook partnerships or status changes

## Error Handling

Standard HTTP status codes apply:
- `200 OK`: Successful response with sportsbook data
- `429 Too Many Requests`: Rate limit exceeded
- `500 Internal Server Error`: Server-side issues

## Integration Examples

### Filtering Active Sportsbooks
```javascript
const activeSportsbooks = response.data.filter(book => book.is_active === true);
```

### Separating Onshore vs Offshore
```javascript
const onshoreSportsbooks = response.data.filter(book => book.is_onshore === true);
const offshoreSportsbooks = response.data.filter(book => book.is_onshore === false);
```

### Creating a Sportsbook Lookup Map
```javascript
const sportsbookMap = response.data.reduce((map, book) => {
  map[book.id] = book;
  return map;
}, {});
```

This comprehensive endpoint serves as the foundation for understanding which sportsbooks are available in the OpticOdds ecosystem and their current operational status, making it essential for any application integration with the OpticOdds platform.