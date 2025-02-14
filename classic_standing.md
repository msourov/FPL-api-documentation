# Fantasy Premier League API Documentation

## Overview

The **Fantasy Premier League (FPL) API** provides structured data for the game, including teams, players, events, chips, and game settings.

- **Base URL:** `https://fantasy.premierleague.com/api`
- **Version:** 1.0.0

---

## **Classic League Standings API**

#### `GET /entry/{manager_id}/`

#### **Sample Response:**

```json
{
  "new_entries": {
    "has_next": false,
    "page": 1,
    "results": []
  },
  "last_updated_data": "2025-02-12T22:41:03Z",
  "league": {
    "id": 24234,
    "name": "Drumaness",
    "created": "2024-07-17T14:05:38.337828Z",
    "closed": false,
    "max_entries": null,
    "league_type": "x",
    "scoring": "c",
    "admin_entry": 124344,
    "start_event": 1,
    "code_privacy": "p",
    "has_cup": true,
    "cup_league": null,
    "rank": null
  },
  "standings": {
    "has_next": false,
    "page": 1,
    "results": [
      {
        "id": 29329339,
        "event_total": 99,
        "player_name": "Olan O’Regan",
        "rank": 1,
        "last_rank": 1,
        "rank_sort": 1,
        "total": 1495,
        "entry": 3306565,
        "entry_name": "got mainoo boots on",
        "has_played": true
      }
    ]
  }
}
```
## New Entries

The `new_entries` object contains pagination information for new entries.

| Field     | Type    | Description                                                    |
|-----------|---------|----------------------------------------------------------------|
| has_next  | boolean | Indicates if there is a next page of new entries available.    |
| page      | integer | The current page number for new entries.                       |
| results   | array   | An array of new entry objects (empty if no new entries exist).   |

---

## Last Updated Data

| Field               | Type              | Description                                                    |
|---------------------|-------------------|----------------------------------------------------------------|
| last_updated_data   | string (ISO 8601) | Timestamp of the last update in the data.                      |

---

## League

The `league` object provides details about the league.

| Field         | Type              | Description                                                                               |
|---------------|-------------------|-------------------------------------------------------------------------------------------|
| id            | integer           | Unique identifier for the league.                                                         |
| name          | string            | Name of the league.                                                                       |
| created       | string (ISO 8601) | Timestamp when the league was created.                                                    |
| closed        | boolean           | Indicates if the league is closed.                                                        |
| max_entries   | integer or null   | Maximum number of entries allowed in the league (null if not specified).                  |
| league_type   | string            | Type of league (e.g., "x").                                                                 |
| scoring       | string            | Scoring system used by the league (e.g., "c").                                              |
| admin_entry   | integer           | Entry ID of the league admin.                                                             |
| start_event   | integer           | The starting event (or gameweek) for the league.                                            |
| code_privacy  | string            | Privacy code for the league (e.g., "p" for private).                                        |
| has_cup       | boolean           | Indicates if the league has an associated cup competition.                                |
| cup_league    | integer or null   | Identifier for the associated cup league (if applicable).                                 |
| rank          | integer or null   | League rank (may be null if not applicable).                                               |

---

## Standings

The `standings` object provides information about the league standings.

| Field     | Type    | Description                                                           |
|-----------|---------|-----------------------------------------------------------------------|
| has_next  | boolean | Indicates if there is a next page of standings results.             |
| page      | integer | The current page number for the standings.                          |
| results   | array   | An array of standings result objects.                               |

### Standings Result Object

Each object in the `results` array represents an entry in the standings with the following fields:

| Field         | Type    | Description                                                                           |
|---------------|---------|---------------------------------------------------------------------------------------|
| id            | integer | Unique identifier for the standings entry.                                            |
| event_total   | integer | Total points earned in the current event (gameweek).                                  |
| player_name   | string  | Name of the player associated with this entry.                                        |
| rank          | integer | Current rank of the entry in the standings.                                           |
| last_rank     | integer | Rank of the entry in the previous update.                                             |
| rank_sort     | integer | Value used for sorting the rank.                                                       |
| total         | integer | Total points accumulated by the entry.                                                 |
| entry         | integer | Entry ID representing the team.                                                       |
| entry_name    | string  | Name of the team/entry.                                                                 |
| has_played    | boolean | Indicates whether the entry has played in the current event.                           |

---