Looking at the provided HTML file, I can see this is actually a **documentation page** for OpticOdds' "Common Issues" section rather than a specific API endpoint documentation. The content describes common problems users face when working with the OpticOdds API, but it doesn't contain actual API endpoint specifications.

However, based on the content and the extensive sidebar navigation visible in the HTML, I can extract information about the general API structure and common usage patterns:

# OpticOdds API - Common Issues Documentation

## Overview
This documentation page describes common issues that users experience when working with the OpticOdds API. While this specific page doesn't contain endpoint details, it provides important implementation guidance.

## Common API Usage Patterns

### 1. Multiple Parameters
**Pattern**: When passing multiple values for the same parameter, repeat the parameter name:
```
&sportsbook=DraftKings&sportsbook=Fanduel
```

### 2. URL Encoding Requirements
**Critical Implementation Detail**: All query parameters must be properly URL encoded.

**Common Issue**: Parameters containing special characters (especially `+`) will not return expected results if not properly encoded.

**Example Problem and Solution**:
- ❌ **Incorrect**: `&market=Player Passing + Rushing Yards`
- ✅ **Correct**: `&market=Player%20Passing%20%2B%20Rushing%20Yards`

**Encoding Rules**:
- Replace `+` with `%2B`
- Replace spaces with `%20`
- Follow standard URL encoding practices for all special characters

### 3. Pagination Structure
**Response Format**: Most OpticOdds API endpoints return paginated data in this structure:

```json
{
  "data": [...],
  "page": 1,
  "total_pages": 7
}
```

**Pagination Parameters**:
- `page`: Current page number (starts at 1)
- `total_pages`: Total number of pages available
- Use these values to navigate through large datasets

## Available API Endpoints (from sidebar navigation)

Based on the navigation structure, the OpticOdds API includes these endpoint categories:

### Authentication & Setup
- Authentication endpoints
- Getting Started guides

### Common Endpoints
- `/sports` - GET - Retrieve available sports
- `/sports/active` - GET - Get currently active sports
- `/leagues` - GET - Get league information
- `/leagues/active` - GET - Get active leagues
- `/sportsbooks` - GET - Get sportsbook information
- `/sportsbooks/active` - GET - Get active sportsbooks
- `/sportsbooks/last-polled` - GET - Get last polling times
- `/markets` - GET - Get available betting markets
- `/markets/active` - GET - Get active markets
- `/markets/settleable` - GET - Get markets that can be settled

### Teams & Players (Squads)
- `/teams` - GET - Get team information
- `/players` - GET - Get player information

### Fixtures & Events
- `/fixtures` - GET - Get fixture information
- `/fixtures/active` - GET - Get active fixtures
- `/tournaments` - GET - Get tournament data
- `/conferences` - GET - Get conference information
- `/divisions` - GET - Get division data

### Odds Data
- `/fixtures/odds` - GET - Get current odds for fixtures
- `/fixtures/odds/historical` - GET - Get historical odds data

### Results
- `/fixtures/results` - GET - Get fixture results
- `/fixtures/player-results` - GET - Get player-specific results
- `/tournaments/results` - GET - Get tournament results
- `/fixtures/player-results/last-x` - GET - Get recent player results
- `/fixtures/results/head-to-head` - GET - Get head-to-head results

### Futures Betting
- `/futures` - GET - Get futures markets
- `/futures/odds` - GET - Get futures odds

### Grader Services
- `/grader/odds` - GET - Get grading odds
- `/grader/futures` - GET - Get futures grading

### Injuries
- `/injuries` - GET - Get injury reports

### Parlay
- `/parlay/odds` - POST - Calculate parlay odds

### Streaming Data
- `/stream/odds/{sport}` - GET - Stream live odds by sport
- `/stream/results/{sport}` - GET - Stream results by sport

### Copilot Features
- `/copilot/fixtures/odds` - GET - Copilot odds data
- `/copilot/grader/odds` - GET - Copilot grading
- `/stream/copilot/{sport}/odds` - GET - Copilot streaming
- `/copilot/parlay/odds` - GET - Copilot parlay odds
- `/copilot/queue/start` - POST - Start copilot queue
- `/copilot/queue/stop` - POST - Stop copilot queue
- `/copilot/queue/status` - GET - Check queue status
- `/copilot/fixtures/odds/historical` - GET - Historical copilot odds

### Queue Management
- `/fixture/results/queue/start` - POST - Start results queue
- `/fixture/results/queue/stop` - POST - Stop results queue
- `/fixture/results/queue/status` - GET - Check queue status

## Authentication
The API uses API key authentication with two possible methods:
- Header: `X-Api-Key`
- Query parameter: `key`

## Important Implementation Notes

1. **Always URL encode parameters** - This is the most common source of API issues
2. **Use pagination properly** - Check `total_pages` to avoid missing data
3. **Handle multiple parameter values correctly** - Repeat parameter names for multiple values
4. **Monitor rate limits** - The API likely has rate limiting (though specifics aren't provided in this page)

This documentation page serves as a troubleshooting guide for developers implementing the OpticOdds API, focusing on the most common mistakes and proper parameter handling techniques.