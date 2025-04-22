# NYT-Restaurant-Reviews


**Overview**\
A reproducible pipeline to collect, preprocess, enrich, and model data from The New York Times restaurant reviews, with a focus on detecting potential geographic or socioeconomic indicators to determine likelihood of restaurants getting reviwed by the NYT. Workflows include web scraping, data cleaning, census-based feature augmentation, NLP on review text, and predictive modeling with XGBoost.

**Repository Structure**

```
├── notebooks/                      # Analysis and pipeline notebooks
│   ├── 00_NYTRestaurantReviews_DataCollection.ipynb  # Scrape & ingest review data
│   ├── 02_Preprocessing.ipynb      # Clean & normalize raw data
│   ├── 07_Census_data.ipynb         # Pull & join Census demographic features
│   ├── 08_ModelingDataset.ipynb     # Assemble and engineer model-ready dataset
│   ├── 09_NLP.ipynb                 # Natural language processing on reviews
│   └── 12.XGBoost.ipynb             # Train & evaluate XGBoost classification model
├── data/                           # (Git‑ignored) raw & processed data files
│   ├── raw/                        
│   └── processed/                  
├── requirements.txt               # Python package dependencies
├── environment.yml                # Conda environment specification
└── README.md                      # Project overview and instructions
```

**Getting Started**

1. **Clone the repo**

   ```bash
   git clone https://github.com/<your-org>/nyt-restaurant-bias.git
   cd nyt-restaurant-bias
   ```

2. **Set up environment**

   - **Using Conda**:
     ```bash
     conda env create -f environment.yml
     conda activate nyt-bias
     ```
   - **Using pip**:
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     pip install -r requirements.txt
     ```

3. **Prepare data directories**

   ```bash
   mkdir -p data/raw data/processed
   ```

4. **Run Notebooks**

   - Launch Jupyter Lab/Notebook:
     ```bash
     jupyter lab
     ```
   - Execute each notebook in numeric order (00 → 02 → 07 → 08 → 09 → 12).

**Notebook Descriptions**

- **00\_NYTRestaurantReviews\_DataCollection.ipynb**: Automates scraping of NYT restaurant review pages (Selenium + BeautifulSoup), saving raw JSON/CSV outputs under `data/raw/`.
- **02\_Preprocessing.ipynb**: Cleans raw tables, handles missing values, standardizes date & location fields; exports to `data/processed/preprocessed_reviews.csv`.
- **07\_Census\_data.ipynb**: Fetches US Census demographic variables for each restaurant’s census tract; merges into processed reviews.
- **08\_ModelingDataset.ipynb**: Combines preprocessed review data with Census features, engineers additional variables (e.g., price tier, borough indicators).
- **09\_NLP.ipynb**: Applies NLP techniques (e.g., tokenization, sentiment analysis, topic modeling) to review text, generating text-based features.
- **12.XGBoost.ipynb**: Builds, tunes, and evaluates an XGBoost model to predict whether a restaurant receives a “Critics Pick,” with metrics and SHAP-based interpretability.

**Usage Examples**

- **Quick model run**:
  ```bash
  # After running through preprocessing and dataset creation
  jupyter nbconvert --execute --to notebook --inplace notebooks/12.XGBoost.ipynb
  ```
- **Extract feature importance**:
  ```python
  import shap
  model = ...  # loaded from notebook
  shap.summary_plot(shap_values, X)
  ```

---

## Additional Documentation Suggestions

- **CONTRIBUTING.md**: Guidelines for code formatting, branch strategy, and pull-request workflow.
- **LICENSE**: Choose an open‑source license (e.g., MIT, Apache 2.0).
- **DATA\_DICTIONARY.md**: Describe each column in raw and processed datasets, including source and transformations.
- **MODEL\_REPORT.md**: Summarize model performance, evaluation metrics, and deployment considerations.
- **.gitignore**: Exclude data directories and environment artifacts (`venv/`, `*.csv`, `__pycache__/`).
- **docs/** folder: Host rendered HTML/docs (e.g., Sphinx or MkDocs) for detailed API and pipeline documentation.
- **requirements.txt** or **environment.yml**: Ensure dependencies are up to date and pinned.
- **Jenkinsfile** or **GitHub Actions workflow**: Automate testing/notebook execution on push.


