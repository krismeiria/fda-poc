# FDA FAERS PoC Dashboard

> **Data engineering pipeline:** openFDA API → temporal enrichment → MedDRA SOC classification → analytics-ready dataset.

**FDA Adverse Event Reporting System** — 3,000 adverse event reports from **2023–2026**.

## Dataset: `faers_2023_2026.csv`

### 13 Columns

| Column | Type | Description | Example |
|--------|------|-------------|---------|
| `ReportID` | String | Unique FAERS safety report ID | `21803134` |
| `Age` | Integer | Patient age at onset | `59` |
| `Age_Unit` | Integer | 801=Years, 802=Months, 803=Weeks | `801` |
| `Sex` | String | Patient sex | `Male`, `Female` |
| `Drug` | String | Medicinal product | `DUPIXENT` |
| `Reaction` | String | Adverse reaction (MedDRA PT) | `Headache` |
| `Country` | String | Reporter country (ISO-2) | `US`, `ZA`, `GB` |
| `Serious` | Integer | 1=Serious, 2=Not serious | `1`, `2` |
| `Seriousness_Death` | Integer | 1=Death, 2=No death | `1`, `2` |
| `Period` | String | **Enriched:** Year-Month | `2023-01` |
| `Quarter` | String | **Enriched:** Year-Quarter | `2023-Q1` |
| `Reaction_SOC` | String | **Enriched:** System Organ Class (26 cats) | `Nervous System Disorders` |
| `Reaction_Group` | String | **Enriched:** Aggregated group (12 cats) | `Neurological` |

## Pipeline

```
openFDA API (4.3M records)
        ↓ Stratified sampling (750/yr)
  Temporal enrichment (Period, Quarter)
        ↓ 
  MedDRA SOC classification (26 SOCs, 99.5% coverage)
        ↓
  faers_2023_2026.csv
```

## Top Reaction SOCs

| SOC | % |
|-----|---|
| Product & Medication Issues | 18.1% |
| General Disorders | 11.3% |
| Nervous System Disorders | 7.5% |
| Skin & Subcutaneous | 7.3% |
| Gastrointestinal | 6.2% |
| Respiratory | 5.9% |
| Death | 5.1% |

## Use Cases (Tableau)

- **Drug Safety Profile:** Drug vs Reaction_SOC heatmap
- **Trend Analysis:** Period/Quarter over time
- **Demographic:** Age by Sex by Reaction_SOC
- **Geographic:** Country map by Reaction_Group
- **Seriousness:** Serious × Seriousness_Death by Drug

---

*Source: [openFDA API](https://open.fda.gov/apis/drug/event/) · Classification: MedDRA SOC*
