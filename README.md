# GenAI & Agentic AI Security Incidents (2024–2026)

Incident-level records underlying the report **"Coverage Without Casualties?"**. Each row is a
publicly disclosed GenAI / agentic-AI security incident, vulnerability, or red-team finding,
tagged against common AI-security taxonomies and (where applicable) crosswalked to the threat IDs
of the *Insurability Frontier* companion paper.

**4,328 records · 2024–2026 · data cutoff 17 May 2026.**

## Files

| File | Description |
|------|-------------|
| `Incident_Data_2024-2026.xlsx` | Canonical workbook. Includes an embedded `Readme` sheet plus the `Incidents 2024-2026` data sheet. |
| `incidents_2024-2026.csv` | CLI-friendly export of the data sheet (UTF-8, RFC-4180 quoted). Identical content, git-diffable. |

## Provenance

A subset of **GenAI & Agentic AI Security Incidents** (Zenodo v2.0.0,
[zenodo.org/records/20248676](https://zenodo.org/records/20248676), DOI
[10.5281/zenodo.20248676](https://doi.org/10.5281/zenodo.20248676)), restricted to 2024–2026.

Records are consolidated and de-duplicated from public AI-incident repositories and vulnerability
databases: OECD AI Incidents Monitor (oecd.ai), AI Incident Database / Responsible AI Collaborative
(incidentdatabase.ai), AIAAIC Repository (aiaaic.org), AIRI Navigator (airi-navigator.com), NIST
National Vulnerability Database (nvd.nist.gov), and MITRE ATLAS case studies (atlas.mitre.org).
Every record derives from a **publicly disclosed** source; no private or personal data is added.

Taxonomy tags: OWASP LLM Top 10, OWASP ASI (Agentic Security Initiative), MITRE ATLAS, NIST AI RMF.

## Important caveats

- **Streams are distinct evidence types and are NOT summed.** *Realized*, *Demonstrated*, and
  *Surfacing* (see below) measure different things; do not add them into a single frequency.
- **This is an incident catalogue, not insured-loss experience.** Counts reflect documented
  disclosures, not claims or losses.
- **`Mapped threats` may be empty, one, or many.** A record maps to a threat only when its
  documented predicate is satisfied; a blank value means it matched no threat predicate but still
  counts toward its stream total.

### Evidence streams

| Stream | Meaning | n |
|--------|---------|---:|
| Realized | Real-world incidents | 3,054 |
| Demonstrated | Research / red-team demonstrations | 214 |
| Surfacing | Vulnerability disclosures | 1,060 |
| **Total** | | **4,328** |

## Data dictionary

20 columns. Free-text and multi-value fields are quoted in the CSV; multi-value tags are
comma-separated within a single cell. Counts in parentheses are non-empty values out of 4,328.

| Column | Type | Notes / example |
|--------|------|-----------------|
| `ID` | string | Stable record ID, e.g. `INC-01411`. |
| `Stream` | enum | `Realized` / `Demonstrated` / `Surfacing`. |
| `Source category` | enum | `real-world`, `research`, `research-demonstrated`, `red-team`, `vulnerability-disclosure`. |
| `Date` | string | **Variable precision**: `YYYY`, `YYYY-MM`, or `YYYY-MM-DD`. Kept as text. |
| `Year` | integer | 2024 (960) / 2025 (1,249) / 2026 (2,119). |
| `Severity` | enum | `Critical` (913) / `High` (1,765) / `Medium` (1,617) / `Low` (33). |
| `CVSS` | number | CVSS base score where available (1,017). |
| `Attack vector` | string | e.g. `prompt-injection`, `jailbreak`, `rce`, `deepfake`, `supply`, `other`. |
| `OWASP LLM` | multi-value | OWASP LLM Top 10 IDs, e.g. `LLM01, LLM03` (3,742). |
| `OWASP ASI` | multi-value | OWASP Agentic Security IDs, e.g. `ASI08, ASI09` (3,594). |
| `MITRE ATLAS` | multi-value | ATLAS technique IDs, e.g. `AML.T0048` (3,836). |
| `NIST AI RMF` | multi-value | NIST AI RMF subcategory IDs, e.g. `GOVERN-1.4` (3,836). |
| `CVE IDs` | multi-value | Associated CVE identifiers (1,130). |
| `AIID ID` | string | AI Incident Database identifier (728). |
| `Mapped threats (Insurability Frontier companion paper crosswalk)` | multi-value | Threat IDs `T-01`..`T-55`; may be empty (3,101 populated). |
| `Quality tier` | enum | `curated` (121) / `reviewed` (2,519) / `auto` (1,688). |
| `Title` | string | Short incident title. |
| `Affected` | string | Affected systems / parties where known (1,946). |
| `Primary reference URL` | string | Public source link. |
| `Description` | string | Free-text summary (up to ~4,000 chars). |

## Quick start (CLI)

```bash
# Row count by stream
csvcut -c Stream incidents_2024-2026.csv | tail -n +2 | sort | uniq -c

# Ad-hoc SQL with DuckDB
duckdb -c "SELECT Year, Severity, count(*) FROM 'incidents_2024-2026.csv' GROUP BY 1,2 ORDER BY 1,2"
```

```python
import pandas as pd
df = pd.read_csv("incidents_2024-2026.csv", dtype={"Date": str})
df.groupby(["Stream", "Severity"]).size()
```

## License

Released under **[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)**, matching the upstream
Zenodo dataset. You may share and adapt the data with appropriate attribution.

## Citation

Please cite both this dataset and the upstream source:

> Guilherme Jr., E. *GenAI & Agentic AI Security Incidents* (v2.0.0). Zenodo.
> DOI: 10.5281/zenodo.20248676

> *Coverage Without Casualties?* — incident dataset (2024–2026 subset, cutoff 17 May 2026).
