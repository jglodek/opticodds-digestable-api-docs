# OpticOdds API - Active Sportsbooks Endpoint

## Description

This API endpoint returns a comprehensive list of all the sportsbooks that currently have odds available in the OpticOdds system. The endpoint provides detailed information about each sportsbook including their identification details, branding information, operational status, and regulatory classification.

## Endpoint Information

**URL:** `https://api.opticodds.com/api/v3/sportsbooks/active`

**HTTP Method:** `GET`

**Content-Type:** `application/json`

## Query Parameters

### Required Parameters
- None specified in the provided documentation

### Optional Parameters
- `league` (string): Filters sportsbooks by specific league (example shows "nba")

## Response Structure

The API returns a JSON response with the following structure:

### Root Response Object
```json
{
   "data": [
      // Array of sportsbook objects
   ]
}
```

### Sportsbook Object Properties

Each sportsbook object in the `data` array contains the following properties:

| Property | Type | Description | Example |
|----------|------|-------------|---------|
| `id` | string | Unique identifier for the sportsbook used internally by the API system | "1xbet", "draftkings", "betmgm" |
| `name` | string | Display name of the sportsbook as it appears to end users | "1XBet", "DraftKings", "BetMGM" |
| `logo` | string | Complete URL path to the sportsbook's logo image hosted on OpticOdds CDN | "https://cdn.opticodds.com/sportsbook-logos/1xbet.jpg" |
| `is_onshore` | boolean | Indicates whether the sportsbook operates under US regulatory jurisdiction and compliance | true, false |
| `is_active` | boolean | Current operational status indicating if the sportsbook is actively providing odds data | true, false |

## Detailed Sportsbook Categories

### Onshore Sportsbooks (is_onshore: true)
These sportsbooks operate under US regulatory compliance and are legally authorized to operate within specific US jurisdictions. Examples include:
- Major US operators: DraftKings, BetMGM, Caesars, FanDuel (Fanatics)
- Regional US operators: BetRivers, Hard Rock, Wind Creek
- State-specific variants: BetRivers (New York), Caesars (Louisiana), Caesars (Pennsylvania), Caesars (Tennessee)

### Offshore Sportsbooks (is_onshore: false)
These sportsbooks operate outside US regulatory jurisdiction and typically serve international markets or US customers through offshore licensing. Examples include:
- International operators: 1XBet, Pinnacle, Bovada, Bodog
- Exchange platforms: Betfair Exchange, Betfair Exchange (Lay)
- Offshore US-facing books: BetOnline, BetUS, MyBookie

### Active vs Inactive Status
- **Active sportsbooks** (`is_active: true`): Currently providing live odds data and operational
- **Inactive sportsbooks** (`is_active: false`): Not currently providing odds data, may be temporarily offline or permanently discontinued

## Special Sportsbook Types

### Fantasy Sports Platforms
The API includes various fantasy sports and pick'em style platforms:
- **PrizePicks**: Standard and Flex variants (5 or 6 Pick Flex)
- **Underdog Fantasy**: Multiple variants including 3 or 5 Pick, 6 Pick, and Sportsbook
- **DraftKings (Pick 6)**: Fantasy pick variant separate from main sportsbook
- **Boom Fantasy (5 Pick Insured)**: Insured pick variant
- **Dabble (3 or 5 Pick)**: Multi-pick fantasy platform
- **Vivid Picks**: Standard and 4 Pick variants
- **Sleeper**: Fantasy platform with sportsbook functionality

### Exchange and Trading Platforms
- **Betfair Exchange**: Peer-to-peer betting exchange with back betting
- **Betfair Exchange (Lay)**: Lay betting functionality on the exchange
- **Sporttrade**: Sports betting exchange platform with Colorado-specific variant

### Regional and Jurisdiction-Specific Variants
Many major sportsbooks have specific variants for different states or regions:
- **BetRivers (New York)**: New York-specific regulatory compliance
- **Caesars (Louisiana, Pennsylvania, Tennessee)**: State-specific implementations
- **Sporttrade (Colorado)**: Colorado-specific variant
- **Ladbrokes (Australia)**: Australian market variant
- **Unibet (Australia, United Kingdom)**: Regional variants for different markets

## Logo Assets

All sportsbook logos are hosted on the OpticOdds CDN at `https://cdn.opticodds.com/sportsbook-logos/` with various file formats including:
- `.jpg` (most common)
- `.png` (for logos requiring transparency)
- `.jpeg` (alternative JPEG format)

Logo filenames typically correspond to simplified versions of the sportsbook names or identifiers.

## Example Request

```
GET https://api.opticodds.com/api/v3/sportsbooks/active?league=nba
```

## Example Response

```json
{
   "data":[
      {
         "id":"1xbet",
         "name":"1XBet",
         "logo":"https://cdn.opticodds.com/sportsbook-logos/1xbet.jpg",
         "is_onshore":false,
         "is_active":true
      },
      {
         "id":"888sport",
         "name":"888sport",
         "logo":"https://cdn.opticodds.com/sportsbook-logos/888sport.jpg",
         "is_onshore":true,
         "is_active":true
      },
      {
         "id":"bally_bet",
         "name":"Bally Bet",
         "logo":"https://cdn.opticodds.com/sportsbook-logos/BallyBet.jpg",
         "is_onshore":true,
         "is_active":true
      }
   ]
}
```

## Notes and Considerations

- The example response provided is for demonstration purposes only and actual data may vary based on real-time sportsbook availability and operational status
- Sportsbook availability may be filtered based on the `league` parameter when specified
- The `is_active` status can change dynamically based on operational conditions, maintenance windows, or business decisions
- Some sportsbooks may appear multiple times with different variants (geographic, product-specific, etc.)
- Logo URLs are subject to change and should not be cached indefinitely
- The API appears to support various programming languages as indicated by the Shell, Node, Ruby, PHP, and Python options mentioned

## Parameter Information Reference

For a complete list of available parameters and their specifications, users are directed to scroll to the bottom of the original documentation page, though these details were not included in the provided content.