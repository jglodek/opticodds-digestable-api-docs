# OpticOdds API v3 - Divisions Endpoint

## Endpoint Overview

**Base URL:** `https://api.opticodds.com/api/v3/divisions`

**HTTP Method:** `GET`

**Description:** Get a comprehensive list of all divisions and the leagues that they are a part of for the given sports and leagues. This endpoint provides detailed information about organizational divisions within specific sports leagues, allowing users to understand the hierarchical structure of various sporting competitions.

## Endpoint Description

This API endpoint retrieves a complete list of divisions associated with specified sports and leagues. The endpoint is designed to provide users with detailed information about how various sports leagues are organized into divisions, which is crucial for understanding the structure of different sporting competitions. The response includes both division names and their associated league information, providing a comprehensive view of the organizational hierarchy within the specified sports ecosystem.

The endpoint is particularly useful for applications that need to categorize teams, organize competitions, or provide users with detailed league structure information. By querying this endpoint, developers can obtain structured data about how leagues are divided and organized, which can be used for various analytical, informational, or organizational purposes within sports-related applications.

## Required Parameters

### Parameter Requirements

**Important Note:** You must pass at least one of the following parameters: `sport` and/or `league`. The API requires a minimum of one parameter to be specified to return meaningful results.

### sport

- **Parameter Name:** `sport`
- **Data Type:** String
- **Required:** Conditional (at least one of `sport` or `league` must be provided)
- **Description:** The sport you want division data for. This parameter accepts flexible input formats to accommodate different use cases and user preferences.
- **Accepted Values:** 
  - Sport ID (string identifier)
  - Sport name (full name as string)
- **Usage Notes:** This parameter allows you to filter divisions by a specific sport. You can use either the standardized sport ID or the full sport name, providing flexibility in how you reference sports in your API calls.

### league

- **Parameter Name:** `league`
- **Data Type:** String
- **Required:** Conditional (at least one of `sport` or `league` must be provided)
- **Description:** The league you want division data for. This parameter provides detailed filtering capabilities for specific league structures.
- **Accepted Values:**
  - League ID (string identifier)
  - League name (full name as string)
- **Usage Notes:** This parameter enables you to retrieve division information for a specific league. Similar to the sport parameter, you can use either the league ID or the full league name, ensuring compatibility with various data sources and user input methods.

## Example API Requests

### Example Request URL

```
https://api.opticodds.com/api/v3/divisions?league=NCAAF
```

**Request Breakdown:**
- **Base URL:** `https://api.opticodds.com/api/v3/divisions`
- **Query Parameter:** `league=NCAAF`
- **Purpose:** Retrieve all divisions associated with the NCAAF (National Collegiate Athletic Association Football) league

## Response Format

### Response Structure

The API returns data in JSON format with a structured hierarchy that provides comprehensive information about divisions and their associated leagues.

### Example JSON Response

```json
{
    "data": [
        {
            "name": "FBS",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "FCS",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        }
    ]
}
```

### Response Schema Explanation

#### Root Level Object

- **data** (Array): Contains the complete list of divisions and their associated league information

#### Division Object Structure

Each division object within the data array contains the following properties:

- **name** (String): The official name or designation of the division
  - **Purpose:** Provides the human-readable identifier for the division
  - **Example Values:** "FBS", "FCS", "Division I", "Division II", etc.
  - **Usage:** This field can be used for display purposes, categorization, or filtering operations

#### Leagues Array Structure

Within each division object, the `leagues` array contains detailed information about associated leagues:

- **leagues** (Array): Contains league objects that are associated with the current division

#### League Object Properties

Each league object within the leagues array includes:

- **id** (String): The unique identifier for the league
  - **Purpose:** Provides a standardized, programmatic reference for the league
  - **Example:** "ncaaf"
  - **Usage:** Ideal for database operations, API calls, and system integrations

- **name** (String): The full, official name of the league
  - **Purpose:** Provides the complete, human-readable name of the league
  - **Example:** "NCAAF"
  - **Usage:** Suitable for user interfaces, reports, and display purposes

### Response Data Interpretation

#### Example Response Analysis

In the provided example response:

1. **FBS Division:**
   - Division Name: "FBS" (Football Bowl Subdivision)
   - Associated League: NCAAF (ID: "ncaaf", Name: "NCAAF")

2. **FCS Division:**
   - Division Name: "FCS" (Football Championship Subdivision)
   - Associated League: NCAAF (ID: "ncaaf", Name: "NCAAF")

This structure demonstrates how multiple divisions can be associated with the same league, providing a clear hierarchical view of how sports organizations are structured.

### Technical Implementation Notes

#### Data Relationships

The response structure illustrates the many-to-many relationship between divisions and leagues, where:
- A single league can contain multiple divisions
- A division can potentially be associated with multiple leagues (though not shown in this example)

#### API Response Consistency

The response maintains consistent naming conventions and data types across all division and league objects, ensuring reliable parsing and processing in client applications.

#### Scalability Considerations

The array-based structure allows for efficient handling of variable numbers of divisions and leagues, accommodating different sports with varying organizational structures.