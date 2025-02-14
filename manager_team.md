# Fantasy Premier League API Documentation

## Overview

The **Fantasy Premier League (FPL) API** provides structured data for the game, including teams, players, events, chips, and game settings.

- **Base URL:** `https://fantasy.premierleague.com/api`
- **Version:** 1.0.0

---

## **Manager's Team API**

#### `GET /my-team/{manager_id}/`

Authentication is required to access this endpoint. Returns the given manager's current team, data on what chips the manager has used and when, and also the transfers made by the manager in the latest gameweek. The manager id specified must match the details you authenticate with.

#### **Sample Response:**

```json
{
  "picks": [
    {
      "element": 201,
      "position": 1,
      "multiplier": 1,
      "is_captain": false,
      "is_vice_captain": false,
      "element_type": 1,
      "selling_price": 45,
      "purchase_price": 45
    }
  ],
  "picks_last_updated": "2025-02-05T17:02:50.792811Z",
  "chips": [
    {
      "id": 2,
      "status_for_entry": "unavailable",
      "played_by_entry": [],
      "name": "wildcard",
      "number": 1,
      "start_event": 20,
      "stop_event": 38,
      "chip_type": "transfer",
      "is_pending": false
    }
  ],
  "transfers": {
    "cost": 4,
    "status": "unlimited",
    "limit": null,
    "made": 0,
    "bank": 45,
    "value": 958
  }
}
```


## Picks  

The `picks` array contains details of selected players in the team.

| Field           | Type     | Description                                           |
|----------------|---------|-------------------------------------------------------|
| element        | integer | The player's unique identifier.                       |
| position       | integer | The player's position in the lineup.                  |
| multiplier     | integer | Points multiplier (e.g., 2 for captain, 1 by default). |
| is_captain     | boolean | Indicates if the player is the captain.               |
| is_vice_captain| boolean | Indicates if the player is the vice-captain.         |
| element_type   | integer | The type of player (e.g., 1 = goalkeeper, etc.).      |
| selling_price  | integer | The price at which the player can be sold.            |
| purchase_price | integer | The price at which the player was bought.             |

---

## Picks Last Updated  

| Field               | Type              | Description                                  |
|---------------------|------------------|----------------------------------------------|
| picks_last_updated  | string (ISO 8601) | Timestamp when the picks were last updated. |

---

## Chips  

The `chips` array contains special game-enhancing chips.

| Field             | Type      | Description                                      |
|------------------|----------|--------------------------------------------------|
| id              | integer  | Unique identifier for the chip.                  |
| status_for_entry| string   | Current status of the chip for the entry.        |
| played_by_entry | array    | Entries that have played this chip.              |
| name            | string   | Name of the chip (e.g., "wildcard").             |
| number          | integer  | The number of times the chip can be played.      |
| start_event     | integer  | The first gameweek the chip can be used.         |
| stop_event      | integer  | The last gameweek the chip can be used.          |
| chip_type       | string   | Type of chip (e.g., "transfer").                 |
| is_pending      | boolean  | Indicates if the chip is pending activation.     |

---

## Transfers  

The `transfers` object contains details about the team's transfer activity.

| Field   | Type    | Description                                                   |
|---------|--------|---------------------------------------------------------------|
| cost    | integer | Points deducted for making transfers beyond the free limit.  |
| status  | string  | Transfer status (e.g., "unlimited" during wildcard use).     |
| limit   | integer or null | Maximum number of transfers allowed (null if unlimited). |
| made    | integer | Number of transfers made in the current gameweek.            |
| bank    | integer | Budget remaining after transfers.                            |
| value   | integer | Total squad value including transfers.                       |

---

