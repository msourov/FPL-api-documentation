# Fantasy Premier League API Documentation

## Overview

The **Fantasy Premier League (FPL) API** provides structured data for the game, including teams, players, events, chips, and game settings.

- **Base URL:** `https://fantasy.premierleague.com/api`
- **Version:** 1.0.0

---

## **Manager's Team on a given gameweek API**

#### `GET /entry/{manager_id}/event/{event_id}/picks/`

Returns data on the given manager for the given gameweek and also shows the players chosen for the manager's team.

#### **Sample Response:**

```json
{
  "active_chip": null,
  "automatic_subs": [
    {
      "entry": 5428542,
      "element_in": 495,
      "element_out": 129,
      "event": 4
    }
  ],
  "entry_history": {
    "event": 4,
    "points": 50,
    "total_points": 269,
    "rank": 5443328,
    "rank_sort": 5526906,
    "overall_rank": 1853858,
    "percentile_rank": 55,
    "bank": 15,
    "value": 1004,
    "event_transfers": 0,
    "event_transfers_cost": 0,
    "points_on_bench": 1
  },
  "picks": [
    {
      "element": 201,
      "position": 1,
      "multiplier": 1,
      "is_captain": false,
      "is_vice_captain": false,
      "element_type": 1
    }
  ]
}
```

## Active Chip  

| Field        | Type    | Description                                     |
|-------------|--------|-------------------------------------------------|
| active_chip | string or null | The currently active chip (e.g., "wildcard") or null if none. |

---

## Automatic Substitutions  

The `automatic_subs` array contains details of automatic substitutions made due to injuries, non-playing players, etc.

| Field        | Type     | Description                                      |
|-------------|---------|--------------------------------------------------|
| entry       | integer | The unique identifier of the user's team entry.  |
| element_in  | integer | The ID of the player who was subbed in.          |
| element_out | integer | The ID of the player who was subbed out.        |
| event       | integer | The gameweek in which the substitution occurred. |

---

## Entry History  

The `entry_history` object provides historical data on the user's team performance in a specific gameweek.

| Field                 | Type    | Description                                      |
|----------------------|--------|--------------------------------------------------|
| event               | integer | The gameweek number.                            |
| points              | integer | Points scored in the current gameweek.         |
| total_points        | integer | Total accumulated points.                      |
| rank                | integer | The team's rank in the gameweek.               |
| rank_sort           | integer | Sorted rank for tiebreak purposes.             |
| overall_rank        | integer | The team's overall rank across all managers.   |
| percentile_rank     | integer | The team's percentile rank compared to others. |
| bank               | integer | Remaining budget after transfers.              |
| value              | integer | The team's total squad value.                  |
| event_transfers     | integer | Number of transfers made in this gameweek.    |
| event_transfers_cost| integer | Points deducted due to excess transfers.       |
| points_on_bench     | integer | Points scored by bench players.               |

---

## Picks  

The `picks` array contains details of the players selected for the team.

| Field           | Type     | Description                                           |
|----------------|---------|-------------------------------------------------------|
| element        | integer | The player's unique identifier.                       |
| position       | integer | The player's position in the lineup.                  |
| multiplier     | integer | Points multiplier (e.g., 2 for captain, 1 by default). |
| is_captain     | boolean | Indicates if the player is the captain.               |
| is_vice_captain| boolean | Indicates if the player is the vice-captain.         |
| element_type   | integer | The type of player (e.g., 1 = goalkeeper, etc.).      |

---