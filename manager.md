# Fantasy Premier League API Documentation

## Overview

The **Fantasy Premier League (FPL) API** provides structured data for the game, including teams, players, events, chips, and game settings.

- **Base URL:** `https://fantasy.premierleague.com/api`
- **Version:** 1.0.0

---

## **Manager Summary API**

#### `GET /entry/{manager_id}/`

Returns a summary of the data on a given manager.

#### **Sample Response:**

```json
{
  "id": 11289294,
  "joined_time": "2025-02-05T16:48:44.126752Z",
  "started_event": 25,
  "favourite_team": 12,
  "player_first_name": "Mahmud Hasan",
  "player_last_name": "Sourov",
  "player_region_id": 18,
  "player_region_name": "Bangladesh",
  "player_region_iso_code_short": "BD",
  "player_region_iso_code_long": "BGD",
  "years_active": 0,
  "summary_overall_points": null,
  "summary_overall_rank": null,
  "summary_event_points": null,
  "summary_event_rank": null,
  "current_event": 24,
  "leagues": {
    "classic": [
        {
            {
                "id": 12,
                "name": "Liverpool",
                "short_name": "team-12",
                "created": "2024-07-17T11:51:46.332200Z",
                "closed": false,
                "rank": null,
                "max_entries": null,
                "league_type": "s",
                "scoring": "c",
                "admin_entry": null,
                "start_event": 1,
                "entry_can_leave": false,
                "entry_can_admin": false,
                "entry_can_invite": false,
                "has_cup": true,
                "cup_league": 2451204,
                "cup_qualified": false,
                "rank_count": 2007955,
                "entry_percentile_rank": null,
                "active_phases": [
                    {
                    "phase": 1,
                    "rank": 0,
                    "last_rank": 0,
                    "rank_sort": 0,
                    "total": 0,
                    "league_id": 12,
                    "rank_count": 2007955,
                    "entry_percentile_rank": null
                    },
                ],
                "entry_rank": 0,
                "entry_last_rank": 0
                },
        }
    ],
    "h2h": [...],
    "cup": {
        "matches": [...],
        "status": {
            "qualification_event": null,
            "qualification_numbers": null,
            "qualification_rank": null,
            "qualification_state": null
        },
        "cup_league": null
    },
    "cup_matches": [...]
  },
  "name": "Narsil",
  "name_change_blocked": false,
  "entered_events": [],
  "kit": null,
  "last_deadline_bank": null,
  "last_deadline_value": null,
  "last_deadline_total_transfers": 0
}
```

## Field Descriptions

| Field                           | Type              | Description                                                      |
| ------------------------------- | ----------------- | ---------------------------------------------------------------- |
| `id`                            | integer           | Unique identifier for the manager.                               |
| `joined_time`                   | string (ISO 8601) | Timestamp when the manager joined, in ISO 8601 format.           |
| `started_event`                 | integer           | The first event (gameweek) that the manager started.             |
| `favourite_team`                | integer           | Identifier for the manager's favourite team.                     |
| `player_first_name`             | string            | The first name of the player/manager.                            |
| `player_last_name`              | string            | The last name of the player/manager.                             |
| `player_region_id`              | integer           | Identifier for the player's region.                              |
| `player_region_name`            | string            | Name of the player's region.                                     |
| `player_region_iso_code_short`  | string            | Short ISO code for the player's region (e.g., "BD").             |
| `player_region_iso_code_long`   | string            | Long ISO code for the player's region (e.g., "BGD").             |
| `years_active`                  | integer           | Number of years the manager has been active.                     |
| `summary_overall_points`        | integer or null   | Overall points summary; null if not available.                   |
| `summary_overall_rank`          | integer or null   | Overall rank summary; null if not available.                     |
| `summary_event_points`          | integer or null   | Points summary for the current event; null if not available.     |
| `summary_event_rank`            | integer or null   | Rank summary for the current event; null if not available.       |
| `current_event`                 | integer           | Identifier for the current event (gameweek).                     |
| `leagues`                       | object            | Object containing league information.                            |
| `name`                          | string            | Name of the manager/team.                                        |
| `name_change_blocked`           | boolean           | Indicates whether the manager/team name is blocked from changes. |
| `entered_events`                | array             | List of events that the manager has entered.                     |
| `kit`                           | string or null    | Kit information; can be null if not set.                         |
| `last_deadline_bank`            | number or null    | Bank amount at the last deadline; null if not available.         |
| `last_deadline_value`           | number or null    | Squad value at the last deadline; null if not available.         |
| `last_deadline_total_transfers` | integer           | Total transfers made by the deadline.                            |

## Leagues Object

The `leagues` object provides details about the various leagues the manager is involved in.

| Field         | Type   | Description                  |
| ------------- | ------ | ---------------------------- |
| `classic`     | array  | List of classic leagues      |
| `h2h`         | array  | List of head-to-head leagues |
| `cup`         | object | Cup league information       |
| `cup_matches` | array  | List of cup matches          |

## Classic League

The `classic` field is an array of objects, where each object represents a classic league. Below is the documentation for the fields within a classic league object.

| Field                   | Type                  | Description                                                                                      |
|-------------------------|-----------------------|--------------------------------------------------------------------------------------------------|
| `id`                    | integer               | Unique identifier for the league.                                                              |
| `name`                  | string                | Name of the league.                                                                             |
| `short_name`            | string                | Short name or code for the league.                                                              |
| `created`               | string (ISO 8601)     | Timestamp when the league was created.                                                         |
| `closed`                | boolean               | Indicates if the league is closed.                                                             |
| `rank`                  | integer or null       | Current rank in the league; may be null if not applicable.                                     |
| `max_entries`           | integer or null       | Maximum number of entries allowed in the league.                                               |
| `league_type`           | string                | Type of league (e.g., `"s"` for standard).                                                       |
| `scoring`               | string                | Scoring system used (e.g., `"c"` for classic).                                                   |
| `admin_entry`           | integer or null       | Admin's entry ID, if applicable.                                                               |
| `start_event`           | integer               | The event number when the league started.                                                      |
| `entry_can_leave`       | boolean               | Indicates whether an entry can leave the league.                                               |
| `entry_can_admin`       | boolean               | Indicates whether an entry can administer the league.                                          |
| `entry_can_invite`      | boolean               | Indicates whether an entry can invite others to the league.                                    |
| `has_cup`               | boolean               | Indicates if the league has an associated cup.                                                 |
| `cup_league`            | integer               | Identifier for the associated cup league.                                                      |
| `cup_qualified`         | boolean               | Indicates if the entry is qualified for the cup.                                               |
| `rank_count`            | integer               | Total number of entries in the league ranking.                                                 |
| `entry_percentile_rank` | integer or null       | The percentile rank of the entry within the league; may be null.                               |
| `active_phases`         | array                 | List of active phases within the league. See details below.                                    |
| `entry_rank`            | integer               | The current entry rank within the league.                                                      |
| `entry_last_rank`       | integer               | The entry's rank from the previous phase or event.                                             |

### Active Phases (inside Classic League)

Each object in the `active_phases` array represents a specific phase in the league.

| Field                   | Type            | Description                                                                                       |
|-------------------------|-----------------|---------------------------------------------------------------------------------------------------|
| `phase`                 | integer         | The phase number.                                                                                 |
| `rank`                  | integer         | Current rank within the phase.                                                                    |
| `last_rank`             | integer         | Rank from the previous update in the phase.                                                       |
| `rank_sort`             | integer         | A value used for sorting ranks.                                                                   |
| `total`                 | integer         | Total number of entries or points in this phase.                                                  |
| `league_id`             | integer         | Identifier for the league to which this phase belongs.                                            |
| `rank_count`            | integer         | Total number of entries considered in this phase.                                                 |
| `entry_percentile_rank` | integer or null | The entry's percentile rank within this phase; may be null.                                       |

---
## Cup League

The `cup` field is an object that contains details about cup competitions related to the league.

| Field        | Type                  | Description                                                              |
|--------------|-----------------------|--------------------------------------------------------------------------|
| `matches`    | array                 | List of cup matches (empty array if no matches).                        |
| `status`     | object                | Object containing the cup qualification status.                        |
| `cup_league` | integer or null       | Identifier for the cup league; may be null if not applicable.             |

### Cup Status Object

The `status` object within the `cup` field provides information about cup qualification.

| Field                   | Type                  | Description                                                                          |
|-------------------------|-----------------------|--------------------------------------------------------------------------------------|
| `qualification_event`   | integer or null       | The event number associated with qualification; may be null.                         |
| `qualification_numbers` | *varies* or null      | Qualification numbers; the type can vary, and may be null.                           |
| `qualification_rank`    | integer or null       | The qualification rank; may be null.                                                 |
| `qualification_state`   | string or null        | The state of qualification; may be null.                                             |

---
## H2H League

The `h2h` field is an array of objects representing head-to-head leagues. Each object includes the following fields:

| Field                   | Type                   | Description                                                                                         |
|-------------------------|------------------------|-----------------------------------------------------------------------------------------------------|
| `id`                    | integer                | Unique identifier for the h2h league.                                                              |
| `name`                  | string                 | Name of the h2h league.                                                                             |
| `short_name`            | string or null         | Short name for the league; may be null if not provided.                                             |
| `created`               | string (ISO 8601)      | Timestamp when the league was created.                                                              |
| `closed`                | boolean                | Indicates if the league is closed.                                                                  |
| `rank`                  | integer or null        | Current rank in the league; may be null if not applicable.                                          |
| `max_entries`           | integer or null        | Maximum number of entries allowed in the league.                                                  |
| `league_type`           | string                 | Type of league (e.g., `"x"` for h2h leagues).                                                       |
| `scoring`               | string                 | Scoring system used (e.g., `"h"` for head-to-head).                                                 |
| `admin_entry`           | integer or null        | Entry ID of the league admin.                                                                       |
| `start_event`           | integer                | The event number when the league started.                                                         |
| `entry_can_leave`       | boolean                | Indicates whether an entry can leave the league.                                                  |
| `entry_can_admin`       | boolean                | Indicates whether an entry can administer the league.                                             |
| `entry_can_invite`      | boolean                | Indicates whether an entry can invite others to the league.                                       |
| `has_cup`               | boolean                | Indicates if the league has an associated cup competition.                                        |
| `cup_league`            | integer or null        | Identifier for the associated cup league, if any.                                                 |
| `cup_qualified`         | boolean or null        | Indicates if the entry is qualified for the cup competition.                                      |
| `rank_count`            | integer or null        | Total number of entries in the league ranking.                                                    |
| `entry_percentile_rank` | integer or null        | The percentile rank of the entry within the league; may be null.                                  |
| `active_phases`         | array                  | List of active phases within the league (empty if none).                                          |
| `entry_rank`            | integer                | The current entry rank within the league.                                                         |
| `entry_last_rank`       | integer                | The entry's rank from the previous update.                                                        |

---
## Cup Matches

The `cup_matches` field is an array of objects representing details about cup matches. Each object contains information about the competing entries, match outcomes, and additional match metadata.

| Field                  | Type               | Description                                                                                         |
|------------------------|--------------------|-----------------------------------------------------------------------------------------------------|
| `id`                   | integer            | Unique identifier for the cup match.                                                              |
| `entry_1_entry`        | integer            | Entry ID for the first team/participant.                                                          |
| `entry_1_name`         | string             | Name of the first team.                                                                           |
| `entry_1_player_name`  | string             | Player name of the first team's manager.                                                          |
| `entry_1_points`       | integer            | Points scored by the first team in the match.                                                     |
| `entry_1_win`          | integer            | Number of wins for the first team in the match context.                                           |
| `entry_1_draw`         | integer            | Number of draws for the first team in the match context.                                          |
| `entry_1_loss`         | integer            | Number of losses for the first team in the match context.                                         |
| `entry_1_total`        | integer            | Total points or aggregate score for the first team (if applicable).                               |
| `entry_2_entry`        | integer            | Entry ID for the second team/participant.                                                         |
| `entry_2_name`         | string             | Name of the second team.                                                                          |
| `entry_2_player_name`  | string             | Player name of the second team's manager.                                                         |
| `entry_2_points`       | integer            | Points scored by the second team in the match.                                                    |
| `entry_2_win`          | integer            | Number of wins for the second team in the match context.                                          |
| `entry_2_draw`         | integer            | Number of draws for the second team in the match context.                                         |
| `entry_2_loss`         | integer            | Number of losses for the second team in the match context.                                        |
| `entry_2_total`        | integer            | Total points or aggregate score for the second team (if applicable).                              |
| `is_knockout`          | boolean            | Indicates whether the match is in a knockout format.                                              |
| `league`               | integer            | Identifier of the league that the cup match belongs to.                                           |
| `winner`               | integer            | Entry ID of the winning team.                                                                     |
| `seed_value`           | integer or null    | Seeding value for the match; may be null if not applicable.                                       |
| `event`                | integer            | The event or round number associated with the match.                                              |
| `tiebreak`             | (varies) or null   | Details regarding tiebreak criteria; may be null if not applicable.                               |
| `is_bye`               | boolean            | Indicates if the match was a bye.                                                                 |
| `knockout_name`        | string             | Name of the knockout stage (e.g., "Round of 8388608").                                            |

---