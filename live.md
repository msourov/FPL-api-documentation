# Fantasy Premier League API Documentation

## Overview

The **Fantasy Premier League (FPL) API** provides structured data for the game, including teams, players, events, chips, and game settings.

- **Base URL:** `https://fantasy.premierleague.com/api`
- **Version:** 1.0.0

---

## **Live API**

#### `GET /event/{event_id}/live`

Returns statistics on every football player in FPL for the specified gameweek.

#### **Sample Response:**

```json
{
  "elements": [
    {
      "id": 1,
      "stats": {
        "minutes": 0,
        "goals_scored": 0,
        "assists": 0,
        "clean_sheets": 0,
        "goals_conceded": 0,
        "own_goals": 0,
        "penalties_saved": 0,
        "penalties_missed": 0,
        "yellow_cards": 0,
        "red_cards": 0,
        "saves": 0,
        "bonus": 0,
        "bps": 0,
        "influence": "0.0",
        "creativity": "0.0",
        "threat": "0.0",
        "ict_index": "0.0",
        "starts": 0,
        "expected_goals": "0.00",
        "expected_assists": "0.00",
        "expected_goal_involvements": "0.00",
        "expected_goals_conceded": "0.00",
        "mng_win": 0,
        "mng_draw": 0,
        "mng_loss": 0,
        "mng_underdog_win": 0,
        "mng_underdog_draw": 0,
        "mng_clean_sheets": 0,
        "mng_goals_scored": 0,
        "total_points": 0,
        "in_dreamteam": false
      },
      "explain": [
        {
          "fixture": 39,
          "stats": [
            {
              "identifier": "minutes",
              "points": 0,
              "value": 0,
              "points_modification": 0
            }
          ]
        }
      ],
      "modified": false
    }
  ]
}
```

## Field Descriptions

## Elements Array

Each object in the `elements` array represents an individual entity (such as a player) with its own statistics and explanation details.

| Field      | Type    | Description                                                                                                              |
| ---------- | ------- | ------------------------------------------------------------------------------------------------------------------------ |
| `id`       | integer | Unique identifier for the element.                                                                                       |
| `stats`    | object  | An object containing 31 statistical metrics for the element. (Details of these metrics are similar to the global stats.) |
| `explain`  | array   | An array of explanation objects related to the element. In this example, each element contains one explanation item.     |
| `modified` | boolean | Indicates whether the element's stats have been modified.                                                                |

---

## Stats Object

The `stats` object provides overall statistical metrics. Each field represents a different metric, as described below:

| Field                        | Type    | Description                                                       |
| ---------------------------- | ------- | ----------------------------------------------------------------- |
| `minutes`                    | integer | Total minutes played.                                             |
| `goals_scored`               | integer | Number of goals scored.                                           |
| `assists`                    | integer | Number of assists made.                                           |
| `clean_sheets`               | integer | Number of clean sheets.                                           |
| `goals_conceded`             | integer | Number of goals conceded.                                         |
| `own_goals`                  | integer | Number of own goals.                                              |
| `penalties_saved`            | integer | Number of penalties saved.                                        |
| `penalties_missed`           | integer | Number of penalties missed.                                       |
| `yellow_cards`               | integer | Number of yellow cards received.                                  |
| `red_cards`                  | integer | Number of red cards received.                                     |
| `saves`                      | integer | Number of saves made.                                             |
| `bonus`                      | integer | Bonus points awarded.                                             |
| `bps`                        | integer | Bonus point system rating.                                        |
| `influence`                  | string  | Influence rating (represented as a string, e.g., "0.0").          |
| `creativity`                 | string  | Creativity rating (represented as a string, e.g., "0.0").         |
| `threat`                     | string  | Threat rating (represented as a string, e.g., "0.0").             |
| `ict_index`                  | string  | ICT index rating (represented as a string, e.g., "0.0").          |
| `starts`                     | integer | Number of starts.                                                 |
| `expected_goals`             | string  | Expected goals (formatted as a string, e.g., "0.00").             |
| `expected_assists`           | string  | Expected assists (formatted as a string, e.g., "0.00").           |
| `expected_goal_involvements` | string  | Expected goal involvements (formatted as a string, e.g., "0.00"). |
| `expected_goals_conceded`    | string  | Expected goals conceded (formatted as a string, e.g., "0.00").    |
| `mng_win`                    | integer | Manager win count (or similar metric).                            |
| `mng_draw`                   | integer | Manager draw count.                                               |
| `mng_loss`                   | integer | Manager loss count.                                               |
| `mng_underdog_win`           | integer | Manager underdog win count.                                       |
| `mng_underdog_draw`          | integer | Manager underdog draw count.                                      |
| `mng_clean_sheets`           | integer | Manager clean sheets count.                                       |
| `mng_goals_scored`           | integer | Manager goals scored count.                                       |
| `total_points`               | integer | Total points accumulated.                                         |
| `in_dreamteam`               | boolean | Indicates if the element is included in the dream team.           |

---
## Explain Object


The `explain` array contains objects that provide detailed breakdowns of statistics related to specific fixtures.

| Field     | Type    | Description                                                |
| --------- | ------- | ---------------------------------------------------------- |
| `fixture` | integer | The fixture number associated with this explanation.       |
| `stats`   | array   | An array of statistical breakdown objects for the fixture. |

### Explanation Stats Object

Each object within the `stats` array inside an explanation object has the following fields:

| Field               | Type    | Description                                                                              |
|---------------------|---------|------------------------------------------------------------------------------------------|
| `identifier`        | string  | The type of statistic (e.g., "minutes").                                                 |
| `points`            | integer | Points awarded for this particular statistic.                                            |
| `value`             | number  | The value of the statistic.                                                              |
| `points_modification`| integer| Any modification applied to the points awarded for the statistic.                        |