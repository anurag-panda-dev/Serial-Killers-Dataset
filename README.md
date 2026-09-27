# Serial Killers Dataset

> A comprehensive structured dataset of 494 serial killers from Wikipedia with detailed profiles for criminology research, data analysis, and machine learning.

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC_BY_SA_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Format: JSON/CSV](https://img.shields.io/badge/Format-JSON%20%7C%20CSV-blue.svg)](https://github.com/)
[![Profiles: 494](https://img.shields.io/badge/Profiles-494-green.svg)](https://en.wikipedia.org/wiki/List_of_serial_killers_by_number_of_victims)

## 📋 Overview

This dataset contains structured profiles of **494 serial killers** extracted from Wikipedia's authoritative ["List of serial killers by number of victims"](https://en.wikipedia.org/wiki/List_of_serial_killers_by_number_of_victims) page. Each profile includes victim counts, temporal data, geographic information, personal details, criminal justice outcomes, and behavioral patterns.

### Key Statistics
- **494** serial killer profiles
- **60+** countries represented
- **1900–2023** time coverage
- **Structured fields**: 33 per profile (CSV) / 12 nested objects (JSON)
- **Formats**: JSON (nested) + CSV (flattened)

## 🎯 Use Cases

| Domain | Applications |
|--------|--------------|
| **Criminology Research** | Victimology patterns, geographic profiling, temporal trends |
| **Data Science/ML** | Classification (solo vs group), regression (victim count prediction), clustering |
| **Education** | Case studies, comparative analysis, statistics exercises |
| **Journalism** | Background research, fact-checking, trend analysis |
| **True Crime Analysis** | Pattern recognition, MO comparison, timeline reconstruction |

## 📊 Data Preview

### JSON Structure (Nested, Complete)
```json
{
  "name": "Luis Garavito",
  "wikipedia_url": "https://en.wikipedia.org/wiki/Luis_Garavito",
  "summary": "Luis Alfredo Garavito Cubillos (1957–2023) was a Colombian serial killer...",
  "infobox": {
    "Born": "25 January 1957, Génova, Quindío, Colombia",
    "Died": "12 October 2023, Valledupar, Colombia",
    "Victims": "193 proven, 194–300+ possible",
    "Span of crimes": "1992–1999",
    "Country": "Colombia, Ecuador, Venezuela"
  },
  "victims": {
    "proven": "193",
    "possible": "194–300+",
    "details": "Child-murderer, torture-killer, and rapist known as 'La Bestia'..."
  },
  "timeline": {"start_year": "1992", "end_year": "1999", "span": "1992–1999"},
  "location": {"country": "Colombia", "regions": ["Ecuador", "Venezuela"]},
  "personal_info": {
    "born": "25 January 1957",
    "died": "12 October 2023",
    "penalty": "22 years (reduced from 1,853)"
  },
  "modus_operandi": "Targeted street children aged 6-16, lured with gifts/money...",
  "categories": ["Colombian serial killers", "Child murderers", "1990s criminals"]
}
```

### CSV Structure (Flattened, Analysis-Ready)
| name | victims_proven | victims_possible | country_primary | active_start_year | active_end_year | gender | operated_alone | medical_professional | modus_operandi |
|------|---------------|------------------|-----------------|-------------------|-----------------|--------|----------------|---------------------|----------------|
| Luis Garavito | 193 | 300 | Colombia | 1992 | 1999 | Male | True | False | Targeted street children... |
| Andrei Chikatilo | 53 | 56 | USSR/Russia | 1978 | 1990 | Male | True | False | Lured victims at train stations... |
| Aileen Wuornos | 7 | 7 | United States | 1989 | 1990 | Female | True | False | Shot male motorists... |

## 🔧 Quick Start

### Python (Pandas)
```python
import pandas as pd

# Load CSV (recommended for analysis)
df = pd.read_csv('serial_killers_dataset.csv')

# Top 10 by proven victims
print(df.nlargest(10, 'victims_proven')[['name', 'victims_proven', 'country_primary', 'active_span']])

# By country
us_killers = df[df['country_primary'] == 'United States']

# Female serial killers
female_killers = df[df['gender'] == 'Female']

# High victim count killers (30+)
prolific = df[df['victim_count_category'] == 'High (30+)']

# Medical professionals who killed
medical_killers = df[df['medical_professional'] == True]

# Law enforcement killers
le_killers = df[df['law_enforcement'] == True]
```

### Python (Full JSON)
```python
import json

with open('serial_killers_dataset.json', 'r') as f:
    killers = json.load(f)

# Access full nested data
for killer in killers:
    if killer['victims']['proven'] and int(killer['victims']['proven']) > 50:
        print(f"{killer['name']}: {killer['victims']['proven']} victims")
        print(f"  MO: {killer['modus_operandi'][:200]}...")
```

### R
```r
library(jsonlite)
library(dplyr)

# Load CSV
df <- read.csv('serial_killers_dataset.csv')

# Or load JSON
killers <- fromJSON('serial_killers_dataset.json')

# Analysis
df %>% 
  filter(victims_proven >= 30) %>% 
  group_by(country_primary) %>% 
  summarise(count = n(), avg_victims = mean(victims_proven)) %>%
  arrange(desc(count))
```

## 📁 File Structure

```
serial-killers-dataset/
├── serial_killers_dataset.json      # Full nested dataset (recommended for development)
├── serial_killers_dataset.csv       # Flattened CSV (recommended for analysis)
├── datapackage.json                 # Frictionless Data package descriptor
├── DATASET_CARD.md                  # Detailed field documentation
├── dataset_stats.json               # Summary statistics
└── README.md                        # This file
```

## 📈 Dataset Statistics

| Metric | Value |
|--------|-------|
| Total Profiles | 494 |
| Countries | 20+ (with data) |
| Year Range | 1900–2023 |
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
7. Mexico (9)
8. England (8)
9. Japan (8)
10. Australia (8)

### Victim Count Distribution
- **High (30+)**: 76 killers
- **Medium (15-29)**: 60 killers
- **Low (5-14)**: 262 killers
- **Very Low (<5)**: 96 killers

## ⚠️ Ethical Considerations

**This dataset documents real crimes with real victims.** Please use responsibly:

- ✅ Academic research, education, statistical analysis
- ✅ Crime prevention, victim advocacy, policy research
- ✅ Historical documentation, journalism
- ❌ Glorification, sensationalism, entertainment
- ❌ Identifying or contacting victims/families
- ❌ Instructions for harmful activities

## 📝 Data Quality Notes

1. **Source limitations**: Data comes from Wikipedia - may contain inaccuracies, biases, or outdated information
2. **Victim counts**: "Proven" = legally convicted/definitively linked; "Possible" = suspected but unconfirmed
3. **Missing data**: Historical cases often have incomplete records; fields may be `null`
4. **Disputed cases**: Some entries are controversial - flagged in `wikipedia_categories`
5. **Groups/Couples**: Listed as separate entries with `operated_alone=false`
6. **Medical professionals**: Included with `medical_professional=true` flag

## 🔄 Updates

This dataset was extracted from Wikipedia on **August 2026**. Wikipedia is continuously updated. To refresh:

1. Re-run extraction scripts (included in repo)
2. Check for new/updated Wikipedia articles
3. Verify victim counts against court records where possible

## 📜 License

**CC BY-SA 4.0** - ShareAlike license inherited from Wikipedia.

You are free to:
- **Share** — copy and redistribute in any medium/format
- **Adapt** — remix, transform, build upon the material

Under terms:
- **Attribution** — credit Wikipedia and this dataset
- **ShareAlike** — distribute under same license

## 🙏 Acknowledgments

- **Wikipedia contributors** for maintaining the source list
- **Criminologists & researchers** whose work underpins the articles
- **Victims' families** whose tragedy this data represents

## 📬 Citation

```bibtex
@dataset{serial_killers_2026,
  title = {Serial Killers Dataset: Comprehensive Profiles from Wikipedia},
  author = {Anurag Panda},
  year = {2026},
  source = {Wikipedia: List of serial killers by number of victims},
  url = {https://en.wikipedia.org/wiki/List_of_serial_killers_by_number_of_victims},
  license = {CC-BY-SA-4.0}
}
```

## 🔗 Related Resources

- [Wikipedia: Serial killer](https://en.wikipedia.org/wiki/Serial_killer)
- [FBI: Serial Murder](https://www.fbi.gov/file-repository/serial-murder-multi-disciplinary-perspectives-for-investigators.pdf)
- [Radford University Serial Killer Database](https://www.radford.edu/psychology/serial-killer-database/)
- [Murder Accountability Project](https://www.murderdata.org/)

---

**Remember**: Behind every data point is a human tragedy. Use this dataset to understand and prevent, not to exploit.
