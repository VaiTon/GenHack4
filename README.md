# GenHack - ChefAI: Urban Heat Island Risk Prediction

<p align="center">
  <img src="logos/week1.png" width="120" />
  <img src="logos/week2.png" width="120" />
  <img src="logos/week3.png" width="120" />
  <img src="logos/week4.png" width="120" />
</p>

**Team**: ChefAI

- [@VaiTon](https://github.com/VaiTon)
- [@andreeado](https://github.com/andreeado)
- [@mpreda01](https://github.com/mpreda01)
- [@Torna99](https://github.com/Torna99)

**Project**: Predictive Modeling of Urban Heat Island (UHI) Risk Levels

## 🎯 Challenge Overview

**GenHack 2025** is a four-week collaborative hackathon on Urban Heat Islands and Climate Downscaling, organized by the **BNP Paribas "Stress Test" Chair** and **École Polytechnique**.

This challenge explores the **Urban Heat Island (UHI) effect** using:

- **ERA5 temperature data** - Global climate reanalysis
- **Sentinel-2 NDVI maps** - Vegetation indices from satellite imagery
- **Ground-station observations** - High-quality weather station measurements

The goal is to understand and model local climate variations, bridging the gap between coarse-resolution satellite data and fine-scale urban microclimate reality.

## 📋 Project Overview

This four-week journey explores the **Urban Heat Island (UHI) effect** focusing on **Bologna and the Emilia-Romagna region** in northern Italy, progressing from data exploration to predictive modeling. The project investigates how well satellite-based climate reanalysis (ERA5) captures urban heat patterns compared to ground-based weather station measurements in this diverse landscape of urban centers, agricultural plains, and mountainous areas.

### Four-Week Structure

**Week 1 - Data Exploration**: Understanding GADM administrative boundaries, ERA5 climate data structure, and ECA&D weather station networks across Europe.

**Week 2 - Visualizing UHI**: Analyzing temperature patterns in Bologna and Emilia-Romagna, exploring relationships between NDVI (vegetation), DEGURBA (urbanization), and observed temperature anomalies.

**Week 3 - Quantitative Metrics**: Computing UHI discrepancies between ERA5 satellite estimates and ground station measurements across 70+ stations, identifying systematic biases in urban areas.

**Week 4 - Predictive Modeling**: Building machine learning classifiers to predict UHI discrepancy risk levels, discovering that urbanization density and vegetation are the strongest predictors.

### Key Discovery

Through our analysis, we discovered that **ERA5 systematically underestimates urban heat** in dense cities. Classification models can effectively predict **Low, Medium, or High UHI discrepancy risk** levels using:

- **Urbanization level** (DEGURBA) - Most critical factor
- **Vegetation index** (NDVI) - Strong predictor of urban heat retention
- **Meteorological features** (temperature, wind, precipitation from ERA5)
- **Geographic features** (elevation, coordinates)

This approach identifies priority areas where satellite-based climate data fails to capture localized urban microclimate effects.

## 🗂️ Project Structure

```
GenHack/
├── 1_exploration/          # Week 1: Data exploration
│   ├── era5_data_exploration.ipynb      # ERA5 NetCDF climate reanalysis
│   ├── gadm_exploration.ipynb           # Administrative boundaries (Italy/Europe)
│   └── tx_data_exploration.ipynb        # ECA&D weather station temperatures
├── 2_explain/              # Week 2: UHI visualization
│   └── week2_team29.ipynb               # Bologna/Emilia-Romagna UHI patterns
├── 3_metrics/              # Week 3: Discrepancy quantification
│   └── week3_team29.ipynb               # ERA5 vs ground truth comparison (19 quarters)
├── 4_model/                # Week 4: ML risk classification
│   └── week4_team29.ipynb               # Random Forest/XGBoost predictive models
├── data/                   # Raw input data
│   ├── degurba.csv                      # EU urbanization classification (download separately)
│   ├── gadm_410_europe.gpkg             # GADM v4.1 administrative polygons
│   ├── derived-era5-land-daily-statistics/  # ERA5 2020-2025 daily NetCDF files
│   └── sentinel2_ndvi/                  # Sentinel-2 vegetation indices (10m)
├── processed/              # Processed datasets
│   ├── ECA_blend_tx/                    # 70+ Italian weather stations (TX)
│   └── uhi_discrepancy_*.parquet        # Week 3 output: 1.75M ERA5-ECA comparisons
└── README.md
```

## 📊 Data Sources

### 1. **ERA5 Climate Reanalysis** (Copernicus Climate Data Store)

- **Resolution**: 0.1° × 0.1° (~11km)
- **Variables**:
  - `t2m`: 2-meter temperature (K)
  - `u10`, `v10`: Wind components at 10m (m/s)
  - `tp`: Total precipitation (m)
- **Period**: 2020-2025
- **Format**: NetCDF files (EPSG:4326)

### 2. **ECA&D Station Data** (European Climate Assessment)

- **Stations**: 70+ weather stations in Emilia-Romagna region
- **Variable**: TX (daily maximum temperature)
- **Quality**: Ground truth measurements
- **Format**: Text files with station metadata
- **Coverage**: Bologna, Modena, Parma, and surrounding provinces

### 3. **DEGURBA Urbanization** (Eurostat)

- **Classification**:
  - Class 1: Cities (dense urban)
  - Class 2: Towns and suburbs
  - Class 3: Rural areas
- **Resolution**: 1km² grid cells aggregated to comuni
- **Format**: CSV with semicolon delimiter
- **Source**: [ISTAT - Degree of Urbanization](https://situas.istat.it/web/#/home/piu-consultati?id=73&dateFrom=2025-12-04)

### 4. **GADM Administrative Boundaries** (v4.1)

- **Level**: NAME_3 (comuni/municipalities)
- **Country**: Italy
- **CRS**: EPSG:4326 (WGS84)
- **Format**: GeoPackage

### 5. **Sentinel-2 NDVI** (Copernicus Sentinel)

- **Index**: Normalized Difference Vegetation Index
- **Purpose**: Proxy for urbanization/land cover
- **Resolution**: 10m

## 🔬 Methodology

### Week 1: Data Exploration & Understanding

- **Load and visualize** GADM administrative boundaries (European comuni/municipalities)
- **Inspect ERA5 NetCDF** files: understand coordinate systems, variables, temporal coverage
- **Parse ECA&D station data**: convert DMS coordinates, explore TX (max temperature) observations
- **Initial mapping**: plot station locations, ERA5 grid cells, administrative boundaries

### Week 2: UHI Visualization & Pattern Analysis

- **Focus region**: Emilia-Romagna (Bologna, Modena, Parma, other provinces)
- **Calculate urban-rural differences**: identify temperature anomalies in city centers vs countryside
- **NDVI integration**: correlate vegetation index with observed temperatures
- **DEGURBA classification**: overlay urbanization density on temperature maps
- **Visual storytelling**: create multi-panel maps showing UHI intensity across seasons

### Week 3: Quantitative Discrepancy Analysis

- **Study area**: Emilia-Romagna region (all provinces)
- **19 quarterly periods** (2020-2023): capture seasonal variations
- **Spatial join**: match 70+ ECA&D stations across the region with ERA5 grid cells (nearest neighbor)
- **UHI computation**:
  - **ECA UHI**: Ground truth urban-rural temperature difference from stations
  - **ERA5 UHI**: Satellite-estimated urban-rural difference from reanalysis
  - **Discrepancy**: `abs(ECA_UHI - ERA5_UHI)` — how much ERA5 misses
- **Statistical analysis**: correlate discrepancy with NDVI, elevation, DEGURBA, wind, precipitation
- **Output**: 1.75M row dataset with discrepancies for all station-date combinations

### Week 4: Machine Learning Risk Prediction

- **Risk binning**: Quantile-based classification (Low/Medium/High at 33rd/67th percentiles)
- **Feature engineering**: 8 predictive variables (DEGURBA, NDVI, ERA5 climate, elevation)
- **Model comparison**: Train 8 algorithms (Random Forest, XGBoost, Neural Networks, etc.)
- **Validation**: 80/20 train/test split with stratification
- **Feature importance**: Discover DEGURBA and NDVI as dominant predictors
- **Best model**: Random Forest achieves ~66% accuracy (vs 33% random baseline)

## 🚀 Getting Started

### Prerequisites

- **Python 3.12+**
- **uv** - Python package installer ([install uv](https://github.com/astral-sh/uv))

**Required packages**:

```
pandas numpy matplotlib seaborn geopandas scikit-learn xgboost netCDF4 xarray rioxarray tqdm
```

### Installation

```bash
# Clone repository
git clone <repository-url>
cd GenHack

# Create virtual environment and install dependencies with uv (fast!)
uv venv  # create .venv
uv sync  # install packages
source .venv/bin/activate.fish  # or: source .venv/bin/activate (bash/zsh)

# Download and extract data archive
# Download genhack.tar.zst from: https://drive.google.com/file/d/16F2AAG0bG-iARXSaO1rsOLKTZUmh2Es7/view?usp=sharing
tar xvf genhack.tar.zst

# Download DEGURBA urbanization data
wget -O data/degurba.csv <DEGURBA_CSV_URL>
# Or manually download from: https://situas.istat.it/web/#/home/piu-consultati?id=73&dateFrom=2025-12-04
# and save as data/degurba.csv

# Open notebooks with VS Code (recommended)
code .

# Or launch Jupyter Lab
jupyter lab

# Or use classic Jupyter Notebook
jupyter notebook
```

### Running the Analysis

**Week-by-week progression** (open in VS Code or Jupyter Lab):

```bash
# Week 1: Explore individual datasets
1_exploration/gadm_exploration.ipynb
1_exploration/era5_data_exploration.ipynb
1_exploration/tx_data_exploration.ipynb
# Week 1: Main notebook
1_exploration/week1_team29.ipynb

# Week 2: Visualize UHI in Bologna/Emilia-Romagna
2_explain/week2_team29.ipynb

# Week 3: Compute ERA5 vs ground truth discrepancies
3_metrics/week3_team29.ipynb
# Output: processed/uhi_discrepancy_eca_era5_stats_all_regions.parquet

# Week 4: Train ML classifiers for risk prediction
4_model/week4_team29.ipynb
```

**Key outputs**:

- Week 2: UHI visualization maps (Bologna urban core vs rural areas)
- Week 3: Discrepancy statistics, correlation analyses, 1.75M measurement dataset
- Week 4: Trained Random Forest classifier, feature importance scores, confusion matrices

## 📈 Key Results

### Core Hypothesis Validation (Week 3)

✅ **Confirmed**: ERA5 discrepancies are **3× larger in dense urban areas** (DEGURBA=1) compared to rural areas (DEGURBA=3)

✅ **Confirmed**: **Low vegetation** (NDVI < 0.3) correlates strongly with high discrepancies

✅ **Confirmed**: ERA5's ~30km resolution **systematically underestimates** localized urban heat islands captured by ground stations

### Model Performance (Week 4)

| Model               | Accuracy  | F1 Score  | Key Characteristic            |
| ------------------- | --------- | --------- | ----------------------------- |
| Random Forest ⭐    | **66.2%** | **0.661** | Best overall, fast training   |
| XGBoost             | 65.8%     | 0.657     | Close second, handles missing |
| Gradient Boosting   | 65.4%     | 0.653     | Sequential boosting           |
| Logistic Regression | 60.1%     | 0.599     | Linear baseline               |
| Neural Network      | 59.8%     | 0.597     | Slow, requires more data      |

_Baseline (random guessing): 33.3% accuracy_

### Feature Importance Ranking

1. **DEGURBA** (urbanization class) — **Critical** (importance: 0.28)
   - Cities (class 1) have 3× higher discrepancy risk than rural areas
2. **NDVI** (vegetation index) — **High** (importance: 0.22)
   - Lower vegetation = more concrete = larger ERA5 blind spots
3. **ERA5_t2m** (2m temperature) — **High** (importance: 0.18)
   - Base temperature influences UHI magnitude
4. **HGHT** (elevation) — **Moderate** (importance: 0.12)
   - Altitude affects atmospheric mixing and heat retention
5. **ERA5_UHI** (satellite UHI estimate) — **Moderate** (importance: 0.08)
   - ERA5's own UHI calculation has some predictive signal

## 📍 Use Cases

### Urban Planning

- **Prioritize** cooling infrastructure investments in high-risk zones
- **Monitor** medium-risk areas with enhanced vegetation strategies
- **Validate** satellite-based UHI estimates with ground measurements

### Climate Adaptation

- **Identify** vulnerable neighborhoods for heat wave early warning
- **Optimize** green space planning based on predicted UHI risk
- **Assess** effectiveness of mitigation measures over time

### Policy Support

- **Evidence-based** zoning decisions for new developments
- **Risk-stratified** building code requirements (cool roofs, etc.)
- **Performance metrics** for city climate action plans

## 📝 License

This project was developed as part of the GenHack challenge.

## 👥 Team ChefAI

Contributors to this analysis and model development.

## 🙏 Acknowledgments

- **Copernicus Climate Change Service** - ERA5 reanalysis data
- **European Climate Assessment & Dataset** - Ground station measurements
- **Eurostat** - DEGURBA urbanization classification
- **GADM** - Administrative boundary data
- **ESA Copernicus** - Sentinel-2 NDVI data

## 📧 Contact

For questions or collaboration opportunities, please open an issue in this repository.

---

**Note**: This is a research project for educational purposes. The authors do not guarantee the accuracy or applicability of the models for operational use. Please refer to original data sources and domain experts for critical applications.
