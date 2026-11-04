# Helsinki Air Pollution: Weather, Traffic & Sensitivity Analysis

**Python | Regression | Monte Carlo Simulation | Sensitivity Analysis | Environmental Analytics**

A Python-based analysis of how weather and traffic relate to air pollution in Helsinki. The project combines hourly traffic, meteorological and air-quality observations and examines **nitrogen dioxide (NO₂)** and **black carbon (BC)** using regression, scenario analysis, uncertainty propagation and sensitivity-analysis methods.

This repository documents the coursework project *Impact of Weather and Traffic on Air Pollution: An Uncertainty and Sensitivity Analysis* (System Dynamics with Applications, February 2026).

## Project objective

- Combine traffic, weather and air-pollution measurements into a common hourly dataset.
- Explore the modeled relationships between weather, traffic volume, NO₂ and black carbon.
- Compare the influence of uncertain inputs using local and global sensitivity methods.
- Examine illustrative traffic-reduction scenarios and visualize how combinations of conditions affect modeled pollution.

## Project workflow

1. **Data preparation:** Align hourly timestamps, select traffic counter 32, combine traffic/weather/pollution data, interpolate missing weather values and export an analytical dataset.
2. **Modeling:** Fit regression-based models to describe traffic volume and pollution indicators.
3. **Sensitivity analysis:** Explore one-at-a-time and two-at-a-time input changes; calculate Morris and Sobol indices.
4. **Uncertainty and scenarios:** Examine modeled outcomes with Monte Carlo sampling and traffic-reduction scenarios.
5. **Visualization:** Use histograms, heatmaps, SimDec and parallel-coordinate plots to communicate model behavior.

## Key findings reported in the analysis

- **Wind speed** was an important variable in the modeled NO₂ results, consistent with the role of atmospheric dispersion.
- **Snow depth** was among the most influential variables in the modeled black carbon results.
- Traffic-reduction scenarios of 0%, 20% and 40% produced only small changes in modeled median NO₂ under the assumptions used in the report (approximately **9.190**, **9.188** and **9.185 µg/m³**, respectively).
- The simulated distributions and visualizations suggest that high-pollution outcomes may be associated with particular combinations of weather and traffic conditions rather than average conditions alone.

**Interpretation:** These findings describe the fitted models and scenario assumptions, **not causal proof or independently validated policy effects**. The model should not be treated as a production forecasting system.

## Data

The project draws from publicly documented Helsinki-area data sources:

| Data | Source | Role |
|---|---|---|
| Traffic counts | [Helsinki Region Infoshare](https://hri.fi/en_gb/) | Traffic volume at the selected counter |
| Weather observations | [Finnish Meteorological Institute](https://en.ilmatieteenlaitos.fi/download-observations) | Meteorological inputs from Kaisaniemi |
| Air-quality observations | [Helsinki Region Environmental Services (HSY)](https://www.hsy.fi/en/) | Pollution data from Kallio |

The provided analysis dataset contains **12,696 merged hourly records and 16 columns**. Original collection periods and time-zone handling should be verified against source documentation before interpreting the exact observation coverage.

### Repository files

```text
helsinki-air-pollution-sensitivity-analysis/
├── README.md
├── notebooks/
│   ├── final-dataset.ipynb
│   └── System_dynamics.ipynb
├── data/
│   ├── raw/
│   │   ├── liva_hourly.csv
│   │   ├── weather.csv
│   │   └── kalio.csv
│   └── processed/
│       └── clean_dataset.csv
└── reports/
    └── Air_Pollution_Sensitivity_Analysis.pdf
```

- `final-dataset.ipynb`: data integration and construction of the analysis dataset.
- `System_dynamics.ipynb`: regression, scenario analysis, uncertainty analysis and visualization.
- `data/raw/liva_hourly.csv`: **counter-32 extract**, not the full multi-counter original traffic data. This reduces repository size; the original nearest-counter comparison across all counters cannot be independently repeated using this extract alone.
- `data/processed/clean_dataset.csv`: the dataset used by the analysis notebook.
- `reports/Air_Pollution_Sensitivity_Analysis.pdf`: course report describing the methods and results.

## Running the notebooks

Install the packages used by the analysis in an appropriate Python environment:

```bash
pip install pandas numpy matplotlib scikit-learn scipy SALib simdec plotly notebook
```

The notebooks currently reference CSV files by **bare filenames** (e.g. `pd.read_csv("clean_dataset.csv")`). Once uploaded into the folder structure above, **adjust the paths** to `../data/raw/...` in `final-dataset.ipynb` and `../data/processed/clean_dataset.csv` in `System_dynamics.ipynb` when running from the `notebooks/` directory. The data-construction notebook writes `clean_dataset.csv` to its working directory until its output path is updated.

**Reproducibility note:** The published processed dataset was produced during the original project workflow. A rerun against the provided source extracts produces the same 12,696 records and 16 columns, but some interpolated weather values differ from the published processed CSV. Investigate the upstream cleaning/interpolation steps before claiming exact row-by-row replication.

## Analysis methods

| Method | Purpose |
|---|---|
| Linear regression | Explore associations between weather, traffic and pollution outcomes |
| One-at-a-time sensitivity | See how modeled predictions respond to individual input changes |
| Two-at-a-time sensitivity | Explore joint variations such as wind speed and traffic |
| Traffic-reduction scenarios | Compare predicted NO₂ under illustrative reductions |
| Monte Carlo sampling | Explore the distribution of model outcomes under input uncertainty |
| Latin hypercube and Sobol sampling | Compare ways to cover an uncertain input space |
| Morris and Sobol sensitivity indices | Examine influential variables in the fitted models |
| SimDec and parallel coordinates | Visualize conditions associated with different modeled outcomes |

## Limitations

- This is an academic modeling exercise. Regression associations and sensitivity rankings do not establish causation.
- Observations come from particular traffic, weather and air-quality locations; results should not be generalized uncritically across Helsinki.
- Traffic-reduction scenarios are model simulations rather than observed impacts of implemented policies.
- The counter-32 repository extract does not preserve all source traffic counters used in the original selection procedure.
- Original input transformations and time-zone assumptions require additional verification for full end-to-end reproducibility.

## Attribution and AI assistance

Data sources are credited above and in the accompanying report. The report discloses that ChatGPT was used as a learning aid to understand concepts and help generate or fix code. Analysis choices, interpretations and limitations should be evaluated against the notebooks and cited source data.
