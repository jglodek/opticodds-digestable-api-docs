# OpticOdds Stream API Documentation

## Description

This endpoint provides an alternative to polling the `/fixtures/odds` endpoint and allows you to passively listen for updates. This endpoint leverages the Server-Sent Events (SSE) responses of the HTTP protocol, providing real-time streaming capabilities for odds data and fixture updates.

## API Endpoint

**Base URL:** `https://api.opticodds.com/api/v3/stream/odds/{sport}`

**Method:** GET

**Protocol:** Server-Sent Events (SSE)

**Sports Available:** basketball, football, tennis, and other supported sports

## Specific Parameter Information

### include_fixture_updates

**Type:** Boolean  
**Required:** No  
**Description:** This parameter will return any status or start date changes for fixtures that meet the criteria of the passing data. When set to `true`, the API will send `fixture-status` events whenever a game's start time changes or its status changes (e.g., from "unplayed" to "cancelled").

## Best Practices

While our endpoint supports passing multiple leagues and game IDs, we recommend grouping up to 10 leagues per connection to optimize performance and maintain connection stability. This helps prevent connection timeouts and ensures reliable data delivery.

## Request Parameters

The API accepts the same parameters as the polling endpoint, including:

- `key` - Your API key (required)
- `sportsbook` - Array of sportsbook names to filter
- `market` - Array of market types to filter
- `league` - Array of league names to filter
- `is_main` - Boolean to filter main/alternate lines
- `last_entry_id` - String for resuming from a specific point in the stream
- `include_fixture_updates` - Boolean to include fixture status changes

## Example Requests

### Python Implementation

#### Requirements

- Python 3.10.2
- requests==2.31.0  
- sseclient-py==1.8.0 | **Important:** Use this specific sseclient dependency: https://pypi.org/project/sseclient-py/

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
            "sportsbook": ["DraftKings", "FanDuel", "Hard Rock"],
            "market": ["Moneyline"],
            "league": ["NCAAB"],
            # "is_main": True,
        }
        if last_entry_id:
            params["last_entry_id"] = last_entry_id
      
        r = requests.get(
            "https://api.opticodds.com/api/v3/stream/odds/basketball",
            params=params,
            stream=True,
        )
        client = sseclient.SSEClient(r)
        for event in client.events():
            if event.event == "odds":
                data = json.loads(event.data)
                last_entry_id = data.get("entry_id")
                print("odds data", ":", data)
            elif event.event == "locked-odds":
                data = json.loads(event.data)
                last_entry_id = data.get("entry_id")
                print("locked-odds data", ":", data)
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

- eventsource package: `npm install eventsource`

#### JavaScript Code Example

```javascript
const EventSource = require("eventsource");  // npm install eventsource

const url = "https://api.opticodds.com/api/v3/stream/odds/basketball";
const params = {
  key: "1234-5678-124",
  sportsbook: ["DraftKings", "FanDuel", "Hard Rock"],
  market: ["Moneyline"],
  league: ["NCAAB"],
};
const lastEntryId = null;

function connectToStream() {
  // Construct the query string with repeated parameters
  const queryString = new URLSearchParams();
  queryString.append("key", params.key);
  params.sportsbook.forEach((sportsbook) =>
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

  eventSource.addEventListener("odds", function (event) {
    const data = JSON.parse(event.data);
    lastEntryId = data.entry_id;
    console.log("odds data:", data);
  });

  eventSource.addEventListener("locked-odds", function (event) {
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

connectToStream()
```

## Example Events

### Connected Event

This event is sent immediately when a connection is established with the streaming endpoint.

```
event: connected
retry: 5000
data: ok go
```

**Fields:**
- `event`: "connected" - indicates successful connection establishment
- `retry`: 5000 - retry interval in milliseconds
- `data`: "ok go" - confirmation message

### Ping Event

Periodic heartbeat events to maintain connection and verify connectivity.

```
event: ping
retry: 5000
data: 2024-08-28T18:57:49Z
```

**Fields:**
- `event`: "ping" - heartbeat event type
- `retry`: 5000 - retry interval in milliseconds  
- `data`: ISO 8601 timestamp indicating when the ping was sent

### Odds Event

Triggered when an odd gets unsuspended, posted for the first time, or updated with new pricing information.

```
event: odds
id: 1730079534820-2
retry: 5000
data: {"data":[{"deep_link":{"android":"https://www.pinnacle.com/en/football/nfl/jacksonville-jaguars-vs-philadelphia-eagles/1599745256/#all","desktop":"https://www.pinnacle.com/en/football/nfl/jacksonville-jaguars-vs-philadelphia-eagles/1599745256/#all","ios":"https://www.pinnacle.com/en/football/nfl/jacksonville-jaguars-vs-philadelphia-eagles/1599745256/#all"},"fixture_id":"A69FA4D64518","game_id":"28265-17233-24-44","grouping_key":"default","id":"28265-17233-24-44:pinnacle:1st_half_moneyline:philadelphia_eagles","is_live":false,"is_main":true,"league":"NFL","limits":{"max_stake":1000},"market":"1st Half Moneyline","name":"Philadelphia Eagles","player_id":"","points":null,"price":-230,"selection":"Philadelphia Eagles","selection_line":"","selection_points":null,"sport":"football","sportsbook":"Pinnacle","team_id":"EDCC2866B795","timestamp":1730079534.7125728},{"deep_link":{"android":"https://www.pinnacle.com/en/football/nfl/jacksonville-jaguars-vs-philadelphia-eagles/1599745256/#all","desktop":"https://www.pinnacle.com/en/football/nfl/jacksonville-jaguars-vs-philadelphia-eagles/1599745256/#all","ios":"https://www.pinnacle.com/en/football/nfl/jacksonville-jaguars-vs-philadelphia-eagles/1599745256/#all"},"fixture_id":"A69FA4D64518","game_id":"28265-17233-24-44","grouping_key":"default","id":"28265-17233-24-44:pinnacle:1st_half_moneyline:jacksonville_jaguars","is_live":false,"is_main":true,"league":"NFL","limits":{"max_stake":1000},"market":"1st Half Moneyline","name":"Jacksonville Jaguars","player_id":"","points":null,"price":198,"selection":"Jacksonville Jaguars","selection_line":"","selection_points":null,"sport":"football","sportsbook":"Pinnacle","team_id":"9CCE4CA64CF2","timestamp":1730079534.7125728}],"entry_id":"1730079534820-2","type":"odds"}
```

**Event Fields:**
- `event`: "odds" - indicates odds data event
- `id`: "1730079534820-2" - unique event identifier
- `retry`: 5000 - retry interval in milliseconds
- `data`: JSON object containing odds information

**Data Object Structure:**
- `data`: Array of odds objects
- `entry_id`: Unique identifier for this event entry
- `type`: "odds" - event type confirmation

**Individual Odds Object Fields:**
- `deep_link`: Object containing platform-specific URLs (android, desktop, ios)
- `fixture_id`: Unique identifier for the game fixture
- `game_id`: Composite game identifier
- `grouping_key`: Key used for grouping related odds
- `id`: Unique identifier for this specific odds entry
- `is_live`: Boolean indicating if the game is currently live
- `is_main`: Boolean indicating if this is the main line (vs alternate)
- `league`: League name (e.g., "NFL", "NBA", "NCAAB")
- `limits`: Object containing betting limits information
- `market`: Market type (e.g., "1st Half Moneyline", "Total Points")
- `name`: Display name for the betting option
- `player_id`: Player identifier (if applicable to player props)
- `points`: Point value for spread/total bets
- `price`: Odds price in American format
- `selection`: Selection name
- `selection_line`: Line type (over/under for totals)
- `selection_points`: Point value for the selection
- `sport`: Sport type (e.g., "football", "basketball")
- `sportsbook`: Sportsbook name (e.g., "Pinnacle", "DraftKings")
- `team_id`: Unique identifier for the team
- `timestamp`: Unix timestamp of when the odds were recorded

### Locked Odds Event

Triggered when an odd gets suspended, taken off the board, or becomes unavailable for betting.

```
event: locked-odds
id: 1730079527180-0
retry: 5000
data: {"data":[{"deep_link":{"android":"dksb://sb/addbet/0QA219503604%2374975813_13L88808Q11169437916Q20","desktop":"https://sportsbook.draftkings.com/event/30568741?outcomes=0QA219503604%2374975813_13L88808Q11169437916Q20","ios":"dksb://sb/addbet/0QA219503604%2374975813_13L88808Q11169437916Q20"},"fixture_id":"8BDC2E0FF301","game_id":"11434-13184-24-43","grouping_key":"dak_prescott:247.5","id":"11434-13184-24-43:draftkings:player_passing_yards:dak_prescott_over_247_5","is_live":true,"is_main":true,"league":"NFL","limits":null,"market":"Player Passing Yards","name":"Dak Prescott Over 247.5","player_id":"4E18B0FEC4C5","points":247.5,"price":-115,"selection":"Dak Prescott","selection_line":"over","selection_points":247.5,"sport":"football","sportsbook":"DraftKings","team_id":"","timestamp":1730079527.1784158},{"deep_link":{"android":"dksb://sb/addbet/0QA219503604%2374975814_15L88808Q1-422942275Q20","desktop":"https://sportsbook.draftkings.com/event/30568741?outcomes=0QA219503604%2374975814_15L88808Q1-422942275Q20","ios":"dksb://sb/addbet/0QA219503604%2374975814_15L88808Q1-422942275Q20"},"fixture_id":"8BDC2E0FF301","game_id":"11434-13184-24-43","grouping_key":"dak_prescott:247.5","id":"11434-13184-24-43:draftkings:player_passing_yards:dak_prescott_under_247_5","is_live":true,"is_main":true,"league":"NFL","limits":null,"market":"Player Passing Yards","name":"Dak Prescott Under 247.5","player_id":"4E18B0FEC4C5","points":247.5,"price":-115,"selection":"Dak Prescott","selection_line":"under","selection_points":247.5,"sport":"football","sportsbook":"DraftKings","team_id":"","timestamp":1730079527.1784158}],"entry_id":"1730079527180-0","type":"locked-odds"}
```

The locked odds event contains the same data structure as the odds event, but indicates that these odds are no longer available for betting. The `limits` field may be `null` indicating no betting limits are applicable since the odds are suspended.

### Fixture Status Updates (Game Time Change)

This event type is only sent if you have `include_fixture_updates=true` in your request parameters. It notifies of changes to game start times.

```
event: fixture-status
id: 1724871720243-0
retry: 5000
data: {"data":{"fixture":{"away_team_display":"Lorenzo Musetti","game_id":"88067-26534-2024-35","home_team_display":"Miomir Kecmanovic","id":"FB0D30DCDD6C","start_date":"2024-08-28T20:30:00+00:00"},"fixture_id":"FB0D30DCDD6C","game_id":"88067-26534-2024-35","league":"ATP","new_start_date":"2024-08-28T20:30:00+00:00","new_status":null,"old_start_date":"2024-08-28T20:20:00+00:00","old_status":null,"sport":"tennis","timestamp":1724871720.2406485},"entry_id":"1724871720243-0"}
```

**Data Object Fields:**
- `fixture`: Object containing current fixture information
  - `away_team_display`: Display name of the away team/player
  - `game_id`: Unique game identifier
  - `home_team_display`: Display name of the home team/player
  - `id`: Fixture ID
  - `start_date`: Current start date in ISO 8601 format
- `fixture_id`: Fixture identifier
- `game_id`: Game identifier
- `league`: League name (e.g., "ATP", "WTA", "NFL")
- `new_start_date`: New start date after the change
- `new_status`: New game status (null if only time changed)
- `old_start_date`: Previous start date before the change
- `old_status`: Previous game status (null if only time changed)
- `sport`: Sport type
- `timestamp`: Unix timestamp of when the change occurred

### Fixture Status Updates (Status Change)

This event indicates a change in game status (e.g., from "unplayed" to "cancelled").

```
event: fixture-status
id: 1724871720243-0
retry: 5000
data: { "data": { "fixture": { "away_team_display": "Saisai Zheng", "game_id": "30697-79652-2024-35", "home_team_display": "Jessika Ponchet", "id": "E145B23767E0", "start_date": "2024-08-27T15:00:00+00:00" }, "fixture_id": "E145B23767E0", "game_id": "30697-79652-2024-35", "league": "WTA", "new_start_date": null, "new_status": "cancelled", "old_start_date": null, "old_status": "unplayed", "sport": "tennis", "timestamp": 1724761586.2172334 }, "entry_id": "1724761586216-0" }
```

In this example, the game status changed from "unplayed" to "cancelled", with no change to the start date (hence `new_start_date` and `old_start_date` are null).

## Implementation Notes

### Choosing a Good Key to Store the Data

Proper data storage key selection is crucial for efficient data management:

**For Multiple Sportsbooks per Game/Market Combination:**
- Recommended key format: `(Fixture ID + Sportsbook + Market + Name)`
- Example: `"A69FA4D64518_Pinnacle_Moneyline_Philadelphia Eagles"`

**For Single Sportsbook per Game/Market Combination:**
- Recommended key format: `(Fixture ID + Market + Name)`
- Example: `"A69FA4D64518_Moneyline_Philadelphia Eagles"`

This approach ensures unique identification and prevents data conflicts when processing multiple odds simultaneously.

### Connection Management and Resilience

- Implement proper error handling for `ChunkedEncodingError` to handle connection drops
- Use the `last_entry_id` parameter to resume streams from the last processed event
- Implement exponential backoff for reconnection attempts
- Monitor the `retry` field in events for server-recommended retry intervals

## Common Line Movement Cases

Understanding how the API handles line movements is crucial for proper implementation:

### Case 1: Sportsbook Moves Main Line and DOES NOT Have Any Alternate Lines

**Original Lines:**
- Over 5.5 | -110 | is_main=True
- Under 5.5 | +110 | is_main=True

**Sportsbook Changes Lines:**
- Over 5.5 | -110 | is_main=True → Over 6.5 | -110 | is_main=True
- Under 5.5 | +110 | is_main=True → Under 6.5 | +110 | is_main=True

#### When Filtering `is_main=True`:

You will receive these events in sequence:

1. `{event: "locked-odds", data: {"data":[{"bet_name": "Over 5.5", "is_main": True, "bet_price": -110, ...}]}}`
2. `{event: "locked-odds", data: {"data":[{"bet_name": "Under 5.5", "is_main": True, "bet_price": +110, ...}]}}`
3. `{event: "odds", data: {"data":[{"bet_name": "Over 6.5", "is_main": True, "bet_price": -110, ...}]}}`
4. `{event: "odds", data: {"data":[{"bet_name": "Under 6.5", "is_main": True, "bet_price": +110, ...}]}}`

#### When Filtering `is_main=False`:

You will not receive any events since no alternate lines exist in this scenario.

#### When `is_main` Filter is Not Set:

You will receive the same four events as the `is_main=True` case, since all lines in this scenario are main lines.

### Case 2: Sportsbook Moves Main Line and DOES HAVE Alternate Lines

**Original Lines:**
- Over 5.5 | -110 | is_main=True
- Under 5.5 | +110 | is_main=True  
- Over 6.5 | +120 | is_main=False
- Under 6.5 | -120 | is_main=False

**Sportsbook Changes Lines:**
- Over 5.5 | -110 | is_main=True → Over 5.5 | -120 | is_main=False
- Under 5.5 | +110 | is_main=True → Under 5.5 | +120 | is_main=False
- Over 6.5 | +120 | is_main=False → Over 6.5 | -110 | is_main=True
- Under 6.5 | -120 | is_main=False → Under 6.5 | +110 | is_main=True

#### When Filtering `is_main=True`:

You will receive these events:

1. `{event: "odds", data: {"data":[{"bet_name": "Over 6.5", "is_main": True, "bet_price": -110, ...}]}}`
2. `{event: "odds", data: {"data":[{"bet_name": "Under 6.5", "is_main": True, "bet_price": +110, ...}]}}`

**Important:** You will NOT receive locked events for the original Over 5.5 and Under 5.5 main lines, as they are being converted to alternate lines rather than being removed entirely.

#### When Filtering `is_main=False`:

You will receive these events:

1. `{event: "odds", data: {"data":[{"bet_name": "Over 5.5", "is_main": False, "bet_price": -120, ...}]}}`
2. `{event: "odds", data: {"data":[{"bet_name": "Under 5.5", "is_main": False, "bet_price": +120, ...}]}}`

**Important:** You will NOT receive locked events for the original Over 6.5 and Under 6.5 alternate lines, as they are being promoted to main lines.

#### When `is_main` Filter is Not Set:

You will receive these events:

1. `{event: "odds", data: {"data":[{"bet_name": "Over 5.5", "is_main": False, "bet_price": -120, ...}]}}`
2. `{event: "odds", data: {"data":[{"bet_name": "Under 5.5", "is_main": False, "bet_price": +120, ...}]}}`
3. `{event: "odds", data: {"data":[{"bet_name": "Over 6.5", "is_main": True, "bet_price": -110, ...}]}}`
4. `{event: "odds", data: {"data":[{"bet_name": "Under 6.5", "is_main": True, "bet_price": +110, ...}]}}`

**Important:** You will NOT receive locked events for any of the original lines since they are all being transformed rather than removed.

### Key Takeaways for Line Movement Handling

1. **No Locked Events for Line Transitions:** When lines move from main to alternate status or vice versa, you won't receive `locked-odds` events for the transitioning lines.

2. **Only True Removals Generate Locked Events:** `locked-odds` events are only sent when odds are actually suspended or removed from the board, not when they change status or pricing.

3. **Filter Impact:** Your `is_main` filter setting significantly affects which events you'll receive during line movements.

4. **State Management:** Implement proper state management to handle these transitions correctly in your application, especially when tracking both main and alternate lines.

This comprehensive documentation provides all the technical details needed to successfully implement and maintain connections to the OpticOdds streaming API, handle various event types, and properly manage line movement scenarios.