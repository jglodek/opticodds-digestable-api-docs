# OpticOdds API Getting Started Guide

The HTML file provided appears to be a documentation landing page rather than specific API endpoint documentation. This is the "Getting Started" guide for the OpticOdds API, which provides an overview of the API structure and recommended onboarding flow rather than detailed endpoint specifications.

## API Overview

**Base Information:**
- **API Name:** OpticOdds API
- **Version:** 3.0
- **Base URL:** Not explicitly specified in this page (this is a getting started guide)
- **Description:** All-in-one source for real-time and historical sports betting data

## Authentication Requirements

**Authentication Method:** API Key
- **Header Name:** `X-Api-Key`
- **Alternative Parameter:** `key`
- **Access:** Requires a license key - request access via the [contact form](https://opticodds.com/contact)

## API Structure & Endpoints Overview

Based on the documentation structure visible in the sidebar, the OpticOdds API is organized into the following main categories:

### 1. Common Endpoints
- `GET /sports` - List all sports
- `GET /sports/active` - List active sports only
- `GET /leagues` - List all leagues
- `GET /leagues/active` - List active leagues only
- `GET /sportsbooks` - List all sportsbooks
- `GET /sportsbooks/active` - List active sportsbooks only
- `GET /sportsbooks/last-polled` - Get last polling timestamps for sportsbooks
- `GET /markets` - List all betting markets
- `GET /markets/active` - List active markets only
- `GET /markets/settleable` - List markets that can be settled

### 2. Squads (Teams & Players)
- `GET /teams` - List teams
- `GET /players` - List players

### 3. Fixtures (Games & Schedules)
- `GET /fixtures` - List fixtures/games
- `GET /fixtures/active` - List active fixtures only
- `GET /tournaments` - List tournaments
- `GET /conferences` - List conferences
- `GET /divisions` - List divisions

### 4. Odds
- `GET /fixtures/odds` - Get current odds for fixtures
- `GET /fixtures/odds/historical` - Get historical odds data

### 5. Results
- `GET /fixtures/results` - Get game results
- `GET /fixtures/player-results` - Get player performance results
- `GET /tournaments/results` - Get tournament results
- `GET /fixtures/player-results/last-x` - Get recent player results
- `GET /fixtures/results/head-to-head` - Get head-to-head results

### 6. Futures (Long-term Markets)
- `GET /futures` - List futures markets
- `GET /futures/odds` - Get futures odds

### 7. Grader (Settlement)
- `GET /grader/odds` - Get settlement-ready odds data
- `GET /grader/futures` - Get settlement-ready futures data

### 8. Injuries
- `GET /injuries` - Get player injury data

### 9. Parlay
- `POST /parlay/odds` - Calculate parlay odds for combinations

### 10. Stream (Real-time Updates)
- `GET /stream/odds/{sport}` - Stream live odds updates via Server-Sent Events
- `GET /stream/results/{sport}` - Stream live results via Server-Sent Events

### 11. Copilot (Automated Trading Service)
- `GET /copilot/fixtures/odds` - Get structured odds for trading
- `GET /copilot/grader/odds` - Get structured settlement data
- `GET /stream/copilot/{sport}/odds` - Stream copilot odds updates
- `GET /copilot/parlay/odds` - Get structured parlay odds
- `POST /copilot/queue/start` - Start automated data queue
- `POST /copilot/queue/stop` - Stop automated data queue
- `GET /copilot/queue/status` - Check queue status
- `GET /copilot/fixtures/odds/historical` - Get historical copilot odds

### 12. Queue Management
- `POST /fixture/results/queue/start` - Start results queue
- `POST /fixture/results/queue/stop` - Stop results queue
- `GET /fixture/results/queue/status` - Check results queue status

## Recommended Integration Flow

The documentation suggests following this order when exploring the API:

1. **Common** - Start with foundational resources (sports, leagues, sportsbooks, markets)
2. **Squads** - Explore teams and players data
3. **Fixtures** - Access game schedules and information
4. **Odds** - Pull current and historical betting odds
5. **Results** - Access game outcomes and player performance
6. **Futures** - Work with long-term betting markets
7. **Grader** - Implement automated settlement logic
8. **Injuries** - Track player availability
9. **Parlay** - Handle combination betting
10. **Stream** - Implement real-time data feeds
11. **Copilot** - Use automated trading features

## Key Features

- **Real-time Data:** Live odds and results streaming via Server-Sent Events
- **Historical Data:** Access to historical odds and results
- **Settlement Tools:** Automated grading and settlement capabilities
- **Parlay Support:** Calculate combination bet odds
- **Injury Tracking:** Up-to-date player injury information
- **Multiple Sports:** Coverage across various sports and leagues
- **Trading Integration:** Structured data for automated trading systems

## Support & Documentation

- **Discussion Forum:** Available for questions and community support
- **Contact:** Direct support via contact form on OpticOdds website
- **Additional Documentation:** Authentication, Fixtures Lifecycle, and Common Issues guides available

**Note:** This appears to be an introductory page. For detailed endpoint specifications, request/response schemas, and examples, you would need to access the individual endpoint documentation pages listed in the sidebar navigation.