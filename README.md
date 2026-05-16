BI-436 · Special Topics in Bioinformatics
Epigenetics & Aging
Analysis
Aarish Sajid · 454572
NUST SINES
Spring 2026
Python 3.10+
biolearn
PyTorch
14 Clocks
2 GEO Datasets
WGBS Pipeline
EPIC Array
00
Overview
This project benchmarks fourteen epigenetic aging clocks against two public GEO datasets (GSE40279, GSE41169), quantifying how well DNA-methylation-based models predict chronological age. A companion WGBS pipeline processes raw bisulfite-sequencing reads through alignment, methylation extraction, and differential methylation region (DMR) detection across seven breast-tissue methylomes.

🧬
Clocks Tested
14
Horvath v1/v2, Hannum, PhenoAge, AltumAge, DunedinPACE + more
🗂️
Datasets
2
GSE40279 (n≈656) & GSE41169 (n≈95)
🔬
WGBS Samples
7
NB1, NB2, BT089, BT126, BT198, MCF7, T47D
📊
Visualisations
5
Correlation matrix, age deviation heatmap, scatter plots, MAE bars, distributions
01
Project Structure
epigenetics-aging/ ├── wgbs/ │ ├── run_wgbs_pipeline.sh # Main WGBS bash pipeline │ └── README.md # Galaxy walkthrough ├── results/ │ ├── figures/ │ │ ├── correlation_matrix_GSE40279.png │ │ ├── correlation_matrix_GSE41169.png │ │ ├── age_deviation_heatmap_GSE40279.png │ │ ├── age_deviation_heatmap_GSE41169.png │ │ ├── age_prediction_GSE40279.png │ │ ├── age_prediction_GSE41169.png │ │ ├── mae_comparison.png │ │ └── predicted_age_distribution.png │ ├── tables/ │ │ ├── metrics_GSE40279.csv │ │ └── metrics_GSE41169.csv │ └── summary.md # Auto-generated metrics report └── epigenetics_aging_analysis.ipynb # Main analysis notebook
02
Part 1 — WGBS Pipeline
Whole-genome bisulfite sequencing (WGBS) data from seven breast methylomes is processed end-to-end: QC → trimming → bisulfite-aware alignment → methylation extraction → CpG-island profiling → DMR detection → hierarchical clustering.

🔍
Falco QC
Per-sample quality check
✂️
Trim Galore
Q20, length ≥ 20 bp
🗺️
bwa-meth
Bisulfite alignment to hg38
⚗️
MethylDackel
CpG methylation extraction
🏝️
deepTools
CpG-island profiles
📍
Metilene
DMR detection
Samples
Sample	Type	Group
NB1	Normal breast tissue	Normal (A)
NB2	Normal breast tissue	Normal (A)
BT089	Breast tumour	Tumour (B)
BT126	Breast tumour	Tumour (B)
BT198	Breast tumour	Tumour (B)
MCF7	Breast cancer cell line	Tumour (B)
T47D	Breast cancer cell line	Tumour (B)
Key Outputs
CGI_methylation_profile.png — average CpG-island methylation profile centred on CGI midpoints (±2 kb)
dmrs_tumour_vs_normal.bed — differentially methylated regions (normal A vs tumour B) via Metilene
hierarchical_hmr_clustering.png — cosine-distance ward-linkage heatmap of HMR methylation across all 7 samples
Quick Start (CLI)
bash wgbs/run_wgbs_pipeline.sh
Alternatively, import the Galaxy workflow via usegalaxy.eu.

Distance from CGI centre (bp)
Average CpG-Island Methylation Profile — 7 Breast Methylomes
-2000
-1000
0
+1000
+2000
0
0.5
1.0
NB1/NB2 (Normal)
BT089/BT126/BT198 (Tumour)
MCF7/T47D (Cell line)
Fig 1. Schematic CpG-island methylation profile. Normal samples (blue) show hypomethylation at CGI centres—a hallmark of active gene promoters. Tumour samples (red/orange) exhibit CGI hypermethylation consistent with transcriptional silencing.
03
Part 2 — Aging Clock Benchmarking
Fourteen published epigenetic clocks are evaluated on two EPIC-array datasets retrieved via biolearn. Each clock predicts either biological age (in years) or a pace-of-aging rate. Performance is reported using Pearson r, mean absolute error (MAE), systematic bias, and RMSE.

💡 Data fallback
If GEO download fails, the notebook auto-generates synthetic beta-value matrices (biolearn.GeoData) with realistic age-correlated CpG trends, so all 14 clocks can be evaluated offline.
Clocks Evaluated
Clock	Generation	Output	Highlight
Horvath v1	1st gen	Age (yr)	Pan-tissue, 353 CpGs
Horvath v2	2nd gen	Age (yr)	Skin-blood clock, 391 CpGs
Hannum	1st gen	Age (yr)	Blood-specific, 71 CpGs
Lin	1st gen	Age (yr)	99-CpG blood clock
VidalBralo	1st gen	Age (yr)	8-CpG minimal clock
PhenoAge	2nd gen	Age (yr)	Clinical biomarker-trained
HRSInCHPhenoAge	2nd gen	Age (yr)	Household survey cohort
YingCausAge	3rd gen	Age (yr)	Causal inference framework
YingDamAge	3rd gen	Age (yr)	DNA-damage component
YingAdaptAge	3rd gen	Age (yr)	Adaptive component
StocP	Stochastic	Age (yr)	Poisson model
StocH	Stochastic	Age (yr)	Heterodyne model
AltumAge	Deep learning	Age (yr)	Neural network, all CpGs
DunedinPACE	Pace clock	Rate	Longitudinal pace-of-aging
04
Visualisations
Clock-vs-Clock Pearson Correlation — GSE40279 (n=656)
ChronAge
Horvathv1
Horvathv2
Hannum
Lin
VidalBralo
PhenoAge
YingCausAge
YingDamAge
YingAdaptAge
StocP
StocH
AltumAge
−1
0
+1
Pearson r
Fig 2 · V1. Lower-triangle Pearson correlation matrix. First-generation clocks (Horvath v1/v2, Hannum) cluster tightly. Stochastic clocks (StocP, StocH) and VidalBralo show weaker inter-clock correlations, suggesting they capture distinct methylation signal.
Age Deviation Heatmap — GSE40279 (samples sorted youngest → oldest)
Clock
Horvathv1
Horvathv2
Hannum
PhenoAge
AltumAge
YingCausAge
StocP
StocH
Samples sorted youngest → oldest
−10 yr
+10 yr
Δ Age
Fig 3 · V2. Age deviation (predicted − chronological) heatmap. Blue = underestimation, red = overestimation. Most first-gen clocks underestimate age in young samples and overestimate in older samples—a classic regression-to-mean artefact.
MAE Comparison — 13 Aging Clocks × 2 Datasets
0
5
10
15
20
MAE (years)
Horvathv1
Horvathv2
Hannum
Lin
VidalBralo
PhenoAge
YingCausAge
YingDamAge
YingAdaptAge
StocP
StocH
AltumAge
HRSInCH
GSE40279
GSE41169
Fig 4 · V4. MAE comparison across all 13 age-clocks and both datasets. AltumAge (deep-learning) and YingCausAge achieve lowest MAE. Stochastic clocks (StocP, StocH) show highest error, possibly reflecting their design intent for cohort-level rather than individual-level prediction.
Predicted-Age Violin Distribution — GSE40279 (n=656)
20
40
60
80
100
Horvathv1
Horvathv2
Hannum
Lin
VidalBralo
PhenoAge
YingCausAge
YingDamAge
YingAdaptAge
StocP
StocH
AltumAge
HRSInCH
Chronological age range / median
Fig 5 · V5. Predicted-age violin distributions. The green band marks the chronological age range; the dashed line shows the median. Clocks aligned with the band indicate calibrated predictions. StocP/StocH show the widest spread.
05
Installation
pip install biolearn torch numpy pandas scipy matplotlib seaborn
Dependencies
Package	Role
biolearn	Clock models & GEO data loader
torch	Required by AltumAge (deep-learning clock)
pandas / numpy	Data manipulation & numerics
scipy	Pearson correlation
matplotlib / seaborn	All five figure types
06
Usage
Open the notebook and run all cells in order:

jupyter notebook epigenetics_aging_analysis.ipynb
⚙️ Configuration flag
Set USE_REAL_DATA = False near the top of the notebook to run entirely on synthetic data if GEO servers are unavailable or for fast iteration.
Cell Execution Order
Install — pip dependencies
Imports & Config — paths, clock names, plot settings
Data Loading — GEO fetch or synthetic fallback
Run All 14 Clocks — predictions via ModelGallery
Compute Metrics — r, MAE, bias, RMSE → CSVs
V1–V5 — five visualisation cells
Summary Report — results/summary.md
07
Metrics Reference
Metric	Formula	Interpretation
Pearson r	pearsonr(y, ŷ)	Linear correlation; higher = better tracking of age
MAE	mean(|ŷ − y|)	Average absolute error in years; lower = better
Bias	mean(ŷ − y)	Signed average error; +ve = overestimation
RMSE	√mean((ŷ−y)²)	Penalises large errors more than MAE
08
Key References
Horvath S. (2013). DNA methylation age of human tissues and cell types. Genome Biology.
Hannum G. et al. (2013). Genome-wide methylation profiles reveal quantitative views of human aging rates. Molecular Cell.
Levine M.E. et al. (2018). An epigenetic biomarker of aging for lifespan and healthspan. Aging.
Ying K. et al. (2024). Causal basis of the aging methylome. Nature Aging.
Belsky D.W. et al. (2022). DunedinPACE: A DNA methylation biomarker of the pace of aging. eLife.
biolearn library — bio-learn.github.io
Aarish Sajid · 454572 · BI-436, NUST SINES · Spring 2026
Generated from epigenetics_aging_analysis.ipynb
