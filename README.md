
# Zoonotic Foodborne Disease Surveillance (ECDC, EU/EEA, 2022–2024)

This repository provides a reproducible workflow for analyzing **confirmed cases** of three major zoonotic foodborne diseases using official data from the **European Centre for Disease Prevention and Control (ECDC) Surveillance Atlas of Infectious Diseases**:

- **Campylobacteriosis**
- **Salmonellosis**
- **Listeriosis**

The analysis aggregates total **EU/EEA case counts** for **2022–2024** and generates summary tables and figures.

All processing and figure generation are implemented in:

`zoonoses_2022_2024_analysis.ipynb`

---

## 1. Repository Structure

```
.
├── data/
│   ├── ECDC_surveillance_data_Campylobacteriosis.csv
│   ├── ECDC_surveillance_data_Salmonellosis.csv
│   └── ECDC_surveillance_data_Listeriosis.csv
│
├── output/
│   ├── ECDC_totals_2022_2024_by_disease.csv
│   ├── ECDC_totals_2022_2024_by_disease.png
│   └── ECDC_totals_2022_2024_by_disease.pdf
│
├── zoonoses_2022_2024_analysis.ipynb
└── README.md
```

---

## 2. Input Data (Manual Download Required)

### 2.1 ECDC Surveillance Atlas of Infectious Diseases

**Official data portal:**  
https://atlas.ecdc.europa.eu/public/index.aspx  

The ECDC Atlas structures downloads using two key filters:

- **Indicator** → how the metric is expressed (e.g., counts vs. notification rates)
- **Subpopulation** → case definition (e.g., confirmed cases)

### Correct Download Settings

To obtain **confirmed case counts**, apply the following filters:

- **Indicator:** Reported cases  
- **Subpopulation:** Confirmed cases  
- **Years:** 2024  
- **Diseases (download separately):**
  - Campylobacteriosis
  - Salmonellosis
  - Listeriosis
- **Geographical coverage:** EU/EEA (country level; default view)

**Important note on years:**  
The 2024 ECDC release already contains the full validated historical time series. Therefore, separate downloads for 2022 and 2023 are not required.

---

### Download Instructions

1. Open the ECDC Surveillance Atlas:
   https://atlas.ecdc.europa.eu/public/index.aspx

2. Apply the filters listed above.

3. For each disease, click:
   **Download → CSV**

4. Save the files *without renaming* into:

```
data/
```

Expected filenames:

```
ECDC_surveillance_data_Campylobacteriosis.csv
ECDC_surveillance_data_Salmonellosis.csv
ECDC_surveillance_data_Listeriosis.csv
```

---

## 3. Selection Criteria and Case Definition

All records used in this analysis satisfy:

- **Case classification:** Confirmed cases  
- **Measure:** Annual reported cases (counts)  
- **Geographic level:** Country (EU/EEA)

Where notification rates (N/100000) are encountered, absolute counts are reconstructed using population denominators provided in the file.

---

## 4. Method Summary

1. Load disease-specific CSV files from the `data/` directory.

2. Validate that the **Indicator** field is equal to:
   - `Reported cases`

3. Filter to **EU/EEA country-level records** only.

4. Standardize disease labels across files.

5. Handle mixed units:
   - `N` → direct case counts  
   - `N/100000` → converted to raw counts using population

6. Aggregate **total EU/EEA cases** by:
   - Disease
   - Year (2022–2024)

7. Generate publication-quality bar plots of:
   - Total annual cases by disease

8. Export final summary tables and figures to the `output/` directory.

---

## 5. How to Run

### Requirements
- Python ≥ 3.9  
- pandas  
- numpy  
- matplotlib  
- jupyter  

### Install

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
python -m pip install --upgrade pip
pip install pandas numpy matplotlib jupyter
```

### Run

```bash
jupyter notebook
```

Open:

```
zoonoses_2022_2024_analysis.ipynb
```

---

## 6. Data Sources

European Centre for Disease Prevention and Control (ECDC).  
*Surveillance Atlas of Infectious Diseases.*  
https://atlas.ecdc.europa.eu/public/index.aspx

---

## License

- **Code:**  
  MIT License.

- **Data:**  
  This repository uses third-party datasets that are subject to their own licenses and terms of use, including data from the European Centre for Disease Prevention and Control (ECDC).  
  Users should consult the ECDC Surveillance Atlas for licensing and usage conditions.

