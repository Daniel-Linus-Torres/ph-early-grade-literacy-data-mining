# Mining the Literacy Gap: Early-Grade Proficiency and Regional Disparities in Philippine Student Performance

A data mining study of school-level **CRLA 2025–2026** results from the Department of Education (DepEd). It tests whether Mother Tongue (L1) proficiency relates to Filipino (L2) and English (L3) proficiency, how literacy differs by region and school type, and how well school characteristics predict reading outcomes.

> **Course:** 9349 ITE 17 – Data Mining, Saint Louis University (SAMCIS) · **Submitted:** July 19, 2026

---

## Table of Contents
- [Research Questions](#research-questions)
- [Data](#data)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Limitations](#limitations)
- [Team](#team)
- [Acknowledgments](#acknowledgments)
- [License](#license)

## Research Questions
The study is organized around five themes, each mapped to a data mining method:
1. **Profile:** demographic and geographic profile of participating schools.
2. **Status:** early-grade (Grades 1–3) literacy status by region and school classification.
3. **Cross-linguistic transfer:** correlation between Mother Tongue, Filipino, and English proficiency.
4. **Clustering:** natural groups in Grade 1–3 reading trajectories.
5. **Prediction:** which school characteristics (urban/rural, mother tongue, teacher count, enrollment) predict reading success.

## Data
| Item | Detail |
|---|---|
| Primary source | DepEd Comprehensive Rapid Literacy Assessment (CRLA) 2025–2026, school level |
| Coverage | 6,121 public elementary schools · 647,681 students · 44 school divisions · 5 regions (CAR, I, III, VIII, IX) · 13 mother tongues |
| Size | 58 attributes across school identity, location, language, and proficiency measures |
| Merged with | DepEd Masterlist of Schools (region, division, municipality, barangay); School Personnel SY 2023–24; School Facilities SY 2023–24; Enrollment SY 2024–25; ELLNA Mean Percentage Score |

Files were joined on School ID (or standardized school name where needed). This is secondary data: no new data was collected.

> Raw files are not redistributed here. See [`data/README.md`](data/README.md).

## Methodology
| Goal | Technique |
|---|---|
| Descriptive profile | Frequency tables and regional/school-type breakdowns |
| Cross-linguistic transfer | Pearson correlation (overall and by region/setting) |
| Reading trajectories | Hierarchical clustering on standardized features; number of clusters chosen by silhouette score (k = 2–8) |
| Prediction | Binary and multi-class Logistic Regression, 20 % hold-out test set |
| Evaluation | Accuracy, weighted ROC-AUC, confusion matrices, odds ratios / coefficients |

## Key Findings
- **Strong L1 → L2/L3 relationship at Grade 3.** Correlations ranged from **r = .916** (Mother Tongue–Filipino) to **r = .807** (Mother Tongue–English), all significant, so the null hypothesis was rejected for Grade 3.
- **Clear regional gap.** Region III (Central Luzon) had the highest share of learners "At Grade Level" (**18.40 %**) and Region VIII (Eastern Visayas) the lowest (**12.69 %**).
- **Two natural performance clusters** emerged from Grade 1–3 reading trajectories (best silhouette score at k = 2).
- **Limited predictive power from school profile alone.** Logistic Regression accuracy ranged from about **56 % to 68 %**, suggesting demographic and linguistic attributes do not fully determine school-level outcomes. Implementation quality and region also matter.

## Repository Structure
```
ph-early-grade-literacy-data-mining/
├── data/                   # Dataset and documentation
│   ├── CRLA_Dataset.csv
│   └── README.md
│
├── docs/                   # Research documentation
│   └── Ph-Literacy-Gap-Research-Paper.pdf
│
├── figures/                # Visualizations and analysis outputs
│   ├── 01_schools_per_region.png
│   ├── 02_schools_by_mother_tongue.png
│   ├── 03_classification_pie.png
│   ├── 04_region_by_classification_stacked.png
│   ├── 05_proficiency_by_region.png
│   ├── 06_proficiency_by_classification.png
│   ├── 07_national_proficiency_donut.png
│   ├── 08_I1_I2_I3_correlation_heatmap.png
│   ├── 09_I1_I2_I3_scatterplots.png
│   ├── 10_pca_scree_plot.png
│   ├── 11_pca_loadings.png
│   ├── 12_pca_scatter_by_region.png
│   ├── 13_hierarchical_clusters.png
│   ├── cluster_composition_*.png
│   ├── correlations_by_*.png
│   └── crla_analysis_output.xlsx
│
├── notebooks/              # Analysis notebooks
│   ├── 01_exploratory_analysis_and_clustering.ipynb
│   └── 02_multiclass_logistic_regression.ipynb
│
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

## Getting Started
```bash
git clone https://github.com/<your-username>/ph-early-grade-literacy-data-mining.git
cd ph-early-grade-literacy-data-mining

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

jupyter notebook notebooks/analysis.ipynb
```

## Limitations
- The analysis covers **five regions**, so results should not be read as national estimates. Some regions dominate certain school types, which affects regional and urban/rural comparisons.
- The CRLA data does not directly measure factors such as socioeconomic status, nutrition, or teaching quality.
- Correlation does not imply causation; results describe association across schools.
- Logistic Regression accuracy was modest, so the models are exploratory rather than operational.

## Team
Jecquar Ravent Aguilan, Mark Angara, Ryan Adelard Barrera, Syed Karim, Leon Neil Padiernos, Gelina Tibayan, Daniel Linus Torres, Marvin John Vergara, Benedict Wacdagan.

Submitted to Mrs. Beverly Ferrer.

## Acknowledgments
Data: Department of Education (DepEd), Philippines. Please check DepEd's terms of use and cite the source when reusing results.

## License
Code is released under the [MIT License](LICENSE). Data remains subject to its original provider's terms.
