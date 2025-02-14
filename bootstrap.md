# Fantasy Premier League API Documentation

## Overview

The **Fantasy Premier League (FPL) API** provides structured data for the game, including teams, players, events, chips, and game settings.

- **Base URL:** `https://fantasy.premierleague.com/api`
- **Version:** 1.0.0

---

## **Bootstrap API**


#### `GET /bootstrap-static`

Retrieves all essential FPL data, including game settings, teams, players, and events.

#### **Response:**

```json
{
  "events": [...],
  "chips": [...],
  "game_settings": {...},
  "game_config": {...},
  "phases": [...],
  "teams": [...],
  "total_players": ...,
  "element_stats": [...],
  "element_types": [...],
  "elements": [...]
}
```

# Core Structure

The full response contains these key objects.

# Fantasy Premier League API Response Structure

The response contains various key objects that provide game-related data.

## Field Descriptions
| Object           | Type      | Description |
|-----------------|----------|-------------|
| `chips`         | `array`   | Special gameplay chips available to managers. |
| `events`        | `array`   | List of gameweeks, including schedule and status. |
| `game_settings` | `object`  | Global game rules and configuration. |
| `game_config`   | `object`  | Additional game configuration parameters. |
| `phases`        | `array`   | Season phases and their associated gameweeks. |
| `teams`         | `array`   | Premier League team metadata. |
| `total_players` | `integer` | Total number of players registered in the game. |
| `element_stats` | `array`   | List of statistical categories for player performance. |
| `element_types` | `array`   | Definitions of player positions (GK, DEF, MID, FWD, MGR). |
| `elements`      | `array`   | Player-specific data, including stats and ownership. |

---

# Fantasy Premier League API - Response Objects

## 1. Chips

Represents special gameplay chips available to managers.

### **Fields:**

| Field         | Type     | Description                                                     |
| ------------- | -------- | --------------------------------------------------------------- |
| `id`          | `int`    | Unique identifier for the chip (e.g., 1 = Wildcard)             |
| `name`        | `string` | Chip name (e.g., "wildcard", "manager")                         |
| `number`      | `int`    | Number of times this chip can be used in a season (typically 1) |
| `start_event` | `int`    | First gameweek the chip becomes available                       |
| `stop_event`  | `int`    | Last gameweek the chip can be used                              |
| `chip_type`   | `string` | Type of chip effect (e.g., "transfer")                          |
| `overrides`   | `object` | Rules modified when this chip is activated (see details below)  |

---

### **Overrides Sub-Object**

Modifies game rules when the chip is active. May include:

- `rules`: Object with key-value pairs (e.g., `"squad_squadsize": 16` for the **Manager** chip).
- `element_types`: Array of player/manager position configurations.
- `pick_multiplier`: Always `null` in current data.

### **Example Chip: Manager**

```json
{
  "id": 6,
  "name": "manager",
  "number": 1,
  "start_event": 24,
  "stop_event": 38,
  "chip_type": "transfer",
  "overrides": {
    "rules": { "squad_squadsize": 16 },
    "element_types": [
      {
        "id": 5,
        "plural_name": "Managers",
        "singular_name": "Manager",
        "squad_select": 1
      }
    ]
  }
}
```

## 2. Events

**Path:**  
`GET https://fantasy.premierleague.com/api/bootstrap-static/`  
→ Look for the `"events"` key in the response.

**Contains:**  
38 items (one per Premier League gameweek)

---

## Event Object Structure

Each event object represents a gameweek and includes the following fields:

| Field                | Type        | Description                                                        |
|----------------------|-------------|--------------------------------------------------------------------|
| `id`                 | int         | Gameweek number (1-38)                                               |
| `name`               | string      | Display name (e.g., "Gameweek 1")                                    |
| `deadline_time`      | ISO 8601    | UTC deadline for team changes                                        |
| `deadline_time_epoch`| int         | Deadline as Unix timestamp                                           |
| `average_entry_score`| int         | Average points scored by all teams                                   |
| `highest_score`      | int         | Best individual team score                                           |
| `finished`           | bool        | Whether gameweek results are final                                   |
| `data_checked`       | bool        | Whether stats/points have been verified                              |
| `is_previous`        | bool        | Indicates the immediately preceding gameweek                         |
| `is_current`         | bool        | Indicates the currently active gameweek                              |
| `is_next`            | bool        | Indicates the next upcoming gameweek                                 |
| `chip_plays`         | array[obj]  | Chip usage statistics (see breakdown below)                          |
| `most_selected`      | int         | Player ID of the most selected player                                |
| `most_transferred_in`| int         | Player ID with the most transfers IN                                 |
| `top_element`        | int         | Player ID of the highest-scoring player                              |
| `top_element_info`   | object      | An object containing `{ id: [player_id], points: [points] }`          |
| `most_captained`     | int         | Player ID most frequently captained                                  |
| `most_vice_captained`| int         | Player ID most frequently vice-captained                             |
| `transfers_made`     | int         | Total transfers made by all managers                                  |
| `ranked_count`       | int         | Number of teams included in ranked leagues                            |

---

## Chip Plays Sub-Object

The `chip_plays` sub-object tracks chip usage across all managers. Each item in this array provides:

- **`chip_name`**: Name of the chip (e.g., "bboost", "3xc").
- **`num_played`**: Number of times the chip has been played.

### **Example:**
```json
"chip_plays": [
  {"chip_name": "bboost", "num_played": 144974},  // Bench Boost
  {"chip_name": "3xc", "num_played": 221430}       // Triple Captain
]



## 5. Phases

Defines scoring periods in the Fantasy Premier League (FPL) season.

## **Fields:**

| Field           | Type     | Description                                           |
| --------------- | -------- | ----------------------------------------------------- |
| `id`            | `int`    | Unique identifier for the phase (e.g., `1` = Overall) |
| `name`          | `string` | Name of the phase (e.g., `"August"`)                  |
| `start_event`   | `int`    | First gameweek included in this phase                 |
| `stop_event`    | `int`    | Last gameweek included in this phase                  |
| `highest_score` | `int`    | Highest points achieved in this phase                 |

---

## **Example Phase: August**

```json
{
  "id": 2,
  "name": "August",
  "start_event": 1,
  "stop_event": 3,
  "highest_score": 309
}
```

## 6. Chips
Contains Premier League team information and metrics.

## **Fields:**
| Field                    | Type    | Description |
|--------------------------|--------|-------------|
| `id`                     | `int`   | Unique team identifier (1-20) |
| `name`                   | `string` | Full team name (e.g., `"Arsenal"`) |
| `short_name`             | `string` | 3-letter abbreviation (e.g., `"ARS"`) |
| `code`                   | `int`   | Numeric team code |
| `position`               | `int`   | Current league position |
| `played`                 | `int`   | Matches played |
| `win/draw/loss`          | `int`   | Count of wins/draws/losses |
| `points`                 | `int`   | League points |
| `strength`               | `int`   | Overall strength rating (1-5, where 5 = strongest) |
| `strength_overall_home`  | `int`   | Attack/defense strength metric for home matches |
| `strength_overall_away`  | `int`   | Attack/defense strength metric for away matches |
| `strength_attack_home`   | `int`   | Offensive strength metric for home matches |
| `strength_attack_away`   | `int`   | Offensive strength metric for away matches |
| `strength_defence_home`  | `int`   | Defensive strength metric for home matches |
| `strength_defence_away`  | `int`   | Defensive strength metric for away matches |
| `unavailable`            | `bool`  | Whether team is temporarily unavailable |
| `pulse_id`               | `int`   | Internal identifier for news/pulse updates |

---

## **Example Team: Arsenal**
```json
{
  "code": 3,
  "id": 1,
  "name": "Arsenal",
  "short_name": "ARS",
  "strength": 4,
  "strength_overall_home": 1235,
  "strength_attack_away": 1370,
  "position": 2
}
```

