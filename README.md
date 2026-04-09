# Machine Learning in Hydrology

**ERTH 4750/5750 — Machine Learning and Numerical Modeling in Hydrology**

**Author:** Lijing Wang (lijing.wang@uconn.edu) — University of Connecticut

Co-authored with Claude ;)

---

## Notebooks

### Tabular & Time-Series (CAMELS dataset — 671 US catchments)

| # | Notebook | Topic | Key concepts |
|---|----------|-------|--------------|
| 00 | [00_MLP.ipynb](00_MLP.ipynb) | Multilayer Perceptron | Feedforward networks, backpropagation, R², RMSE |
| 01 | [01_SHAP.ipynb](01_SHAP.ipynb) | Explainability & SHAP | Shapley values, beeswarm, dependence plots, spatial maps |
| 02 | [02_LSTM_dynamic_inputs.ipynb](02_LSTM_dynamic_inputs.ipynb) | LSTM — single catchment | Sequence modeling, NSE, chronological split, persistence baseline |
| 03 | [03_LSTM_static_dynamic_inputs.ipynb](03_LSTM_static_dynamic_inputs.ipynb) | EA-LSTM — all catchments | Entity-Aware LSTM, static + dynamic inputs, multi-catchment training ⚠️ training is slow — requires GPU |

### Image-Based Streamflow (Fenton River trail-camera photos)

| # | Notebook | Topic | Key concepts |
|---|----------|-------|--------------|
| 04 | [04_image_simple_cnn.ipynb](04_image_simple_cnn.ipynb) | Dataset exploration + Simple CNN | log-transform regression target, conv blocks, Grad-CAM++ |
| 05 | [05_image_resnet18.ipynb](05_image_resnet18.ipynb) | Pretrained ResNet-18 | Transfer learning, ImageNet normalisation, fine-tuning, Grad-CAM++ |

---

## Data

### Fenton River trail-camera photos — required for notebooks 04 & 05

989 daily noon photos (2020–2025) from a CTDEEP trail camera at USGS gauge 01121330 (Fenton River at Mansfield, CT), paired with USGS discharge measurements.

**Step 1 — Download from HuskyCT**
Download `Fenton_River_Trail_Camera_Daily_Photos.zip` from the course HuskyCT page. Do **not** unzip it.

**Step 2 — Upload to Google Drive**
Upload the zip file directly into `My Drive` (not inside any subfolder).

The notebooks handle the rest automatically — they detect Colab, mount Drive, unzip the dataset on first run, and set all paths.

---

### CAMELS — automatically downloaded

Notebooks 00–03 use the [CAMELS dataset](https://ral.ucar.edu/solutions/products/camels) (catchment attributes + daily discharge for 671 US catchments). It is downloaded automatically via `pygeohydro` on first run and cached locally.

### Maurer extended forcing — required for notebooks 02 & 03

Daily meteorological forcing (precipitation, temperature, solar radiation, vapor pressure, day length) for all 671 CAMELS catchments, 1980–2008, from [Newman et al. (2015)](https://doi.org/10.5194/hess-19-209-2015).

**Source:** [HydroShare](https://www.hydroshare.org/resource/17c896843cf940339c3c3496d0c1c077/)

#### Getting the data into Google Colab

The Maurer dataset (~200 MB zipped, with hundreds of subfolders) cannot be bundled in this repository. Do this once before running notebooks 02 or 03:

**Step 1 — Download the zip from HydroShare**
Go to [HydroShare](https://www.hydroshare.org/resource/17c896843cf940339c3c3496d0c1c077/) and download `maurer_extended.zip`. Do **not** unzip it.

**Step 2 — Upload the zip to your Google Drive root**
Upload `maurer_extended.zip` directly into `My Drive` (not inside any subfolder).

**Step 3 — The notebooks handle the rest**
The Colab setup cell detects the zip, unzips it into `My Drive/maurer_extended/`, and sets `MAURER_DIR` automatically. This only runs once — subsequent sessions skip the unzip step.

---

## Running on Google Colab

Click the Colab badge at the top of each notebook. No local installation needed — all packages are installed in the first code cell.

**Recommended workflow:**
1. Open the notebook in Colab via the badge
2. Go to **File → Save a copy in Drive** to keep your own editable version
3. Run the Colab setup cell (mounts Drive, sets `MAURER_DIR`)
4. Run remaining cells in order

---

## Running Locally

```bash
conda create -n ml_hydro python=3.12
conda activate ml_hydro
pip install numpy pandas matplotlib scikit-learn torch shap pygeohydro ipywidgets
```

Clone the repo and set `MAURER_DIR` in the setup cell to your local path.

---

## Dependencies

| Package | Purpose |
|---------|---------|
| `pygeohydro` | Download CAMELS attributes and discharge |
| `torch` | MLP and LSTM models |
| `shap` | SHAP explainability |
| `geopandas` | Spatial catchment maps |
| `ipywidgets` | Interactive dropdowns |
| `matplotlib` | All visualisations |

---

## References

### Image-Based Streamflow

- Goodling, P. J., Fair, J. H., Gupta, A., Walker, J. D., Dubreuil, T., Hayden, M., and Letcher, B. H. (2025). Technical note: A low-cost approach to monitoring relative streamflow dynamics in small headwater streams using time lapse imagery and a deep learning model. *Hydrology and Earth System Sciences*, 29, 6445–6460. https://doi.org/10.5194/hess-29-6445-2025

### Tabular & Time-Series

- Newman, A., et al. (2015). Development of a large-sample watershed-scale hydrometeorological dataset for the contiguous USA. *HESS*, 19, 209–223.
- Addor, N., et al. (2017). The CAMELS data set: catchment attributes and meteorology for large-sample studies. *HESS*, 21, 5293–5313.
- Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. *NeurIPS*.
- Kratzert, F., et al. (2019). Towards learning universal, regional, and local hydrological behaviors. *HESS*, 23, 5089–5110.
