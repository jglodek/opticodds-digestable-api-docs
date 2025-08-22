# Parlay Pricer API Documentation

## API Overview

### Description

The Parlay Pricer API allows you to get the odds for a parlay bet across multiple sportsbooks. You can include multiple entries in the parlay from different games and markets. It will only work if all entries are available on the sportsbooks you specify and can be combined into a parlay.

### Endpoint

```
POST https://api.opticodds.com/api/v3/parlay/odds
```

### Authentication

The API requires authentication via an API key passed as a query parameter:

```
?key=your-api-key-here
```

## Supported Sportsbooks

OpticOdds currently supports Same Game Parlay (SGP) data for the following sportsbooks:

- **BetMGM** - Major online sportsbook
- **BetMGM (UK)** - UK version of BetMGM
- **BetRivers** - Regional sportsbook platform
- **Betsson** - European sportsbook operator
- **Betway** - International sportsbook brand
- **Bwin** - European online betting company
- **DraftKings** - Major daily fantasy and sportsbook platform
- **Fanatics** - Sports merchandise and betting platform
- **Hard Rock** - Casino and sportsbook brand
- **LeoVegas** - Online casino and sportsbook
- **Midnite** - Modern sportsbook platform
- **Novig** - Commission-free betting platform
- **Rimble** - Emerging sportsbook platform
- **Sportzino** - Social casino and sportsbook
- **Unibet** - European sportsbook operator

## Supported Sports

OpticOdds currently supports Same Game Parlay (SGP) odds for the following sports:

- **Baseball** - Professional and collegiate baseball leagues
- **Basketball** - Professional and collegiate basketball leagues
- **American Football** - NFL, college football, and other American football leagues
- **Golf** - Professional golf tournaments and events
- **Hockey** - Professional hockey leagues including NHL
- **MMA** - Mixed martial arts events and organizations
- **Football / Soccer** - International soccer leagues and tournaments
- **Tennis** - Professional tennis tournaments and matches

Support for additional sports and markets are continuously being added. Reach out to your account manager if you have specific needs or questions about availability.

## OpticOdds AI - Bring Your Own Price

### Overview

The API supports **OpticOdds AI** as a special sportsbook that allows you to bring your own price and use the OpticOdds parlay engine to handle correlation calculations for you.

### Important Restrictions

- You can **only** pass `"OpticOdds AI"` in the list of sportsbooks when using this feature
- If you include `"OpticOdds AI"` with other sportsbooks, you will receive an error
- You **must** add either `price_american` or `price_decimal` to each of your entries when using OpticOdds AI
- Failure to include pricing information will result in an error

### Price Format Options

- **price_american**: American odds format (e.g., -125, +160)
- **price_decimal**: Decimal odds format (e.g., 2.2, 1.8)

## Request Structure

### Headers

```
Content-Type: application/json
```

### Request Body Parameters

#### sportsbooks (required)
- **Type**: Array of strings
- **Description**: List of sportsbook names to get parlay odds from
- **Special Case**: When using `"OpticOdds AI"`, it must be the only sportsbook in the array

#### entries (required)
- **Type**: Array of objects
- **Description**: List of betting selections to include in the parlay

#### Entry Object Structure

Each entry object contains the following properties:

##### market (required)
- **Type**: String
- **Description**: The betting market type (e.g., "Player Hits", "Player Strikeouts", "Moneyline", "Total Runs")

##### name (required)
- **Type**: String
- **Description**: The specific bet selection name (e.g., "Alec Burleson Over 0.5", "New York Yankees")

##### fixture_id (required)
- **Type**: String
- **Description**: Unique identifier for the game or event

##### price_american (optional)
- **Type**: Number
- **Description**: American odds format price (required when using OpticOdds AI)
- **Example**: -125, +160

##### price_decimal (optional)
- **Type**: Number
- **Description**: Decimal odds format price (required when using OpticOdds AI)
- **Example**: 2.2, 1.8

## Example Requests

### Standard Sportsbook Request

```bash
curl --location 'https://api.opticodds.com/api/v3/parlay/odds?key=a861d7a2-9fd4-4276-9f6e-ba50c110c029' \
--header 'Content-Type: application/json' \
--data '{
    "sportsbooks": [
        "Bwin",
        "DraftKings",
        "BetMGM"
    ],
    "entries": [
        {
            "market": "Player Hits",
            "name": "Alec Burleson Over 0.5",
            "fixture_id": "E1AFAEAF67DD"
        },
        {
            "market": "Player Hits",
            "name": "Brendan Donovan Over 0.5",
            "fixture_id": "E1AFAEAF67DD"
        },
        {
            "market": "Player Strikeouts",
            "name": "Andre Pallante Over 3.5",
            "fixture_id": "E1AFAEAF67DD"
        }
    ]
}'
```

### OpticOdds AI Request (Bring Your Own Price)

```bash
curl --location 'https://api.opticodds.com/api/v3/parlay/odds?key=a861d7a2-9fd4-4276-9f6e-ba50c110c029' \
--header 'Content-Type: application/json' \
--data '{
    "sportsbooks": [
        "OpticOdds AI"
    ],
    "entries": [
        {
            "market": "Player Hits",
            "name": "Alec Burleson Over 0.5",
            "fixture_id": "E1AFAEAF67DD",
            "price_american": -125
        },
        {
            "market": "Player Hits",
            "name": "Brendan Donovan Over 0.5",
            "fixture_id": "E1AFAEAF67DD",
            "price_decimal": 2.2
        },
        {
            "market": "Player Strikeouts",
            "name": "Andre Pallante Over 3.5",
            "fixture_id": "E1AFAEAF67DD",
            "price_american": 160
        }
    ]
}'
```

## Response Structure

### Successful Response Format

The API returns a JSON object with a `data` property containing results for each requested sportsbook.

#### Response Object Properties

##### data (object)
Contains sportsbook-specific results, where each key is a sportsbook name.

#### Sportsbook Result Object Properties

##### error (null or string)
- **Type**: null or string
- **Description**: Error message if the request failed, null if successful

##### missing_entries (null or array)
- **Type**: null or array of objects
- **Description**: List of entries that couldn't be found on the sportsbook, null if all entries were found

##### legs (null or array)
- **Type**: null or array of objects
- **Description**: Individual betting selections with their odds, null if request failed

##### price (null or number)
- **Type**: null or number
- **Description**: Combined parlay odds in American format, null if request failed

##### deep_link_urls (null or object)
- **Type**: null or object
- **Description**: URLs for direct linking to the sportsbook (when available)

#### Leg Object Properties

##### fixture_id (string)
- **Type**: string
- **Description**: Unique identifier for the game or event

##### market (string)
- **Type**: string
- **Description**: The betting market type

##### name (string)
- **Type**: string
- **Description**: The specific bet selection name

##### price (number)
- **Type**: number
- **Description**: Individual selection odds in American format

#### Missing Entry Object Properties

##### fixture_id (string)
- **Type**: string
- **Description**: Unique identifier for the game or event

##### market (string)
- **Type**: string
- **Description**: The betting market type (normalized format)

##### name (string)
- **Type**: string
- **Description**: The specific bet selection name (normalized format)

##### price (null)
- **Type**: null
- **Description**: Always null for missing entries

## Example Responses

### OpticOdds AI Success Response

```json
{
    "data": {
        "OpticOdds AI": {
            "error": null,
            "missing_entries": null,
            "legs": [
                {
                    "fixture_id": "mlb:3D5E0C0B1E12",
                    "market": "Total Runs",
                    "name": "Over 8",
                    "price": -102.0
                },
                {
                    "fixture_id": "mlb:3D5E0C0B1E12",
                    "market": "Moneyline",
                    "name": "New York Yankees",
                    "price": -161.0
                }
            ],
            "price": 194.0,
            "deep_link_urls": null
        }
    }
}
```

### Standard Sportsbook Success Response

```json
{
   "data":{
      "Blue Book":{
         "error":null,
         "missing_entries":null,
         "legs":[
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Hits",
               "name":"Alec Burleson Over 0.5",
               "price":-230.0
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Hits",
               "name":"Brendan Donovan Over 0.5",
               "price":-210.0
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Strikeouts",
               "name":"Andre Pallante Over 3.5",
               "price":122.0
            }
         ],
         "price":336.0
      },
      "DraftKings":{
         "error":null,
         "missing_entries":null,
         "legs":[
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Hits",
               "name":"Alec Burleson Over 0.5",
               "price":-265.0
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Hits",
               "name":"Brendan Donovan Over 0.5",
               "price":-215.0
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Strikeouts",
               "name":"Andre Pallante Over 3.5",
               "price":115.0
            }
         ],
         "price":280.0
      },
      "BetMGM":{
         "error":null,
         "missing_entries":null,
         "legs":[
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Hits",
               "name":"Alec Burleson Over 0.5",
               "price":-250.0
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Hits",
               "name":"Brendan Donovan Over 0.5",
               "price":-210.0
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"Player Strikeouts",
               "name":"Andre Pallante Over 3.5",
               "price":115.0
            }
         ],
         "price":310.0
      }
   }
}
```

## Error Responses

### General API Error Response

When the API encounters a general error retrieving parlay data:

```json
{
   "data":{
      "BetMGM":{
         "error":"Error with response. Try again later.",
         "missing_entries":null,
         "legs":null,
         "price":null
      }
   }
}
```

### Missing Entries Error Response

When specific betting selections cannot be found on the requested sportsbooks:

```json
{
   "data":{
      "Blue Book":{
         "error":"Missing odds for entries.",
         "missing_entries":[
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_hits",
               "name":"brendan_donovan_over_0_5",
               "price":null
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_hits",
               "name":"alec_burleson_over_0_5",
               "price":null
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_strikeouts",
               "name":"andre_pallante_over_3_5",
               "price":null
            }
         ],
         "legs":null,
         "price":null
      },
      "DraftKings":{
         "error":"Missing odds for entries.",
         "missing_entries":[
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_hits",
               "name":"brendan_donovan_over_0_5",
               "price":null
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_hits",
               "name":"alec_burleson_over_0_5",
               "price":null
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_strikeouts",
               "name":"andre_pallante_over_3_5",
               "price":null
            }
         ],
         "legs":null,
         "price":null
      },
      "BetMGM":{
         "error":"Missing odds for entries.",
         "missing_entries":[
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_hits",
               "name":"brendan_donovan_over_0_5",
               "price":null
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_hits",
               "name":"alec_burleson_over_0_5",
               "price":null
            },
            {
               "fixture_id":"E1AFAEAF67DD",
               "market":"player_strikeouts",
               "name":"andre_pallante_over_3_5",
               "price":null
            }
         ],
         "legs":null,
         "price":null
      }
   }
}
```

### Parlay Combination Error Response

When the selected betting entries cannot be combined into a parlay on specific sportsbooks:

```json
{
    "Blue Book": {
        "error": "Cannot be combined into a parlay on the sportsbook."
    },
    "DraftKings": {
        "error": "SelectionsCannotBeCombined"
    },
    "BetMGM": {
        "error": "Could not create parlay for all games."
    }
}
```

## Error Types and Descriptions

### Common Error Messages

1. **"Error with response. Try again later."**
   - General API or sportsbook connectivity issue
   - Recommendation: Retry the request after a brief delay

2. **"Missing odds for entries."**
   - One or more betting selections are not available on the sportsbook
   - The `missing_entries` array will contain details about unavailable selections

3. **"Cannot be combined into a parlay on the sportsbook."**
   - The sportsbook's rules prevent combining the selected bets into a parlay
   - This can occur due to correlation restrictions or market limitations

4. **"SelectionsCannotBeCombined"**
   - DraftKings-specific error indicating the selections violate parlay combination rules

5. **"Could not create parlay for all games."**
   - BetMGM-specific error indicating parlay creation failed

## Usage Notes and Best Practices

### API Key Management
- Keep your API key secure and do not expose it in client-side code
- Include the API key as a query parameter in all requests

### Request Optimization
- Limit the number of sportsbooks in a single request to improve response times
- Ensure all required fields are included to avoid validation errors

### Error Handling
- Always check the `error` field in each sportsbook response
- Use the `missing_entries` array to identify specific unavailable selections
- Implement retry logic for temporary API errors

### OpticOdds AI Usage
- Only use `"OpticOdds AI"` when you want to provide your own pricing
- Cannot be combined with other sportsbooks in the same request
- Must include either `price_american` or `price_decimal` for each entry

### Data Freshness
- Odds data is subject to change rapidly in live markets
- Cache responses appropriately based on your use case requirements
- Consider implementing real-time updates for time-sensitive applications