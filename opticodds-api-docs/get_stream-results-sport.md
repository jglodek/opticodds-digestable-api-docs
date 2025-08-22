# Stream Results API Documentation

## Overview

This endpoint provides an alternative to polling the `/fixtures/results` endpoint and allows you to passively listen for updates. This endpoint leverages Server-Sent Events (SSE) responses of the HTTP protocol to deliver real-time fixture results and player statistics as they become available.

## Base URL

```
https://api.opticodds.com/api/v3/stream/results/{sport}
```

## Endpoint Format

- **Basketball**: `https://api.opticodds.com/api/v3/stream/results/basketball`
- **Football**: `https://api.opticodds.com/api/v3/stream/results/football`
- **Other Sports**: Replace `{sport}` with the appropriate sport identifier

## HTTP Method

**GET** - This endpoint uses HTTP GET requests with Server-Sent Events streaming

## Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `key` | string | Yes | Your API authentication key (e.g., "1234-5678-124") |
| `league` | array | Yes | Array of league identifiers to subscribe to (e.g., ["NCAAB"], ["NFL"]) |

## Best Practices

While the endpoint supports passing multiple leagues and game IDs, **we strongly recommend making a separate connection for each league** you are trying to subscribe to for optimal performance and reliability.

## Data Formats

- **Score Format**: The `score` format is identical to the format used in the `/fixtures/results` endpoint
- **Player Results Format**: The `player_results` format is identical to the format used in the `/player-results` endpoint

## Implementation Examples

### Python Implementation

**Requirements:**
- Python 3.10.2
- requests==2.31.0
- sseclient-py==1.8.0

**Required Dependency:**
Install the specific SSE client dependency: [https://pypi.org/project/sseclient-py/](https://pypi.org/project/sseclient-py/)

```python
import requests
from requests.exceptions import ChunkedEncodingError
import json
import sseclient  # pip install sseclient-py

while True:
    try:
        r = requests.get(
            "https://api.opticodds.com/api/v3/stream/results/basketball",
            params={
                "key": "1234-5678-124",
                "league": ["NCAAB"],
            },
            stream=True,
        )
        client = sseclient.SSEClient(r)
        for event in client.events():
            if event.event == "fixture-results":
                data = json.loads(event.data)
                print("results data", ":", data)
            else:
                print(event.event, ":", event.data)
    except ChunkedEncodingError as ex:
        print("Disconnected, attempting to reconnect...")
    except Exception as e:
        print("Error:", r.status_code, r.text)
        break
```

### Node.js Implementation

**Requirements:**
- Node.js
- eventsource package (`npm install eventsource`)

```javascript
const EventSource = require("eventsource");  // npm install eventsource

const url = "https://api.opticodds.com/api/v3/stream/results/basketball";
const params = {
  key: "1234-5678-124",
  league: ["NCAAB"],
};

function connectToStream() {
  // Construct the query string with repeated parameters
  const queryString = new URLSearchParams();
  queryString.append("key", params.key);
  params.league.forEach((league) => queryString.append("league", league));

  console.log(`${url}?${queryString.toString()}`);

  const eventSource = new EventSource(`${url}?${queryString.toString()}`);

  eventSource.onmessage = function (event) {
    try {
      const data = JSON.parse(event.data);
      console.log("message data:", data);
    } catch (e) {
      console.log("Error parsing message data:", e);
    }
  };

  eventSource.addEventListener("fixture-results", function (event) {
    const data = JSON.parse(event.data);
    console.log("results data:", data);
  });

  eventSource.onerror = function (event) {
    console.error("EventSource failed:", event);
    eventSource.close();
    setTimeout(connectToStream, 1000); // Attempt to reconnect after 1 second
  };
}

connectToStream();
```

## Event Types

The API sends several types of Server-Sent Events:

### 1. Connected Event

Sent when the connection is successfully established.

```
event: connected
retry: 5000
data: ok go
```

**Properties:**
- `event`: "connected"
- `retry`: 5000 (milliseconds before retry on connection failure)
- `data`: "ok go" (confirmation message)

### 2. Ping Event

Periodic heartbeat events to keep the connection alive.

```
event: ping
retry: 5000
data: 2024-08-28T18:57:49Z
```

**Properties:**
- `event`: "ping"
- `retry`: 5000 (milliseconds before retry on connection failure)
- `data`: ISO 8601 formatted timestamp

### 3. Fixture Results Event

The primary event containing comprehensive fixture and player data.

```
event: fixture-results
id: 1722523617827-0
retry: 5000
data: {comprehensive JSON payload with fixture and player data}
```

**Properties:**
- `event`: "fixture-results"
- `id`: Unique identifier for this result update
- `retry`: 5000 (milliseconds before retry on connection failure)
- `data`: Complete JSON payload containing fixture results and player statistics

## Fixture Results Data Structure

The fixture results event contains extensive data including:

### Main Data Object
- `fixture_id`: Unique identifier for the fixture
- `is_live`: Boolean indicating if the game is currently live
- `league`: League identifier (e.g., "NFL", "NCAAB")
- `sport`: Sport type (e.g., "football", "basketball")
- `entry_id`: Unique entry identifier for this data update

### Player Results Array
Each player object includes:
- **Player Information**: ID, name, jersey number, position
- **Team Information**: Team ID and name
- **Status**: Player status (e.g., "completed")
- **Statistics**: Comprehensive stats array with period-specific data

### Score Information
- **Fixture Details**: Teams, start date, game status
- **Live Game State**: Current period, clock, possession, etc.
- **Period Scores**: Breakdown by quarter/period
- **Total Scores**: Final or current totals for both teams

### Team Statistics
Aggregate team statistics including:
- Offensive statistics (passing, rushing, receiving)
- Defensive statistics (tackles, sacks, interceptions)
- Special teams statistics (punting, kicking, returns)
- Turnover statistics (fumbles, interceptions)

## Connection Management

### Error Handling
- Implement retry logic for connection failures
- Handle `ChunkedEncodingError` exceptions gracefully
- Monitor HTTP status codes for authentication and rate limiting issues

### Reconnection Strategy
- Automatically reconnect on connection loss
- Implement exponential backoff for repeated failures
- Maintain separate connections per league for reliability

### Resource Management
- Properly close connections when no longer needed
- Monitor memory usage for long-running connections
- Handle network timeouts appropriately

This streaming endpoint provides real-time access to comprehensive sports data, making it ideal for applications requiring immediate updates on game results and player performance statistics.