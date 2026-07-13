# FDA FAERS PoC Dashboard

> FDA Adverse Event Reporting System — 2023 to 2026

**⚠️ SAMPLED DATA —** This repository contains a **13,000-row sample** drawn from the openFDA API. The full FAERS database holds **~4.3 million records** (as of April 2026). This sample is intended for **dashboard prototyping, proof-of-concept work, and exploratory analysis** — it is **not** the complete dataset and should not be used for production pharmacovigilance or medical decision-making.

## Dataset: `faers_2023_2026.csv`

### 13 Columns

| Column | Type | Example |
|--------|------|---------|
| `ReportID` | String | `21803134` |
| `Age` | Integer | `59` |
| `Age_Unit` | Integer | `801` (Years) |
| `Sex` | String | `Male`, `Female` |
| `Drug` | String | `DUPIXENT` |
| `Reaction` | String (MedDRA PT) | `Headache` |
| `Country` | String (ISO-2) | `US`, `ZA`, `GB` |
| `Serious` | Integer | `1`=Serious, `2`=No |
| `Seriousness_Death` | Integer | `1`=Death, `2`=No |
| `Period` | String | `2023-01` |
| `Quarter` | String | `2023-Q1` |
| `Reaction_SOC` | String | `Nervous System Disorders` |
| `Reaction_Group` | String | `Neurological` |

### Distribution

| Quarter | Rows |
|---------|------|
| 2023-Q1–Q4 | 4,000 |
| 2024-Q1–Q4 | 4,000 |
| 2025-Q1–Q4 | 4,000 |
| 2026-Q1 | 1,000 |
| **Total** | **13,000** |

### Top Reaction SOCs

| Reaction_SOC | % |
|--------------|---|
| Product & Medication Issues | 17.8% |
| General Disorders | 9.6% |
| Nervous System Disorders | 7.1% |
| Skin & Subcutaneous | 6.1% |
| Gastrointestinal | 6.0% |
| Respiratory | 5.7% |
| Musculoskeletal | 4.3% |
| Death | 3.6% |
| Blood & Lymphatic | 3.5% |
| Infections | 3.3% |

## Data Pipeline

1. **openFDA API** — batch download by quarter (100 records/request)
2. **Temporal enrichment** — `Period` (YYYY-MM) and `Quarter` (YYYY-Q#)
3. **SOC classification** — keyword-based MedDRA mapping (93% coverage)

## Use Cases

- Drug safety profile: Drug vs Reaction_SOC heatmap
- Trend analysis: Period/Quarter on timeline
- Demographic: Age by Sex by Reaction_SOC
- Geographic: Country map by Reaction_Group
- Seriousness: Serious × Seriousness_Death by Drug
