# OpticOdds API - Copilot Grader Odds Endpoint

## Overview

### Description
This API endpoint retrieves the graded result of a specific bet using the OpticOdds Copilot system. The endpoint allows users to check the settlement status and outcome of previously placed bets by providing the unique identifier of the copilot odd.

## Endpoint Details

### HTTP Method
`GET`

### Base URL
```
https://api.opticodds.com/api/v3/copilot/grader/odds
```

### Full Endpoint URL Structure
```
https://api.opticodds.com/api/v3/copilot/grader/odds?id={copilot_odd_id}
```

## Parameters

### Required Parameters

#### id (Query Parameter)
- **Type**: String
- **Required**: Yes
- **Description**: The unique identifier of the copilot odd you want to grade. This parameter specifies which particular bet outcome you want to retrieve the graded result for.
- **Location**: Query string parameter
- **Example Value**: `10084DFECD1BD:1st_half_moneyline:fujian_sturgeons`

### Parameter Usage Notes
- For a comprehensive list of all available parameters and their specifications, users should refer to the complete parameter documentation provided at the bottom of the original API documentation page.
- The `id` parameter must match exactly with the copilot odd identifier that was generated when the original bet was placed or analyzed.

## Response Structure

### Response Format
The API returns a JSON response containing an array of graded bet results within a `data` object.

### Response Schema

```json
{
  "data": [
    {
      "id": "string",
      "status": "string", 
      "settled_at": "string (ISO 8601 datetime)"
    }
  ]
}
```

### Response Field Descriptions

#### data
- **Type**: Array of Objects
- **Description**: Contains an array of graded bet result objects. Each object represents a single bet outcome with its settlement details.

#### id
- **Type**: String
- **Description**: The complete identifier of the copilot odd that was graded. This includes additional formatting and prefixes compared to the input parameter.
- **Example**: `"1:-1:0084DFECD1BD:1st_half_moneyline:fujian_sturgeons"`

#### status
- **Type**: String (Enumerated Values)
- **Description**: The final settlement status of the bet, indicating whether the wager was successful, unsuccessful, or resulted in other specific outcomes.

#### settled_at
- **Type**: String (ISO 8601 DateTime Format)
- **Description**: The precise timestamp indicating when the bet was officially settled and graded by the system.
- **Format**: ISO 8601 datetime string with timezone information
- **Example**: `"2024-10-23T13:58:23.363"`

## Status Values

The `status` field can contain the following possible values, each representing a different bet outcome:

### Standard Settlement Statuses

#### Won
- **Description**: The bet is settled as a win
- **Meaning**: The wagered prediction was correct and the bet resulted in a profitable outcome for the bettor
- **Payout**: Full winning amount based on the original odds

#### Lost  
- **Description**: The bet is settled as a loss
- **Meaning**: The wagered prediction was incorrect and the bet resulted in a loss of the stake amount
- **Payout**: No payout; stake is forfeited

#### Refunded
- **Description**: The bet is settled as a push
- **Meaning**: The outcome resulted in neither a win nor a loss, typically due to the exact result matching the betting line or due to event cancellation
- **Payout**: Original stake amount is returned to the bettor

### Asian Market Specific Statuses

#### Half Won
- **Description**: Applies specifically for Asian handicap markets
- **Meaning**: Part of the bet won while the other part was refunded, typically occurring in quarter-line Asian handicap bets
- **Payout**: Partial winning amount plus partial stake refund

#### Half Lost
- **Description**: Applies specifically for Asian handicap markets  
- **Meaning**: Part of the bet lost while the other part was refunded, typically occurring in quarter-line Asian handicap bets
- **Payout**: Partial stake loss with partial stake refund

## Example Usage

### Sample Request
```http
GET https://api.opticodds.com/api/v3/copilot/grader/odds?id=10084DFECD1BD:1st_half_moneyline:fujian_sturgeons
```

### Sample Response
```json
{
  "data": [
    {
      "id": "1:-1:0084DFECD1BD:1st_half_moneyline:fujian_sturgeons",
      "status": "Lost",
      "settled_at": "2024-10-23T13:58:23.363"
    }
  ]
}
```

### Example Breakdown
In this example:
- **Request ID**: `10084DFECD1BD:1st_half_moneyline:fujian_sturgeons`
- **Response ID**: `1:-1:0084DFECD1BD:1st_half_moneyline:fujian_sturgeons` (note the additional prefix formatting)
- **Outcome**: The bet was settled as "Lost"
- **Settlement Time**: October 23, 2024 at 13:58:23.363 (likely UTC timezone)
- **Bet Type**: First half moneyline bet on Fujian Sturgeons team

## Implementation Notes

### Error Handling Considerations
- Ensure proper handling of cases where the provided `id` parameter does not match any existing copilot odd
- Implement appropriate timeout handling for API requests
- Consider rate limiting implications when making multiple grader requests

### Data Processing Recommendations
- Parse the `settled_at` timestamp appropriately for your application's timezone requirements
- Implement proper status handling logic for all five possible status values
- Store the complete response `id` for future reference, as it may differ from the input parameter format

### Integration Best Practices
- Cache graded results to minimize unnecessary API calls for already settled bets
- Implement proper authentication and API key management
- Use appropriate HTTP status code handling for various API response scenarios
- Consider implementing webhooks or polling strategies for real-time bet settlement notifications