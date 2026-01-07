# Multimodal Property Valuation


**Goal**: Build a multimodal regression pipeline that predicts property price by combining tabular housing data with satellite imagery around each property.


## Contents
- `scripts/data_fetcher.py` — script to download satellite images from Mapbox (or other provider).
- `notebooks/preprocessing.ipynb` — EDA, geospatial feature engineering, image checks.
- `notebooks/model_training.ipynb` — training multimodal model (PyTorch), evaluation, Grad-CAM explainability, export predictions CSV.


## Quick-start


1. Create a Python 3.10+ environment and install dependencies:


```bash
python -m venv venv
source venv/bin/activate # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```


2. Put your data files in `data/raw/`:
- `train(1).xlsx` (contains `id`, `price`, `bedrooms`, `bathrooms`, `sqft_living`, `lat`, `long`, ...)
- `test2.xlsx` (same columns except `price`)


3. Set your Mapbox token (or other API key) as an environment variable:


```bash
export MAPBOX_TOKEN="pk.your_token_here"
```


4. Download images for train and test:


```bash
python scripts/data_fetcher.py --input data/raw/train(1).xlsx --outdir data/images/train --api mapbox --token $MAPBOX_TOKEN --zoom 17 --size 512
python scripts/data_fetcher.py --input data/raw/test2.xlsx --outdir data/images/test --api mapbox --token $MAPBOX_TOKEN --zoom 17 --size 512
```


5. Open `notebooks/preprocessing.ipynb` and run the cells to prepare the dataset and create PyTorch datasets.


6. Run `notebooks/model_training.ipynb` to train the model and produce `predictions.csv` in the repository root.


## Mapbox token (short)
- Create a Mapbox account at https://account.mapbox.com.
- From the dashboard go to Access Tokens -> copy your Default public token or create a new token with the `styles:tiles`/`styles:read` or `styles:tiles` scope.


(See notebooks for a full guide and code.)


## Notes
- The repository is intentionally modular. You can swap Mapbox for Google Static Maps or Sentinel Hub by editing `scripts/data_fetcher.py`.
- Be careful with API rate limits and costs. Test with a small subset before downloading all images.
