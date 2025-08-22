# API Documentation: Get Conferences

## Overview

This API endpoint retrieves a comprehensive list of all conferences and their associated leagues for specified sports and leagues. The endpoint provides detailed information about conference structures and their league affiliations, enabling clients to understand the organizational hierarchy of sports competitions.

## Endpoint Details

- **HTTP Method**: `GET`
- **Base URL**: `https://api.opticodds.com`
- **Endpoint Path**: `/api/v3/conferences`
- **Full URL**: `https://api.opticodds.com/api/v3/conferences`

## Description

Get a list of all conferences and the leagues that they are a part of for the given sports and leagues. This endpoint serves as a foundational resource for understanding the structural organization of sports competitions, providing clients with the ability to retrieve conference information filtered by specific sports or leagues. The response includes both the conference names and their associated league information, creating a complete mapping of the sports organizational hierarchy.

## Parameters

### Required Parameters

You must pass at least one sport and/or league parameter to make a valid request to this endpoint.

### Parameter Details

#### `sport`
- **Type**: String
- **Required**: Conditional (must pass either sport or league)
- **Description**: The sport you want data for. You can pass the id or the name.
- **Format**: Accepts both sport ID (identifier) and sport name (display name)
- **Usage**: Used to filter conferences that are part of the specified sport
- **Example Values**: 
  - By ID: `ncaaf`
  - By Name: `NCAAF`

#### `league`
- **Type**: String  
- **Required**: Conditional (must pass either sport or league)
- **Description**: The league you want data for. You can pass the id or the name.
- **Format**: Accepts both league ID (identifier) and league name (display name)
- **Usage**: Used to filter conferences that are part of the specified league
- **Example Values**:
  - By ID: `ncaaf`
  - By Name: `NCAAF`

### Parameter Requirements

- **Minimum Requirement**: At least one of `sport` or `league` must be provided
- **Multiple Parameters**: Both `sport` and `league` can be passed simultaneously for more specific filtering
- **Flexible Input Format**: Both ID and name formats are accepted for each parameter
- **Case Sensitivity**: Parameter values may be case-sensitive depending on the specific implementation

## Request Examples

### Basic League Filter Request
```
GET https://api.opticodds.com/api/v3/conferences?league=NCAAF
```

### Multiple Parameter Request Examples
```
GET https://api.opticodds.com/api/v3/conferences?sport=ncaaf&league=NCAAF
GET https://api.opticodds.com/api/v3/conferences?sport=football
GET https://api.opticodds.com/api/v3/conferences?league=ncaaf
```

## Response Format

### Response Structure

The API returns a JSON object with the following structure:

```json
{
    "data": [
        {
            "name": "string",
            "leagues": [
                {
                    "id": "string",
                    "name": "string"
                }
            ]
        }
    ]
}
```

### Response Fields Description

#### Root Level
- **`data`** (Array): Contains the complete list of conference objects that match the specified criteria

#### Conference Object Structure
- **`name`** (String): The official name or identifier of the conference
- **`leagues`** (Array): Contains an array of league objects that this conference is associated with

#### League Object Structure (within each conference)
- **`id`** (String): The unique identifier for the league (typically lowercase)
- **`name`** (String): The official display name of the league (typically uppercase)

## Example Response

### Request
```
GET https://api.opticodds.com/api/v3/conferences?league=NCAAF
```

### Response
```json
{
    "data": [
        {
            "name": "IndFCS",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "CUSA",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "SoCon",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "SWAC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "MAC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "CAA",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "Pat",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "Pac-12",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "UAT",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "IndFBS",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "Big 12",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "SEC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "BigSky",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "SthLnd",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "ACC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "MEAC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "NEC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "MWC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "AAC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "SBC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "Big 10",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "BigSouOvc",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "MVC",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "Pio",
            "leagues": [
                {
                    "id": "ncaaf",
                    "name": "NCAAF"
                }
            ]
        },
        {
            "name": "Ivy",
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

## Conference Names Explained

The example response includes various college football conferences with their abbreviated names:

- **IndFCS**: Independent FCS (Football Championship Subdivision) teams
- **CUSA**: Conference USA
- **SoCon**: Southern Conference  
- **SWAC**: Southwestern Athletic Conference
- **MAC**: Mid-American Conference
- **CAA**: Colonial Athletic Association
- **Pat**: Patriot League
- **Pac-12**: Pacific-12 Conference
- **UAT**: United Athletic Conference (or similar regional grouping)
- **IndFBS**: Independent FBS (Football Bowl Subdivision) teams
- **Big 12**: Big 12 Conference
- **SEC**: Southeastern Conference
- **BigSky**: Big Sky Conference
- **SthLnd**: Southland Conference
- **ACC**: Atlantic Coast Conference
- **MEAC**: Mid-Eastern Athletic Conference
- **NEC**: Northeast Conference
- **MWC**: Mountain West Conference
- **AAC**: American Athletic Conference
- **SBC**: Sun Belt Conference
- **Big 10**: Big Ten Conference
- **BigSouOvc**: Big South-OVC Association (Ohio Valley Conference partnership)
- **MVC**: Missouri Valley Conference
- **Pio**: Pioneer Football League
- **Ivy**: Ivy League

## Technical Implementation Notes

### Content-Type
- **Request Content-Type**: Not applicable (GET request with query parameters)
- **Response Content-Type**: `application/json`

### HTTP Status Codes
- **200 OK**: Successful request with data returned
- **400 Bad Request**: Missing required parameters or invalid parameter format
- **404 Not Found**: No conferences found matching the specified criteria
- **500 Internal Server Error**: Server-side processing error

### Rate Limiting
- Rate limiting information should be checked in the API provider's general documentation
- Standard HTTP rate limiting headers may be included in responses

### Authentication
- Authentication requirements should be verified in the main API documentation
- API key or token-based authentication may be required

### Additional Notes
- The endpoint supports both ID and name-based parameter inputs for maximum flexibility
- Conference names may vary in format (some abbreviated, some full names)
- The leagues array within each conference object allows for conferences that may participate in multiple leagues
- Response data is returned in a consistent JSON format for easy parsing and integration