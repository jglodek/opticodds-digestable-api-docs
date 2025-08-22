# OpticOdds Leagues API Documentation

## API Endpoint Overview

The OpticOdds Leagues API endpoint provides comprehensive access to retrieve detailed information about all supported leagues across various sports within the OpticOdds platform. This endpoint serves as a fundamental resource for developers and applications requiring league metadata, geographical information, sport categorization, and gender-specific league details.

### Endpoint URL

```
GET https://api.opticodds.com/api/v3/leagues
```

## Description

This API endpoint returns a comprehensive list of all the leagues that are currently supported or have been previously supported by OpticOdds. The endpoint provides detailed information about each league including their unique identifiers, display names, associated sport information, geographical regions, region codes, and gender classifications. This endpoint is particularly useful for applications that need to present users with available league options, filter content by specific leagues, or perform league-based data analysis and reporting.

The leagues endpoint serves as a foundational resource that enables developers to:
- Retrieve all available leagues across the OpticOdds platform
- Understand the geographical distribution of supported leagues
- Filter leagues by sport category
- Identify gender-specific leagues and competitions
- Build dynamic user interfaces that populate league selection options
- Implement league-based routing and navigation systems
- Perform analytics and reporting based on league categorization

## HTTP Method

**GET** - This endpoint uses the HTTP GET method to retrieve league data. As a read-only operation, it does not modify any data on the server and is safe for caching implementations.

## Query Parameters

### sport (Optional)

The `sport` parameter allows filtering of leagues by specific sport categories. When provided, the API will return only leagues that belong to the specified sport.

- **Parameter Name:** `sport`
- **Type:** String
- **Required:** No (Optional)
- **Description:** Filters the league results to only include leagues from the specified sport category
- **Example Values:** 
  - `basketball`
  - `football` 
  - `baseball`
  - `soccer`
  - `hockey`
- **Usage Example:** `?sport=basketball`

### Additional Parameter Information

For comprehensive information about all available parameters, including additional filtering options, pagination controls, and response formatting options, users are directed to reference the complete parameter documentation located at the bottom of the API documentation page. These additional parameters may include options for:

- Pagination controls (limit, offset)
- Sorting preferences (sort_by, sort_order)
- Response format specifications
- Date range filtering options
- Region-specific filtering
- Gender-based filtering
- Active/inactive league status filtering

## Response Structure

The API returns a JSON response with a standardized structure that includes comprehensive league information organized within a data array.

### Root Response Object

The response contains a top-level `data` property that holds an array of league objects.

```json
{
  "data": [
    // Array of league objects
  ]
}
```

### League Object Schema

Each league object within the data array contains the following properties:

#### id (String)
- **Description:** Unique identifier for the league within the OpticOdds system
- **Type:** String
- **Format:** Lowercase, underscore-separated format
- **Purpose:** Used for API queries, database references, and programmatic league identification
- **Examples:** `"nba"`, `"china_-_cba"`, `"olympics_basketball_men"`

#### name (String)
- **Description:** Human-readable display name of the league
- **Type:** String  
- **Format:** Proper title case formatting suitable for user interfaces
- **Purpose:** Used for displaying league names to end users in applications and reports
- **Examples:** `"NBA"`, `"China - CBA"`, `"Olympics Basketball Men"`

#### sport (Object)
The sport object provides detailed information about the sport category to which the league belongs.

##### sport.id (String)
- **Description:** Unique identifier for the sport category
- **Type:** String
- **Format:** Lowercase, single-word format
- **Examples:** `"basketball"`, `"football"`, `"baseball"`

##### sport.name (String)
- **Description:** Human-readable display name of the sport
- **Type:** String
- **Format:** Proper title case formatting
- **Examples:** `"Basketball"`, `"Football"`, `"Baseball"`

#### region (String)
- **Description:** Geographical region or country where the league operates
- **Type:** String
- **Format:** Uppercase, underscore-separated format for multi-word regions
- **Purpose:** Used for geographical filtering and regional analysis
- **Common Values:**
  - `"UNITED_STATES"` - United States-based leagues
  - `"INTERNATIONAL"` - International competitions and tournaments
  - `"CHINA"` - China-based leagues
  - `"FRANCE"` - France-based leagues
  - `"GERMANY"` - Germany-based leagues
  - `"ITALY"` - Italy-based leagues
  - `"SPAIN"` - Spain-based leagues
  - `"NEW_ZEALAND"` - New Zealand-based leagues

#### region_code (String)
- **Description:** ISO country code or standardized abbreviation for the region
- **Type:** String
- **Format:** Three-letter uppercase country codes (ISO 3166-1 alpha-3) or standardized abbreviations
- **Purpose:** Used for internationalization, mapping, and standardized regional identification
- **Common Values:**
  - `"USA"` - United States
  - `"INT"` - International
  - `"CHN"` - China
  - `"FRA"` - France
  - `"DEU"` - Germany
  - `"ITA"` - Italy
  - `"ESP"` - Spain
  - `"NZL"` - New Zealand

#### gender (String)
- **Description:** Gender classification of the league participants
- **Type:** String
- **Format:** Lowercase string value
- **Possible Values:**
  - `"men"` - Men's leagues and competitions
  - `"women"` - Women's leagues and competitions
  - `"mixed"` - Mixed-gender competitions (if applicable)
- **Purpose:** Used for gender-based filtering, analysis, and appropriate content categorization

## Example Request

### Basic Request (All Leagues)
```
GET https://api.opticodds.com/api/v3/leagues
```

### Filtered Request (Basketball Leagues Only)
```
GET https://api.opticodds.com/api/v3/leagues?sport=basketball
```

## Example Response

**Important Note:** The following example response is provided solely to demonstrate the JSON format and data structure. The actual data returned by the API may differ from this example and will contain real-time, up-to-date information about supported leagues.

### Request URL:
```
https://api.opticodds.com/api/v3/leagues?sport=basketball
```

### Response JSON:
```json
{
  "data": [
    {
      "id": "big3",
      "name": "BIG3",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "UNITED_STATES",
      "region_code": "USA",
      "gender": "men"
    },
    {
      "id": "china_-_cba",
      "name": "China - CBA",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "CHINA",
      "region_code": "CHN",
      "gender": "men"
    },
    {
      "id": "eurocup",
      "name": "Eurocup",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "men"
    },
    {
      "id": "eurocup_women",
      "name": "Eurocup Women",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "women"
    },
    {
      "id": "euroleague",
      "name": "Euroleague",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "men"
    },
    {
      "id": "fiba_-_world_cup",
      "name": "FIBA - World Cup",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "men"
    },
    {
      "id": "france_-_lnb_pro_a",
      "name": "France - LNB Pro A",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "FRANCE",
      "region_code": "FRA",
      "gender": "men"
    },
    {
      "id": "germany_-_bbl",
      "name": "Germany - BBL",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "GERMANY",
      "region_code": "DEU",
      "gender": "men"
    },
    {
      "id": "italy_-_lega_basket_serie_a",
      "name": "Italy - Lega Basket Serie A",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "ITALY",
      "region_code": "ITA",
      "gender": "men"
    },
    {
      "id": "nba",
      "name": "NBA",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "UNITED_STATES",
      "region_code": "USA",
      "gender": "men"
    },
    {
      "id": "ncaab",
      "name": "NCAAB",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "UNITED_STATES",
      "region_code": "USA",
      "gender": "men"
    },
    {
      "id": "ncaaw",
      "name": "NCAAW",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "UNITED_STATES",
      "region_code": "USA",
      "gender": "women"
    },
    {
      "id": "new_zealand_-_nbl",
      "name": "New Zealand - NBL",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "NEW_ZEALAND",
      "region_code": "NZL",
      "gender": "men"
    },
    {
      "id": "olympics_3x3_basketball_men",
      "name": "Olympics 3x3 Basketball Men",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "men"
    },
    {
      "id": "olympics_3x3_basketball_women",
      "name": "Olympics 3x3 Basketball Women",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "women"
    },
    {
      "id": "olympics_basketball_men",
      "name": "Olympics Basketball Men",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "men"
    },
    {
      "id": "olympics_basketball_women",
      "name": "Olympics Basketball Women",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "INTERNATIONAL",
      "region_code": "INT",
      "gender": "women"
    },
    {
      "id": "spain_-_liga_acb",
      "name": "Spain - Liga ACB",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "SPAIN",
      "region_code": "ESP",
      "gender": "men"
    },
    {
      "id": "tbt",
      "name": "TBT",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "UNITED_STATES",
      "region_code": "USA",
      "gender": "men"
    },
    {
      "id": "usa_-_nba_summer_league",
      "name": "USA - NBA Summer League",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "UNITED_STATES",
      "region_code": "USA",
      "gender": "men"
    },
    {
      "id": "wnba",
      "name": "WNBA",
      "sport": {
        "id": "basketball",
        "name": "Basketball"
      },
      "region": "UNITED_STATES",
      "region_code": "USA",
      "gender": "women"
    }
  ]
}
```

## League Categories and Examples

The example response demonstrates the diversity of leagues supported by OpticOdds, including:

### Professional Leagues
- **NBA** - National Basketball Association (United States)
- **WNBA** - Women's National Basketball Association (United States)
- **China - CBA** - Chinese Basketball Association
- **Euroleague** - Premier European basketball competition

### College/University Leagues
- **NCAAB** - National Collegiate Athletic Association Basketball (Men's)
- **NCAAW** - National Collegiate Athletic Association Basketball (Women's)

### International Competitions
- **Olympics Basketball Men** - Olympic men's basketball tournament
- **Olympics Basketball Women** - Olympic women's basketball tournament
- **Olympics 3x3 Basketball Men** - Olympic men's 3x3 basketball tournament
- **Olympics 3x3 Basketball Women** - Olympic women's 3x3 basketball tournament
- **FIBA - World Cup** - FIBA Basketball World Cup

### Regional Professional Leagues
- **France - LNB Pro A** - French professional basketball league
- **Germany - BBL** - German Basketball Bundesliga
- **Italy - Lega Basket Serie A** - Italian professional basketball league
- **Spain - Liga ACB** - Spanish professional basketball league
- **New Zealand - NBL** - New Zealand National Basketball League

### Specialty Leagues and Tournaments
- **BIG3** - Professional 3-on-3 basketball league
- **TBT** - The Basketball Tournament
- **USA - NBA Summer League** - NBA's summer development league

## Technical Implementation Notes

### Response Format
- All responses are returned in JSON format with UTF-8 encoding
- The response structure follows a consistent pattern with the main data contained within a `data` array
- Each league object contains complete metadata necessary for identification and categorization

### Data Types and Validation
- String fields are returned as standard JSON strings
- All ID fields use consistent lowercase formatting with underscores for spacing
- Region codes follow international standards where applicable
- Gender classifications use standardized lowercase values

### Performance Considerations
- The endpoint returns all requested data in a single response
- For large datasets, consider implementing client-side pagination or filtering
- Response caching is recommended for frequently accessed league data
- The API supports HTTP caching headers for optimal performance

### Integration Best Practices
- Use league IDs for internal references and database storage
- Display league names for user-facing interfaces
- Implement regional filtering using region or region_code fields
- Consider gender-based filtering for appropriate content presentation
- Cache league data locally to minimize API calls for static reference information

## Additional Resources

For comprehensive information about all available query parameters, advanced filtering options, authentication requirements, rate limiting policies, and additional endpoint functionality, developers should refer to the complete API documentation located at the bottom of the main documentation page. This additional documentation includes detailed information about:

- Complete parameter reference guide
- Authentication and authorization requirements
- Rate limiting policies and best practices
- Error handling and response codes
- SDK availability and code examples
- Advanced filtering and querying capabilities
- Webhook integration options
- Data update frequencies and real-time capabilities