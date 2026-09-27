# Serial Killers Dataset

A comprehensive structured dataset of serial killers from Wikipedia's "List of serial killers by number of victims" page, containing detailed profiles for **494 serial killers** with rich metadata.

## Dataset Overview

- **Source**: Wikipedia - [List of serial killers by number of victims](https://en.wikipedia.org/wiki/List_of_serial_killers_by_number_of_victims)
- **Number of profiles**: 494
- **Time period covered**: 1900–2023
- **Geographic coverage**: Global (20+ countries with data)
- **Format**: JSON (structured) + CSV (tabular)
- **License**: CC BY-SA 4.0 (Wikipedia license)

## Data Fields (CSV - 33 columns)

### Core Identification
| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Primary name of the serial killer |
| `wikipedia_url` | string | Direct link to Wikipedia article |
| `wikipedia_title` | string | Exact Wikipedia page title |
| `aliases` | string | Known aliases, nicknames, birth names (semicolon-separated) |

### Victim Information
| Field | Type | Description |
|-------|------|-------------|
| `victims_proven` | integer | Number of confirmed/proven victims |
| `victims_possible` | integer | Number of possible/suspected victims |
| `victims_confessed` | integer | Number of victims confessed to |
| `victim_count_max` | integer | Maximum of proven/possible/confessed |
| `victim_count_category` | string | Category: High (30+), Medium (15-29), Low (5-14), Very Low (<5) |
| `victim_details` | string | Description of victim demographics and patterns |

### Temporal Information
| Field | Type | Description |
|-------|------|-------------|
| `active_start_year` | integer | Year killings began |
| `active_end_year` | integer | Year killings ended |
| `active_span` | string | Original text description of active period |
| `years_active` | integer | Calculated duration in years |

### Geographic Information
| Field | Type | Description |
|-------|------|-------------|
| `country_primary` | string | Primary country of operation |
| `countries` | string | All countries where killings occurred (semicolon-separated) |
| `regions` | string | Specific regions/states/provinces (semicolon-separated) |
| `cities` | string | Known cities of operation (semicolon-separated) |

### Personal Information
| Field | Type | Description |
|-------|------|-------------|
| `date_of_birth` | string | Birth date (as listed in Wikipedia) |
| `place_of_birth` | string | Birth location |
| `date_of_death` | string | Death date (if applicable) |
| `place_of_death` | string | Death location |
| `occupation` | string | Known occupation(s) |

### Criminal Justice
| Field | Type | Description |
|-------|------|-------------|
| `criminal_status` | string | Criminal status from infobox |
| `sentence` | string | Sentence/penalty received (combined) |

### Behavioral Profile
| Field | Type | Description |
|-------|------|-------------|
| `modus_operandi` | string | Description of killing methods and patterns |

### Classification
| Field | Type | Description |
|-------|------|-------------|
| `victim_count_category` | string | Category based on victim count (High: 30+, Medium: 15-29, Low: 5-14, Very Low: <5) |
| `gender` | string | Killer's gender (Male/Female/Unknown) |
| `operated_alone` | boolean | Whether they operated alone |
| `medical_professional` | boolean | Whether they were a medical professional |
| `law_enforcement` | boolean | Whether they were in law enforcement |

### Additional Metadata
| Field | Type | Description |
|-------|------|-------------|
| `wikipedia_categories` | string | All Wikipedia categories (semicolon-separated) |
| `extraction_date` | string | Date this data was extracted |
| `summary` | string | First few paragraphs of Wikipedia article |

## JSON Structure (Full Nested Data)

The JSON file contains the complete extracted data for each killer:

```json
{
  "name": "string",
  "wikipedia_url": "string",
  "summary": "string",
  "infobox": { "key": "value", ... },
  "sections": { "section_name": "content", ... },
  "victims": { "proven": "string", "possible": "string", "confessed": "string", "details": "string" },
  "timeline": { "start_year": "string", "end_year": "string", "span": "string" },
  "location": { "country": "string", "regions": ["string"], "cities": ["string"] },
  "personal_info": { "born": "string", "died": "string", "other_names": ["string"], "occupation": "string", "criminal_status": "string", "penalty": "string", ... },
  "modus_operandi": "string",
  "categories": ["string"],
  "extracted_at": "string"
}
```

## Data Quality Notes

1. **Victim counts**: "Proven" victims are those legally convicted or definitively linked. "Possible" victims include unconfirmed but suspected victims.
2. **Missing data**: Many historical cases have incomplete information. Fields may be empty.
3. **Disputed cases**: Some entries are disputed or unverified - these are flagged in the `wikipedia_categories`.
4. **Groups/Couples**: Serial killer groups and couples are included as separate entries with `operated_alone=false`.
5. **Medical professionals**: Listed separately in source but included here with `medical_professional=true`.
6. **Law enforcement**: Identified via Wikipedia categories with `law_enforcement=true`.

## Dataset Statistics (v1.0)

| Metric | Value |
|--------|-------|
| Total Profiles | 494 |
| Countries with data | 20+ |
| Female Killers | 48 (9.7%) |
| Medical Professionals | 50 |
| Law Enforcement | 27 |
| Groups/Couples | 26 |
| Avg. Proven Victims | 13.7 |
| Max Proven Victims | 250 (Harold Shipman) |

### Top Countries
1. United States (161)
2. Russia (21)
3. Soviet Union (21)
4. South Africa (15)
5. China (13)
6. France (13)

### Victim Count Distribution
- **High (30+)**: 76 killers
- **Medium (15-29)**: 60 killers
- **Low (5-14)**: 262 killers
- **Very Low (<5)**: 96 killers

## Usage Examples

```python
import pandas as pd

# Load CSV (recommended for analysis)
df = pd.read_csv('serial_killers_dataset.csv')

# Filter by victim count
high_victim_killers = df[df['victims_proven'] >= 30]

# By country
us_killers = df[df['country_primary'] == 'United States']

# By time period
modern_killers = df[df['active_start_year'] >= 1980]

# By gender
female_killers = df[df['gender'] == 'Female']

# Medical professionals who killed
medical_killers = df[df['medical_professional'] == True]

# Law enforcement killers
le_killers = df[df['law_enforcement'] == True]

# Load JSON for full nested data
import json
with open('serial_killers_dataset.json', 'r') as f:
    killers = json.load(f)

# Access full nested data
for killer in killers:
    if killer['victims']['proven'] and int(killer['victims']['proven']) > 50:
        print(f"{killer['name']}: {killer['victims']['proven']} victims")
```

## Citation

If you use this dataset, please cite:

```
Serial Killers Dataset, derived from Wikipedia's "List of serial killers by number of victims"
Wikipedia contributors. "List of serial killers by number of victims." Wikipedia, The Free Encyclopedia.
```

## Ethical Considerations

This dataset contains information about real crimes and real victims. Please use responsibly:
- Respect the victims and their families
- Do not glorify or sensationalize the crimes
- Consider the impact on surviving victims and families
- Use for legitimate research, education, or analysis purposes only

## Version History

- **v1.0** (2025): Initial release with 494 profiles from Wikipedia
- Future versions may include updates from Wikipedia revisions and additional sources

## Contact

For questions or issues with this dataset, please open an issue on the associated GitHub repository.