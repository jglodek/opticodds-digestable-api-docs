# OpticOdds Tournaments API Endpoint Documentation

## GET /api/v3/tournaments

### Description
Returns a comprehensive list of all tournaments that are currently supported or have been previously supported by OpticOdds. This endpoint provides detailed information about golf tournaments across multiple leagues and provides a complete tournament database for historical and current tournament data.

**Current Sport Coverage:**
- Golf (comprehensive coverage across multiple professional tours)

### Endpoint URL
```
https://api.opticodds.com/api/v3/tournaments
```

### HTTP Method
`GET`

### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `sport` | string | Yes | Specifies the sport for which to retrieve tournaments. Currently only supports `"golf"` |

### Example Request URL
```
https://api.opticodds.com/api/v3/tournaments?sport=golf
```

### Response Format
The API returns a JSON response containing a paginated list of tournaments with comprehensive metadata for each tournament.

### Response Structure

#### Root Response Object
| Field | Type | Description |
|-------|------|-------------|
| `data` | array | Array of tournament objects containing detailed tournament information |
| `page` | integer | Current page number in the paginated response |
| `total_pages` | integer | Total number of pages available for the complete dataset |

#### Tournament Object Structure
Each tournament object in the `data` array contains the following comprehensive fields:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique hexadecimal identifier for the tournament (e.g., "8435CFF305F6") |
| `name` | string | Full official name of the tournament (e.g., "Fortinet Australian PGA Championship 2024") |
| `start_date` | string | Tournament start date and time in ISO 8601 format (UTC timezone) |
| `end_date` | string | Tournament end date and time in ISO 8601 format (UTC timezone) |
| `status` | string | Current status of the tournament (e.g., "completed", "active", "upcoming") |
| `season_year` | string | The season year the tournament belongs to (e.g., "2024") |
| `venue_name` | string | Name of the golf course or venue hosting the tournament |
| `venue_location` | string | Geographic location of the venue (city, state/province, country) |
| `sport` | object | Sport information object |
| `league` | object | League/tour information object |
| `is_active` | boolean | Indicates whether the tournament is currently active in the system |
| `is_live` | boolean | Indicates whether the tournament is currently being played live |

#### Sport Object Structure
| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Sport identifier (currently "golf") |
| `name` | string | Human-readable sport name (currently "Golf") |

#### League Object Structure
| Field | Type | Description |
|-------|------|-------------|
| `id` | string | League/tour identifier (e.g., "pga", "dp_world_tour", "liv", "korn_ferry", "champions_tour") |
| `name` | string | Full name of the league/tour (e.g., "PGA", "DP World Tour", "LIV", "Korn Ferry", "Champions Tour") |

### Supported Golf Tours/Leagues
The API currently provides tournament data for the following professional golf tours:

- **PGA Tour** (`pga`) - Premier professional golf tour in North America
- **DP World Tour** (`dp_world_tour`) - Formerly European Tour, premier professional golf tour in Europe and international markets
- **LIV Golf** (`liv`) - Professional golf tour featuring team-based competition
- **Korn Ferry Tour** (`korn_ferry`) - Developmental tour for the PGA Tour
- **Champions Tour** (`champions_tour`) - Senior professional golf tour for players 50 and older

### Example Response
```json
{
  "data": [
    {
      "id": "8435CFF305F6",
      "name": "Fortinet Australian PGA Championship 2024",
      "start_date": "2023-11-22T14:00:00Z",
      "end_date": "2023-11-25T14:00:00Z",
      "status": "completed",
      "season_year": "2024",
      "venue_name": "Royal Queensland GC",
      "venue_location": "Brisbane, Australia",
      "sport": {
        "id": "golf",
        "name": "Golf"
      },
      "league": {
        "id": "dp_world_tour",
        "name": "DP World Tour"
      },
      "is_active": true,
      "is_live": false
    },
    {
      "id": "D3C290475306",
      "name": "The Sentry 2024",
      "start_date": "2024-01-04T00:00:00Z",
      "end_date": "2024-01-08T05:00:00Z",
      "status": "completed",
      "season_year": "2024",
      "venue_name": "Plantation Course at Kapalua",
      "venue_location": "Kapalua, Maui, Hawaii, USA",
      "sport": {
        "id": "golf",
        "name": "Golf"
      },
      "league": {
        "id": "pga",
        "name": "PGA"
      },
      "is_active": true,
      "is_live": false
    }
  ],
  "page": 1,
  "total_pages": 2
}
```

### Tournament Status Values
- `"completed"` - Tournament has finished
- `"active"` - Tournament is currently ongoing
- `"upcoming"` - Tournament is scheduled for the future
- `"cancelled"` - Tournament has been cancelled
- `"postponed"` - Tournament has been postponed

### Date Format Details
All date fields (`start_date` and `end_date`) are provided in ISO 8601 format with UTC timezone designation (Z suffix). The format is: `YYYY-MM-DDTHH:MM:SSZ`

Examples:
- `"2024-01-04T00:00:00Z"` - January 4, 2024 at midnight UTC
- `"2024-01-08T05:00:00Z"` - January 8, 2024 at 5:00 AM UTC

### Pagination
The response includes pagination information to handle large datasets efficiently:
- `page`: Current page number (starts at 1)
- `total_pages`: Total number of pages available
- To retrieve subsequent pages, add `&page=2`, `&page=3`, etc. to the query string

### Geographic Coverage
The tournaments span multiple continents and countries, including:
- **North America**: United States, Canada, Mexico
- **Europe**: United Kingdom, Germany, Belgium, Netherlands, Sweden, Italy
- **Asia-Pacific**: Australia, Singapore, Hong Kong, China, Japan
- **Middle East**: UAE, Qatar, Bahrain, Saudi Arabia
- **Africa**: South Africa, Kenya, Mauritius
- **South America**: Argentina, Chile

### Use Cases
This endpoint is particularly valuable for:
- Tournament scheduling and calendar applications
- Historical tournament data analysis
- Venue and location-based tournament searches
- League/tour-specific tournament filtering
- Sports betting and odds comparison platforms
- Golf event management systems
- Tournament status monitoring and notifications

### Technical Notes
- All tournament IDs are unique hexadecimal strings
- Venue names may include course-specific details (e.g., "TPC Sawgrass (THE PLAYERS Stadium Course)")
- Location information includes varying levels of detail from city-level to specific geographic regions
- The `is_active` flag indicates system availability rather than tournament timing
- The `is_live` flag provides real-time tournament status for active events