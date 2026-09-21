# Data

## `CRLA_Dataset.csv`
The final merged, school-level dataset used in this study. **6,121 rows (one per public elementary school) × 71 columns.** No rows were removed.

| Item | Value |
|---|---|
| Schools | 6,121 (`school_id` is unique) |
| Test takers | 647,681 |
| Regions | CAR, Region I, Region III, Region VIII, Region IX |
| Divisions | 44 |
| Mother tongues | 13 (Tagalog, Waray, Sinugbuanong Binisaya, Ilocano, Pangasinan, Kapampangan, and others) |

The data is aggregated at school level. It contains no student- or teacher-level records. School names and addresses are public institutions' details.

### Sources (Department of Education, Philippines)
| Dataset | Used for |
|---|---|
| Comprehensive Rapid Literacy Assessment (CRLA) 2025–2026 | Reading proficiency levels by grade and language |
| Masterlist of Schools | School name, address, district, and location identifiers |
| School Personnel, SY 2023–2024 | `total_teachers` |
| School Facilities, SY 2023–2024 | `total_facilities` |
| Enrollment, SY 2024–2025 | `total_enrollees` |
| ELLNA Mean Percentage Score (MPS) | `*_mps` columns |

Files were merged on `school_id`, with standardized school name as a fallback.

> **Source and terms:** *(fill in before publishing: where and when you obtained each file, e.g., the DepEd portal or request, the download date, and any usage terms.)* Please cite DepEd when reusing this data.

### Column guide
| Columns | Description |
|---|---|
| `school_id` | DepEd school identifier |
| `region`, `division`, `Municipality`, `District_Name`, `District`, `Barangay`, `Address`, `School_Name` | Location and school identity |
| `language` | Mother tongue used for the school in CRLA |
| `Ownership`, `Classification`, `Management`, `Level` | School type. `Classification` is Urban, Partially Urban, or Rural. `Level` is Purely ES, ES and JHS (K to 10), or All Offering (K to 12) |
| `n_test_takers_x`, `n_test_takers_y` | Number of test takers. The `_x`/`_y` suffixes come from the merge of two source files, so confirm which source each came from in your notebook |
| `school_*_total`, `school_*_percent` | School-wide count and share of learners in each proficiency level |
| `g1_mt_*`, `g2_mt_*`, `g2_fil_*`, `g3_mt_*`, `g3_fil_*`, `g3_eng_*` | Learner counts by grade (g1–g3) and language (`mt` Mother Tongue, `fil` Filipino, `eng` English) for each proficiency level, plus a `_total` |
| `total_enrollees`, `total_teachers`, `total_facilities` | Enrollment, teacher count, and facilities from the merged DepEd files |
| `english_mps`, `filipino_mps`, `mother_tongue_mps`, `numeracy_mps`, `mps`, `overall_mps` | Mean Percentage Scores from ELLNA |

**Proficiency levels** (used in the `*_low_emerging`, `*_high_emerging`, `*_developing`, `*_transitioning`, and `*_at_grade_level` columns): Low Emerging, High Emerging, Developing, Transitioning, At Grade Level.

### Missing values
Missing values are left as blank cells. Columns with gaps:

| Column | Missing |
|---|---|
| `Address` | 651 |
| `District`, `School_Name` | 187 each |
| `total_facilities`, `total_teachers` | 31 each |
| `Barangay` | 12 |
| `District_Name` | 10 |
| `Classification`, `Management` | 9 each |
| `Municipality`, `Level` | 8 each |
| `Ownership` | 3 |

Most `School_Name`, `District`, and `Address` gaps come from schools that did not match the Masterlist of Schools.

### Loading the data
```python
import pandas as pd

df = pd.read_csv("data/CRLA_Dataset.csv")
print(df.shape)   # (6121, 71)
```
