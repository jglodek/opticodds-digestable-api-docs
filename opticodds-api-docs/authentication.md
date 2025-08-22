# OpticOdds Authentication API

## Overview

The OpticOdds API provides two methods for API key authentication to access their sports betting data endpoints. Authentication is required for all API calls to access real-time sportsbook odds, injury reports, schedules, and results.

## Authentication Methods

### 1. X-Api-Key Header Authentication

**Method:** Pass API key as HTTP header  
**Header Name:** `X-Api-Key`  
**Header Value:** Your API key

#### Description
You can authenticate by passing your API key as a header with the name `X-Api-Key`. This is the recommended method for API authentication as it keeps the API key out of URL logs and is more secure.

#### Example Request
```bash
curl --location 'https://api.opticodds.com/api/v3/leagues?sport=basketball' \
--header 'X-Api-Key: <YOUR API KEY>'
```

**Request Details:**
- **Base URL:** `https://api.opticodds.com/api/v3/`
- **HTTP Method:** GET (in example)
- **Required Headers:**
  - `X-Api-Key: <YOUR_API_KEY>` (replace with your actual API key)

### 2. Query Parameter Authentication

**Method:** Pass API key as URL query parameter  
**Parameter Name:** `key`  
**Parameter Value:** Your API key

#### Description
Alternatively, you can pass your API key as a query parameter with the name `key`. This method is simpler for testing but less secure as the API key appears in URL logs.

#### Example Request
```bash
curl --location 'https://api.opticodds.com/api/v3/leagues?sport=basketball&key=<YOUR API KEY>'
```

**Request Details:**
- **Base URL:** `https://api.opticodds.com/api/v3/`
- **HTTP Method:** GET (in example)
- **Required Query Parameters:**
  - `key=<YOUR_API_KEY>` (replace with your actual API key)
  - Additional endpoint-specific parameters (e.g., `sport=basketball`)

## API Key Requirements

- **API Key Source:** Obtained from OpticOdds platform
- **Authentication Type:** API Key authentication
- **Security Level:** Required for all endpoints
- **Key Format:** String value (format not specified in documentation)

## Implementation Notes

1. **Security Recommendation:** Use the header method (`X-Api-Key`) rather than query parameter method for better security
2. **API Key Management:** Keep your API key secure and do not expose it in client-side code
3. **Base URL:** All API requests should be made to `https://api.opticodds.com/api/v3/`
4. **Flexibility:** Both authentication methods can be used interchangeably based on your implementation needs

## Error Handling

The documentation does not specify error codes or responses for authentication failures, but typical API authentication errors would include:

- **401 Unauthorized:** Invalid or missing API key
- **403 Forbidden:** API key lacks required permissions
- **429 Too Many Requests:** Rate limit exceeded

## Usage Context

This authentication system is designed for:
- Sportsbook operators
- Data providers  
- Developers building sports betting applications
- Analytics platforms requiring real-time sports data

The API provides access to comprehensive sports betting data including odds, injury reports, schedules, results, and other sports-related information across multiple sports and regions (United States, Canada, Europe, Australia, and Asia).