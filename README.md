# Cosmetic Ingredients Database

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

A curated, clinically-informed database of cosmetic and skincare ingredients. Each entry is rated by category, comedogenic potential, and includes a clinical rationale and usage notes.

Compiled and maintained by **Dr. Ifeanyi R. Chukwuka, MBBS, M.S., MWACP**, Senior Resident in Dermatology.

---

## Contents

- [Overview](#overview)
- [Schema](#schema)
- [Usage](#usage)
- [License](#license)

---

## Overview

This database currently contains **55 ingredients** spanning three categories:

| Category  | Count | Description                                                                          |
| --------- | ----- | ------------------------------------------------------------------------------------ |
| `good`    | 20    | Ingredients with well-documented skin benefits                                       |
| `bad`     | 20    | Ingredients that are irritating, comedogenic, or harmful to skin barrier integrity   |
| `neutral` | 15    | Functional ingredients with no significant benefit or harm at typical concentrations |

Comedogenic ratings follow the standard 0–5 scale used in dermatological literature:

| Rating | Meaning                |
| ------ | ---------------------- |
| 0      | Non-comedogenic        |
| 1      | Unlikely to clog pores |
| 2      | Mildly comedogenic     |
| 3      | Moderately comedogenic |
| 4      | Fairly comedogenic     |
| 5      | Highly comedogenic     |

---

## Schema

The database is a single JSON file structured as follows:

```json
{
  "version": "1.0",
  "last_updated": "2026-03-12",
  "author": "Dr. Ifeanyi R. Chukwuka, MBBS, M.S., MWACP",
  "source": "Clinical dermatology reference + curated research",
  "ingredients": []
}
```

Each ingredient entry follows this structure:

```json
{
  "name": "Niacinamide",
  "aliases": ["nicotinamide", "vitamin b3", "niacin"],
  "category": "good",
  "comedogenic_rating": 0,
  "reason": "Brightens skin tone, reduces pore appearance, strengthens skin barrier, anti-inflammatory.",
  "notes": "One of the most versatile and well-researched skincare ingredients. Effective at concentrations of 2-10%."
}
```

### Field Reference

| Field                | Type     | Description                                                                        |
| -------------------- | -------- | ---------------------------------------------------------------------------------- |
| `name`               | `string` | Primary ingredient name                                                            |
| `aliases`            | `array`  | Alternative names and INCI variants the ingredient may appear as on product labels |
| `category`           | `string` | `"good"`, `"bad"`, or `"neutral"`                                                  |
| `comedogenic_rating` | `number` | 0–5 scale                                                                          |
| `reason`             | `string` | Clinical rationale for the category rating                                         |
| `notes`              | `string` | Additional context, caveats, concentration thresholds, skin type considerations    |

---

## Usage

The database is publicly accessible as a raw JSON file and can be fetched directly in any JavaScript project.

**Fetch URL:**

```
https://raw.githubusercontent.com/steppino45/ingredients-db/main/ingredients.json
```

**Example — fetching and searching by ingredient name:**

```js
async function loadIngredients() {
  const response = await fetch(
    "https://raw.githubusercontent.com/steppino45/ingredients-db/refs/heads/main/ingredients.json",
  );
  const data = await response.json();
  return data.ingredients;
}

async function findIngredient(name) {
  const ingredients = await loadIngredients();
  return ingredients.find(
    (i) =>
      i.name.toLowerCase() === name.toLowerCase() ||
      i.aliases.includes(name.toLowerCase()),
  );
}
```

**Example — filtering by category:**

```js
const goodIngredients = ingredients.filter((i) => i.category === "good");
const badIngredients = ingredients.filter((i) => i.category === "bad");
```

**Example — filtering by comedogenic rating:**

```js
const highlyComedogenic = ingredients.filter((i) => i.comedogenic_rating >= 4);
```

---

## License

This database is licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License](https://creativecommons.org/licenses/by-nc-nd/4.0/).

© 2026 Dr. Ifeanyi R. Chukwuka, MBBS, M.S., MWACP. All rights reserved.

**You are free to:**

- Share and use this database for personal, academic or non-commercial projects
- Fetch and integrate it into non-commercial applications with attribution

**Under the following terms:**

- **Attribution** — You must give appropriate credit to Dr. Ifeanyi R. Chukwuka, MBBS and link to this repository
- **NonCommercial** — You may not use this database for commercial purposes
- **NoDerivatives** — You may not modify, adapt or build upon this database and redistribute it as your own work

For licensing enquiries or commercial use, open an issue in this repository.
