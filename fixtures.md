# Fantasy Premier League API Documentation
## Overview

The **Fantasy Premier League (FPL) API** provides structured data for the game, including teams, players, events, chips, and game settings.

- **Base URL:** `https://fantasy.premierleague.com/api`
- **Version:** 1.0.0

---
## **Fixtures API**

### All fixtures
#### `GET /fixtures`

Returns an array of fixture objects. If the fixture is a future fixture, only a summary is returned such as teams, kick off time and difficulty for each team. For the past fixtures, statistics for the fixture are also returned.

#### **Sample Response:**

```json 
{
  "code": 2444470,
  "event": 1,
  "finished": true,
  "finished_provisional": true,
  "id": 1,
  "kickoff_time": "2024-08-16T19:00:00Z",
  "minutes": 90,
  "provisional_start_time": false,
  "started": true,
  "team_a": 9,
  "team_a_score": 0,
  "team_h": 14,
  "team_h_score": 1,
  "stats": [
    {
      "identifier": "goals_scored",
      "a": [],
      "h": [
        {
          "value": 1,
          "element": 389
        }
      ]
    },
    {
      "identifier": "assists",
      "a": [],
      "h": [
        {
          "value": 1,
          "element": 372
        }
      ]
    },
    {
      "identifier": "own_goals",
      "a": [],
      "h": []
    }
  ]
}
```
## Field Descriptions

| Field                  | Type     | Description                                                                       |
|------------------------|----------|-----------------------------------------------------------------------------------|
| `code`                 | integer  | A unique code representing the match or event.                                  |
| `event`                | integer  | An identifier for the event or matchday associated with the match.                |
| `finished`             | boolean  | Indicates whether the match has concluded.                                        |
| `finished_provisional` | boolean  | Indicates if the match's finished status is provisional (temporary) or final.       |
| `id`                   | integer  | The unique identifier for the match.                                              |
| `kickoff_time`         | string   | The scheduled start time of the match in ISO 8601 format (UTC).                    |
| `minutes`              | integer  | The number of minutes played in the match.                                        |
| `provisional_start_time`| boolean | Indicates whether the kickoff time is provisional.                                |
| `started`              | boolean  | Indicates whether the match has started.                                          |
| `team_a`               | integer  | The identifier for team A (Away team). |
| `team_a_score`         | integer  | The number of goals scored by team A.                                             |
| `team_h`               | integer  | The identifier for team H (Home team).                    |
| `team_h_score`         | integer  | The number of goals scored by team H.                                             |
| `stats`                | array    | A list of statistical categories for the match. Each object represents a statistic.|

---

## Stats Object Details

| Field        | Type   | Description                                                                                                                                   |
|--------------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| `identifier` | string | The type of statistic (e.g., "goals_scored", "assists", "own_goals").                                                                         |
| `a`          | array  | An array containing statistic details for team A. Each entry includes: <br> - **value (integer):** The numeric value of the statistic. <br> - **element (integer):** The identifier for the player or entity associated with the statistic. |
| `h`          | array  | An array containing statistic details for team H, structured similarly to the `a` array.                                                      |


### Fixtures by Gameweek
#### `GET /fixtures/?event={event_id}`
Similar to the all fixtures endpoint, this returns specific gameweek fixtures.