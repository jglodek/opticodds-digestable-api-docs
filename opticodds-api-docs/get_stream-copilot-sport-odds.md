# OpticOdds Copilot Basketball Odds Streaming API

## Endpoint Description

This endpoint provides an alternative to polling the `/copilot/fixtures/odds` endpoint and allows you to passively listen for updates. This endpoint leverages the Server-Sent Events (SSE) responses of the HTTP protocol, enabling real-time streaming of basketball odds data without the need for continuous polling.

**Base URL:** `https://api.opticodds.com/api/v3/stream/copilot/basketball/odds`

**Method:** GET

**Protocol:** HTTP with Server-Sent Events (SSE)

## Specific Parameter Information

### include_fixture_updates

**Type:** Boolean  
**Required:** No  
**Default:** false

This parameter controls whether the stream will return any status or start date changes for fixtures that meet the criteria of the data being passed in. When set to `true`, you will receive `fixture-status` events containing information about:
- Game time changes (start_date modifications)
- Status changes (e.g., from "unplayed" to "cancelled")
- Complete fixture information including teams, game IDs, and leagues

### is_live

**Type:** Boolean  
**Required:** No  
**Default:** null (returns both)

This parameter allows you to filter for prematch or live odds or both:
- `true`: Returns only live odds during games in progress
- `false`: Returns only prematch odds before games begin
- Not specified or `null`: Returns both prematch and live odds

## Best Practices and Recommendations

While the endpoint supports passing multiple leagues and game IDs simultaneously, it is strongly recommended to group up to a maximum of 10 leagues per connection to ensure optimal performance and maintain connection stability. Exceeding this recommendation may result in connection timeouts, increased latency, or data transmission issues.

## Implementation Examples

### Python Implementation

#### Requirements

- **Python Version:** 3.10.2 or higher
- **Dependencies:**
  - `requests==2.31.0`
  - `sseclient-py==1.8.0` (Must use this specific SSE client dependency: https://pypi.org/project/sseclient-py/)

#### Python Code Example

```python
import requests
from requests.exceptions import ChunkedEncodingError
import json
import sseclient  # pip install sseclient-py

last_entry_id: str | None = None
while True:
    try:
        params = {
            "key": "1234-5678-124",
            "market": ["Moneyline"],
            "league": ["NCAAB"],
            # "is_main": True,
        }
        if last_entry_id:
            params["last_entry_id"] = last_entry_id
      
        r = requests.get(
            "https://api.opticodds.com/api/v3/stream/copilot/basketball/odds",
            params=params,
            stream=True,
        )
        client = sseclient.SSEClient(r)
        for event in client.events():
            if event.event == "copilot-odds":
                data = json.loads(event.data)
                last_entry_id = data.get("entry_id")
                print("copilot-odds data", ":", data)
            elif event.event == "copilot-locked-odds":
                data = json.loads(event.data)
                last_entry_id = data.get("entry_id")
                print("copilot-locked-odds data", ":", data)
            else:
                print(event.event, ":", event.data)
    except ChunkedEncodingError as ex:
        print("Disconnected, attempting to reconnect...")
    except Exception as e:
        print("Error:", r.status_code, r.text)
        break
```

### Node.js Implementation

#### Requirements

- **Node.js Package:** `eventsource` (install via: `npm install eventsource`)

#### JavaScript Code Example

```javascript
const EventSource = require("eventsource");  // npm install eventsource

const url = "https://api.opticodds.com/api/v3/stream/copilot/basketball/odds";
const params = {
  key: "1234-5678-124",
  market: ["Moneyline"],
  league: ["NCAAB"],
};
let lastEntryId = null;

function connectToStream() {
  // Construct the query string with repeated parameters
  const queryString = new URLSearchParams();
  queryString.append("key", params.key);
  params.sportsbook?.forEach((sportsbook) =>
    queryString.append("sportsbook", sportsbook)
  );
  params.market.forEach((market) => queryString.append("market", market));
  params.league.forEach((league) => queryString.append("league", league));
  if (lastEntryId) {
    queryString.append("last_entry_id", lastEntryId);
  }

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

  eventSource.addEventListener("copilot-odds", function (event) {
    const data = JSON.parse(event.data);
    lastEntryId = data.entry_id;
    console.log("odds data:", data);
  });

  eventSource.addEventListener("copilot-locked-odds", function (event) {
    const data = JSON.parse(event.data);
    lastEntryId = data.entry_id;
    console.log("locked-odds data:", data);
  });

  eventSource.onerror = function (event) {
    console.error("EventSource failed:", event);
    eventSource.close();
    setTimeout(connectToStream, 1000); // Attempt to reconnect after 1 second
  };
}

connectToStream();
```

## Server-Sent Events (SSE) Response Types

### Connected Event

This event is sent immediately upon successful connection establishment to confirm the streaming connection is active.

```
event: connected
retry: 5000
data: ok go
```

**Event Fields:**
- `event`: "connected"
- `retry`: Recommended retry interval in milliseconds (5000ms = 5 seconds)
- `data`: Confirmation message "ok go"

### Ping Event

Periodic heartbeat events sent to maintain connection and confirm the stream is still active. Contains timestamp information.

```
event: ping
retry: 5000
data: 2024-08-28T18:57:49Z
```

**Event Fields:**
- `event`: "ping"
- `retry`: Recommended retry interval in milliseconds
- `data`: Current timestamp in ISO 8601 format

### Copilot Odds Event

Contains real-time odds data updates for basketball games. This is the primary data event containing current betting odds information.

```
event: copilot-odds
id: 1730079534820-2
retry: 5000
data: { 
  "entry_id": "1678113258940-2", 
  "data": [ 
    { 
      "fixture_id": "4825158B6424", 
      "game_id": "16903-41811-2024-10-22", 
      "grouping_key": "default:104.5", 
      "id": "1:-1:4825158B6424:1st_half_total_points:over_104_5", 
      "is_live": false, 
      "is_main": false, 
      "league": "NBA", 
      "market": "1st Half Total Points", 
      "name": "Over 104.5", 
      "odd_id": "4825158B6424:1st_half_total_points:over_104_5", 
      "player_id": "", 
      "points": 104.5, 
      "price": -196, 
      "selection": "", 
      "selection_line": "over", 
      "sport": "basketball", 
      "team_id": "", 
      "timestamp": 1729646525, 
      "version_id": -1 
    } 
  ], 
  "type": "copilot-odds" 
}
```

**Data Object Fields:**
- `entry_id`: Unique identifier for tracking event sequence
- `data`: Array of odds objects containing:
  - `fixture_id`: Unique identifier for the game fixture
  - `game_id`: Formatted game identifier with team and date information
  - `grouping_key`: Key used for grouping related odds
  - `id`: Complete unique identifier for this specific odds entry
  - `is_live`: Boolean indicating if odds are for live game or prematch
  - `is_main`: Boolean indicating if this is a main/featured market
  - `league`: League designation (e.g., "NBA", "NCAAB")
  - `market`: Type of betting market (e.g., "1st Half Total Points")
  - `name`: Human-readable name of the bet
  - `odd_id`: Simplified odds identifier
  - `player_id`: Player identifier (empty for non-player markets)
  - `points`: Point value for totals/spreads
  - `price`: Odds price in American format
  - `selection`: Selection description
  - `selection_line`: Line type ("over", "under", etc.)
  - `sport`: Sport type ("basketball")
  - `team_id`: Team identifier (empty for non-team specific markets)
  - `timestamp`: Unix timestamp of odds update
  - `version_id`: Version tracking identifier

### Copilot Locked Odds Event

Contains information about odds that have been locked/removed from betting markets, typically due to game start, suspension, or other market closure reasons.

```
event: copilot-locked-odds
id: 1730079527180-0
retry: 5000
data: { 
  "entry_id": "1682600339900-0", 
  "data": [ 
    { 
      "fixture_id": "D86AB59E8025", 
      "game_id": "19370-30354-2024-10-23", 
      "grouping_key": "miami_heat:105.5", 
      "id": "1:-1:D86AB59E8025:team_total:miami_heat_over_105_5", 
      "is_live": false, 
      "is_main": true, 
      "league": "NBA", 
      "market": "Team Total", 
      "name": "Miami Heat Over 105.5", 
      "odd_id": "D86AB59E8025:team_total:miami_heat_over_105_5", 
      "player_id": "", 
      "points": 105.5, 
      "price": -103, 
      "selection": "Miami Heat", 
      "selection_line": "over", 
      "sport": "basketball", 
      "team_id": "26BB4DC5722F", 
      "timestamp": 1729646600, 
      "version_id": -1 
    } 
  ], 
  "type": "copilot-locked-odds" 
}
```

**Data Structure:** Same as copilot-odds event, but indicates these odds are no longer available for betting.

### Copilot Settled Odds Event

Contains information about odds that have been settled with final results after game completion.

```
event: copilot-settled-odds
id: 1730079534820-2
retry: 5000
data: { 
  "entry_id": "1682600339900-0", 
  "data": [ 
    { 
      "fixture_id": "D86AB59E8025", 
      "game_id": "19370-30354-2024-10-23", 
      "id": "1:-1:D86AB59E8025:team_total:miami_heat_over_105_5", 
      "league": "NBA", 
      "market": "Team Total", 
      "name": "Miami Heat Over 105.5", 
      "odd_id": "D86AB59E8025:team_total:miami_heat_over_105_5", 
      "player_id": "", 
      "sport": "basketball", 
      "team_id": "26BB4DC5722F", 
      "timestamp": 1729646600, 
      "settlement": "Won", 
      "settled_at": "2024-07-16T22:00:00+00:00", 
      "version_id": -1 
    } 
  ], 
  "type": "copilot-settled-odds" 
}
```

**Additional Fields for Settled Odds:**
- `settlement`: Result of the bet ("Won", "Lost", "Push", etc.)
- `settled_at`: ISO 8601 timestamp of when the bet was settled

## Fixture Status Update Events

These events are only transmitted when the `include_fixture_updates=true` parameter is specified in your request.

### Game Time Change Event

Sent when a game's scheduled start time is modified.

```
event: fixture-status
id: 1724871720243-0
retry: 5000
data: {
  "data": {
    "fixture": {
      "away_team_display": "Lorenzo Musetti",
      "game_id": "88067-26534-2024-35",
      "home_team_display": "Miomir Kecmanovic",
      "id": "FB0D30DCDD6C",
      "start_date": "2024-08-28T20:30:00+00:00"
    },
    "fixture_id": "FB0D30DCDD6C",
    "game_id": "88067-26534-2024-35",
    "league": "ATP",
    "new_start_date": "2024-08-28T20:30:00+00:00",
    "new_status": null,
    "old_start_date": "2024-08-28T20:20:00+00:00",
    "old_status": null,
    "sport": "tennis",
    "timestamp": 1724871720.2406485
  },
  "entry_id": "1724871720243-0"
}
```

### Status Change Event

Sent when a game's status changes (e.g., cancelled, postponed, completed).

```
event: fixture-status
id: 1724871720243-0
retry: 5000
data: { 
  "data": { 
    "fixture": { 
      "away_team_display": "Saisai Zheng", 
      "game_id": "30697-79652-2024-35", 
      "home_team_display": "Jessika Ponchet", 
      "id": "E145B23767E0", 
      "start_date": "2024-08-27T15:00:00+00:00" 
    }, 
    "fixture_id": "E145B23767E0", 
    "game_id": "30697-79652-2024-35", 
    "league": "WTA", 
    "new_start_date": null, 
    "new_status": "cancelled", 
    "old_start_date": null, 
    "old_status": "unplayed", 
    "sport": "tennis", 
    "timestamp": 1724761586.2172334 
  }, 
  "entry_id": "1724761586216-0" 
}
```

**Fixture Status Event Fields:**
- `fixture`: Complete fixture information including teams and identifiers
- `fixture_id`: Unique fixture identifier
- `game_id`: Game identification string
- `league`: League or competition name
- `new_start_date`: Updated start time (null if no time change)
- `new_status`: Updated game status (null if no status change)
- `old_start_date`: Previous start time (null if no time change)
- `old_status`: Previous game status (null if no status change)
- `sport`: Sport designation
- `timestamp`: Unix timestamp of the update
- `entry_id`: Unique event tracking identifier

## Connection Management and Error Handling

The SSE connection should be monitored for disconnections and automatically reconnected when failures occur. Both provided code examples include error handling and reconnection logic:

- **Python**: Uses `ChunkedEncodingError` exception handling with reconnection attempts
- **Node.js**: Uses `onerror` event handling with automatic reconnection after 1-second delays

The `last_entry_id` parameter should be maintained across reconnections to ensure no data is missed during brief disconnections. This identifier allows the server to resume streaming from the last successfully received event.