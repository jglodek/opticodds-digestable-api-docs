# API Documentation: Active Fixtures Endpoint

## Endpoint Overview

### Description
This API endpoint provides a paginated list of fixtures that are currently active (not completed) and have or have had odds associated with them at some point. The key distinction between this endpoint and the standard `/fixtures` endpoint is that this endpoint exclusively returns fixtures that have ever been associated with odds data, regardless of whether odds are currently available for those fixtures.

The endpoint maintains complete functional parity with the `/fixtures` endpoint in terms of parameters accepted and response structure returned. Both endpoints utilize identical parameter sets and return responses in the same format, with the only difference being the filtering criteria applied to determine which fixtures are included in the results.

### Key Characteristics
- **Active Status Filter**: Only returns fixtures that are not in a completed state
- **Odds Association Filter**: Only includes fixtures that have had odds data associated with them at any point in their lifecycle
- **Pagination Support**: Results are returned in paginated format to handle large datasets efficiently
- **Parameter Compatibility**: Accepts the same comprehensive set of query parameters as the standard fixtures endpoint
- **Response Structure**: Returns data in identical format to the standard fixtures endpoint

### Relationship to Standard Fixtures Endpoint
This endpoint serves as a specialized variant of the primary `/fixtures` endpoint, with additional filtering logic applied to focus specifically on fixtures with odds history. The implementation ensures that:
- All parameter validation rules remain consistent between endpoints
- Response schemas are identical between endpoints
- Pagination behavior is maintained across both endpoints
- Error handling follows the same patterns

## Technical Specifications

### HTTP Method
The endpoint accepts standard HTTP GET requests for retrieving fixture data.

### Content Type
All responses are returned in JSON format with appropriate content-type headers.

### Authentication Requirements
This endpoint follows the same authentication requirements as other API endpoints in the system. Proper authentication credentials must be provided to access the fixture data.

### Rate Limiting
Standard API rate limiting policies apply to this endpoint, consistent with other fixture-related endpoints in the API.

## Parameter Information

### Parameter Inheritance
This endpoint inherits the complete parameter set from the standard `/fixtures` endpoint. All query parameters that are available for the primary fixtures endpoint are also available for this active fixtures endpoint, maintaining full backward compatibility and consistency across the API.

### Parameter Categories
The available parameters span multiple categories including:
- **Filtering Parameters**: Allow filtering fixtures by various criteria such as date ranges, teams, competitions, and status
- **Pagination Parameters**: Control the number of results returned and which page of results to retrieve
- **Sorting Parameters**: Determine the order in which results are returned
- **Field Selection Parameters**: Allow clients to specify which fields should be included in the response
- **Format Parameters**: Control the format and structure of the returned data

### Parameter Validation
All parameters undergo the same validation processes as the standard fixtures endpoint, ensuring data integrity and preventing invalid requests from being processed.

### Comprehensive Parameter Reference
For the complete and detailed list of all available parameters, including their data types, validation rules, default values, and usage examples, users should refer to the comprehensive parameter documentation located at the bottom of the API documentation page. This reference provides exhaustive details about each parameter's functionality and proper usage patterns.

## Response Structure

### Response Format Consistency
The response structure for this endpoint is completely identical to that of the standard `/fixtures` endpoint. This ensures that existing client implementations can easily adapt to use this specialized endpoint without requiring changes to response parsing logic.

### Data Fields
The response includes all the same data fields as the standard fixtures endpoint, containing comprehensive fixture information such as:
- **Fixture Identification**: Unique identifiers and reference numbers
- **Team Information**: Details about participating teams
- **Competition Data**: Information about the competition or league
- **Scheduling Details**: Date, time, and venue information
- **Status Information**: Current fixture status and lifecycle stage
- **Historical Data**: Relevant historical context and statistics
- **Metadata**: Additional contextual information about the fixture

### Pagination Structure
The pagination structure follows the same format as the standard fixtures endpoint, providing:
- **Current Page Information**: Details about the current page of results
- **Total Count Information**: Total number of fixtures matching the criteria
- **Navigation Links**: URLs for accessing different pages of results
- **Page Size Configuration**: Information about the number of results per page

## Example Responses

### Response Examples Location
Comprehensive example responses for this endpoint can be found in the same location as the examples for the standard `/fixtures` endpoint. Since the response structure is identical between the two endpoints, the same examples apply to both endpoints.

### Example Categories
The available examples cover various scenarios including:
- **Basic Requests**: Simple requests with minimal parameters
- **Complex Filtering**: Requests utilizing multiple filter parameters
- **Pagination Examples**: Demonstrations of paginated result handling
- **Error Responses**: Examples of various error conditions and their responses

### Response Variations
Examples demonstrate the various ways responses can differ based on:
- **Parameter Combinations**: How different parameter combinations affect the response
- **Data Availability**: How responses change based on available data
- **Filtering Results**: How filtering parameters impact the returned fixture set

## Fixture Lifecycle Integration

### Lifecycle Documentation Reference
This endpoint integrates with the broader fixture lifecycle management system. Comprehensive information about fixture statuses, state transitions, and lifecycle stages can be found in the dedicated Fixtures Lifecycle documentation.

### Status Filtering Logic
The "active" classification used by this endpoint aligns with the fixture lifecycle states documented in the Fixtures Lifecycle documentation, ensuring consistent status interpretation across all API endpoints.

### State Management
Understanding the fixture lifecycle is crucial for properly interpreting the results returned by this endpoint, as the "active" status encompasses multiple specific lifecycle states that are detailed in the dedicated lifecycle documentation.

## Implementation Considerations

### Client Integration
When integrating this endpoint into client applications, developers should consider:
- **Response Processing**: Existing response processing logic for the `/fixtures` endpoint can be reused without modification
- **Parameter Usage**: All existing parameter validation and usage patterns remain applicable
- **Error Handling**: Error handling logic should follow the same patterns as the standard fixtures endpoint
- **Caching Strategies**: Cache invalidation strategies should account for the specific filtering criteria of this endpoint

### Performance Characteristics
This endpoint may exhibit different performance characteristics compared to the standard fixtures endpoint due to the additional filtering logic applied to identify fixtures with odds history. Clients should monitor response times and adjust request patterns accordingly.

### Data Freshness
The odds association filter means that fixtures will continue to appear in results even after odds are no longer available, providing a comprehensive view of fixtures that have had betting relevance at any point in their lifecycle.