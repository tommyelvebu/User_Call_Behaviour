# phone call behaviour analysis

exploring outgoing call data from a small south african business (2022-2024). main goal is to understand what the "unknown" calls actually are and how the business line is being used.

## structure

- `data/raw/` - original csv files from kaggle
- `data/processed/` - cleaned stuff
- `data/features/` - engineered features for modeling
- `notebooks/` - jupyter notebooks
- `src/` - reusable code if needed
- `reports/figures/` - saved plots
- `reports/findings/` - notes and insights

## main questions

1. how much work-hour time goes to personal calls?
2. what are those "unknown" contacts - clients? social? prospects?
3. any interesting patterns in when/how calls are made?

## setup

```bash
pip install -r requirements.txt
```

## notebooks

run roughly in order, but feel free to jump around:
1. data exploration
2. feature engineering
3. supervised learning on labeled data
4. clustering the unknown category
5. business insights
