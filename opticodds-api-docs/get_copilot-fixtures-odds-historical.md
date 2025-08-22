# Historical Odds API Documentation

## Overview

### Description
This endpoint provides comprehensive access to the complete historical record of odds data for specific betting markets. The historical data encompasses all significant events in an odds lifecycle, including initial odds publication, price fluctuations throughout the betting period, suspension events, market locking mechanisms, and final settlement outcomes. This endpoint is particularly valuable for analyzing betting market behavior, tracking price movements over time, and understanding the complete lifecycle of betting opportunities within the OpticOdds platform.

## Endpoint Information

**Base URL:** `https://api.opticodds.com/api/v3/copilot/fixtures/odds/historical`

**HTTP Method:** `GET`

**Authentication:** Required (authentication method not specified in provided documentation)

## Request Parameters

### Required Parameters

#### `id` (Query Parameter)
- **Type:** String
- **Description:** Unique identifier for the specific odds entry whose historical data is being requested
- **Format:** Composite identifier in the format `{provider_id}:{market_type}:{fixture_id}:{bet_type}:{selection_identifier}`
- **Example:** `96:-1:2025081351A30193:moneyline:kamil_kos`
- **Constraints:** 
  - Maximum of 10 different `id` parameters can be passed in a single request
  - Each `id` must be properly formatted and correspond to an existing odds entry in the system
- **Multiple Values:** Supported - can include multiple `id` parameters in a single request to retrieve historical data for multiple odds simultaneously

### Optional Parameters

#### `odds_format` (Query Parameter)
- **Type:** String (Enum)
- **Description:** Specifies the numerical format in which odds prices should be returned in the response
- **Default Value:** `AMERICAN`
- **Accepted Values:**
  - `AMERICAN` - American odds format (e.g., +150, -110)
  - `DECIMAL` - Decimal odds format (e.g., 2.50, 1.91)
  - `PROBABILITY` - Probability format as percentage (e.g., 40%, 52.38%)
  - `MALAY` - Malay odds format
  - `HONG_KONG` - Hong Kong odds format
  - `INDONESIAN` - Indonesian odds format
- **Case Sensitivity:** The parameter values are case-sensitive and must be provided in uppercase format exactly as specified
- **Behavior:** When not specified, the system defaults to American odds format for all price values in the response

## Response Structure

### Success Response Format

The API returns a JSON object with the following structure:

#### Root Object
- **Type:** Object
- **Properties:**
  - `data` (Array): Contains the historical odds data for all requested IDs

#### Data Array Elements
Each element in the `data` array represents the complete historical record for one odds ID:

- **Type:** Object
- **Properties:**
  - `id` (String): The unique identifier for the odds entry, matching the requested ID parameter
  - `entries` (Array): Chronological list of all historical events for this specific odds entry

#### Entries Array Elements
Each entry in the `entries` array represents a single historical event:

- **Type:** Object
- **Properties:**
  - `timestamp` (Number): Unix timestamp with microsecond precision indicating when the event occurred
  - `event` (String): Type of event that occurred (see Event Types section below)
  - `price` (Number): The odds price at the time of this event, formatted according to the `odds_format` parameter
  - `is_main` (Boolean): Indicates whether this represents the main/primary odds line
  - `settlement` (String|null): Settlement outcome if the event represents a final settlement, otherwise null

### Event Types

The following event types may appear in the historical data:

#### `copilot-odds`
- **Description:** Represents a standard odds price update or initial odds publication
- **Occurrence:** Multiple times throughout the betting period as market conditions change
- **Settlement Field:** Always `null` for this event type

#### `copilot-locked-odds`
- **Description:** Indicates that the odds have been locked and are no longer available for betting
- **Occurrence:** Typically occurs shortly before an event starts or when betting is suspended
- **Settlement Field:** Always `null` for this event type

#### `copilot-settled-odds`
- **Description:** Represents the final settlement of the odds with the official outcome
- **Occurrence:** Once per odds entry after the event conclusion and official result determination
- **Settlement Field:** Contains the settlement outcome (e.g., "Lost", "Won", "Push")

### Settlement Values

When the `settlement` field is populated (only for `copilot-settled-odds` events), it may contain:

- `"Won"` - The bet was successful/winning
- `"Lost"` - The bet was unsuccessful/losing  
- `"Push"` - The bet resulted in a tie/push (stake returned)
- `null` - No settlement information (for non-settlement events)

## Example Request

### HTTP Request
```
GET https://api.opticodds.com/api/v3/copilot/fixtures/odds/historical?id=96:-1:2025081351A30193:moneyline:kamil_kos&odds_format=AMERICAN
```

### Request Parameters Breakdown
- **Base URL:** `https://api.opticodds.com/api/v3/copilot/fixtures/odds/historical`
- **Query Parameters:**
  - `id=96:-1:2025081351A30193:moneyline:kamil_kos`
  - `odds_format=AMERICAN` (optional, defaults to AMERICAN if not specified)

## Example Response

### JSON Response Structure
```json
{
    "data": [
        {
            "id": "96:-1:2025081351A30193:moneyline:kamil_kos",
            "entries": [
                {
                    "timestamp": 1755110904.696682,
                    "event": "copilot-settled-odds",
                    "price": 1050.0,
                    "is_main": true,
                    "settlement": "Lost"
                },
                {
                    "timestamp": 1755110840.04459,
                    "event": "copilot-locked-odds",
                    "price": 1050.0,
                    "is_main": true,
                    "settlement": null
                },
                {
                    "timestamp": 1755110809.451415,
                    "event": "copilot-odds",
                    "price": 1050.0,
                    "is_main": true,
                    "settlement": null
                },
                {
                    "timestamp": 1755110725.246358,
                    "event": "copilot-odds",
                    "price": 575.0,
                    "is_main": true,
                    "settlement": null
                },
                {
                    "timestamp": 1755110160.409335,
                    "event": "copilot-odds",
                    "price": -130.0,
                    "is_main": true,
                    "settlement": null
                },
                {
                    "timestamp": 1755107335.40856,
                    "event": "copilot-odds",
                    "price": -122.0,
                    "is_main": true,
                    "settlement": null
                }
            ]
        }
    ]
}
```

### Response Analysis

The example response demonstrates a complete odds lifecycle:

1. **Initial Odds Publication** (`timestamp: 1755107335.40856`): 
   - Event: `copilot-odds`
   - Price: `-122.0` (American format, indicating a favorite)
   - Settlement: `null` (active betting)

2. **Price Movement** (`timestamp: 1755110160.409335`):
   - Event: `copilot-odds` 
   - Price: `-130.0` (odds became less favorable for bettors)
   - Settlement: `null` (still active)

3. **Significant Price Change** (`timestamp: 1755110725.246358`):
   - Event: `copilot-odds`
   - Price: `575.0` (dramatic shift to underdog status)
   - Settlement: `null` (still active)

4. **Price Stabilization** (`timestamp: 1755110809.451415`):
   - Event: `copilot-odds`
   - Price: `1050.0` (further movement in underdog direction)
   - Settlement: `null` (still active)

5. **Market Closure** (`timestamp: 1755110840.04459`):
   - Event: `copilot-locked-odds`
   - Price: `1050.0` (final available price before closure)
   - Settlement: `null` (betting no longer available)

6. **Final Settlement** (`timestamp: 1755110904.696682`):
   - Event: `copilot-settled-odds`
   - Price: `1050.0` (settled at final odds)
   - Settlement: `"Lost"` (bet was unsuccessful)

## Use Cases and Implementation Notes

### Primary Use Cases
1. **Historical Analysis:** Track how odds moved throughout the betting period
2. **Market Research:** Understand betting market behavior and price discovery mechanisms
3. **Risk Management:** Analyze settlement patterns and outcomes
4. **Data Analytics:** Feed historical odds data into predictive models or analysis systems

### Implementation Considerations
1. **Timestamp Precision:** The API provides microsecond precision timestamps for accurate chronological ordering
2. **Batch Processing:** Support for up to 10 IDs per request enables efficient bulk historical data retrieval
3. **Format Flexibility:** Multiple odds format options accommodate different regional preferences and calculation methods
4. **Event Ordering:** Entries are provided in chronological order based on timestamp values

### Rate Limiting and Best Practices
- Implement appropriate request throttling when making multiple API calls
- Cache historical data locally when possible, as historical records typically don't change after settlement
- Use batch requests (multiple IDs per request) to minimize API call overhead
- Consider the timezone implications of timestamp data for accurate historical analysis