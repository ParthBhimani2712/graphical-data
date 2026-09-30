# graphical-data: Auto MPG visualisation with seaborn

This is a small exploratory data-visualisation notebook built on the classic **Auto MPG** cars dataset (loaded through `seaborn.load_dataset('mpg')`). It adds two derived fuel-efficiency columns, prints summary statistics and draws three seaborn charts: horsepower per car model, a stacked distribution of a horsepower × efficiency score by region of origin, and a KDE of acceleration against model year for high-scoring cars.

## Dataset

- **Source:** seaborn's built-in `mpg` dataset (the UCI Auto MPG data). It is fetched automatically, so no data file is included or needed.
- **Size:** 398 rows. `horsepower` has 392 non-null values.
- **Original columns:** `mpg`, `cylinders`, `displacement`, `horsepower`, `weight`, `acceleration`, `model_year`, `origin` (usa / europe / japan), `name`.
- **Derived columns added in the notebook:**
  - `km/l` = `mpg × 0.425144` (miles per US gallon converted to kilometres per litre)
  - `hp/km` = `km/l × horsepower`. Despite the name, this is a product of efficiency and power, not horsepower per kilometre.

## What the notebook does

1. Loads the data and adds the `km/l` and `hp/km` columns.
2. Runs `df.describe()` for summary statistics (for example, mean mpg is 23.51 with a range of 9.0 to 46.6, and mean horsepower is 104.5 with a range of 46 to 230).
3. Draws a **bar plot** of `horsepower` for every car `name` (a tall 10×50 figure).
4. Draws a **stacked histogram** of `hp/km` coloured by `origin`, on a log-scaled x-axis.
5. Draws a **bivariate KDE plot** of `acceleration` against `model_year` for cars with `hp/km >= 1000`, coloured by `cylinders`.

## Results

This is purely descriptive: no model is trained and no metrics are reported. The outputs are the summary table and the three figures saved inside the notebook.

## How to run

```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook cars_dataset.ipynb
```

An internet connection is needed the first time, because `sns.load_dataset` downloads the data.

## Repository structure

```
graphical-data/
├── cars_dataset.ipynb   # the analysis and plots
└── README.md
```

## Notes and limitations

- The `hp/km` column name is misleading, since the value is `km/l × horsepower`.
- The KDE plot emits a "KDE cannot be estimated (0 variance)" warning because some `cylinders` groups have too few (or identical) points after the `hp/km >= 1000` filter.
- The per-car bar plot has hundreds of labels and is hard to read at normal sizes.
