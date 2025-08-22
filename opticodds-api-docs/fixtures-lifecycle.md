# Fixtures Lifecycle API Documentation

## Introduction

In the OpticOdds API, the term "fixture" is used throughout to reference a single matchup/game/event. If you are coming from the v2 API, this Fixture model is a combination of the old Schedule and Game model.

## Fixture Status Values

The API supports the following fixture status values that represent different states in a game's lifecycle:

- **"live"** - The fixture is currently in progress
- **"half"** - The fixture is at halftime or between periods
- **"unplayed"** - The fixture has not yet started
- **"completed"** - The fixture has finished
- **"cancelled"** - The fixture has been cancelled
- **"suspended"** - The fixture has been temporarily suspended
- **"delayed"** - The fixture has been delayed from its original start time

## Fixture State Machine

The fixture lifecycle follows a defined state machine that outlines the possible transitions between different statuses. Understanding these transitions is crucial for proper handling of fixture data in your applications.

### State Transition Flow

The images referenced in the documentation show the complete state machine diagram that illustrates:

1. **Initial States**: Fixtures typically start in the "unplayed" status
2. **Active States**: Transitions through "live" and potentially "half" during gameplay
3. **Terminal States**: Final states like "completed" or "cancelled"
4. **Exception States**: Temporary states like "suspended" or "delayed" that can transition back to other states

### Important Notes

- The state machine represents the most common pathways for fixture status changes
- If you encounter a status transition that is not represented in the documented flow, this may indicate a bug or unexpected issue
- Such cases should be reported to OpticOdds support for investigation
- All status changes are tracked and updated in real-time through the API

### API Behavior

When working with fixtures, your application should:

1. **Handle All Status Values**: Ensure your code can process all possible status values
2. **Monitor Status Changes**: Poll or stream fixture updates to catch status transitions
3. **Implement Proper Error Handling**: Account for unexpected status transitions
4. **Cache Appropriately**: Consider caching strategies based on fixture status (e.g., completed fixtures change less frequently)

This lifecycle management is essential for applications that depend on accurate, real-time sports data and need to handle the dynamic nature of sporting events.