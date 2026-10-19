# Titanic Survival Analysis

An exploratory data analysis (EDA) of Titanic passenger records. The Jupyter notebook inspects the data, reviews missing values, fills missing ages with the dataset's mean, creates a train/test split for later analysis, and visualizes survival patterns across passenger characteristics.

> **Scope:** This repository contains data exploration and visualizations. It does not train, evaluate, or save a machine-learning model.

## Project files

| File | Description |
| --- | --- |
| [`titanic-survival-analysis.ipynb`](./titanic-survival-analysis.ipynb) | Jupyter notebook containing the analysis and charts. |
| [`titanic.csv`](./titanic.csv) | Passenger dataset used by the notebook. |
| [`survival_rate_by_age_and_sex.png`](./survival_rate_by_age_and_sex.png) | Survival rate by age group and sex. |
| [`survival_rate_by_pclass.png`](./survival_rate_by_pclass.png) | Survival rate by passenger class. |
| [`titanic_category_bar_charts.png`](./titanic_category_bar_charts.png) | Passenger counts by sex, class, embarkation port, and sibling/spouse count, split by survival. |
| [`age_vs_fare_by_survived.png`](./age_vs_fare_by_survived.png) | Passenger age and fare, colored by survival. |
| [`requirements.txt`](./requirements.txt) | Python packages needed to run the notebook. |

## Dataset

The CSV contains **891 rows and 12 columns**:

`PassengerId`, `Survived`, `Pclass`, `Name`, `Sex`, `Age`, `SibSp`, `Parch`, `Ticket`, `Fare`, `Cabin`, and `Embarked`.

- `Survived`: 0 = did not survive; 1 = survived.
- `Pclass`: passenger ticket class (1st, 2nd, or 3rd).
- `SibSp` and `Parch`: counts of siblings/spouses and parents/children aboard.
- `Embarked`: port of embarkation.

In the supplied CSV, `Age` has 177 missing values, `Cabin` has 687, and `Embarked` has 2. The notebook fills missing `Age` values with the mean. It drops `Cabin` from the DataFrame and does not impute the missing `Embarked` values.

**Data provenance:** The notebook does not record the CSV's original download URL or redistribution terms. Before making the repository public, verify the dataset's source and license and add the appropriate attribution here.

## Analysis and techniques

The notebook uses:

1. **Data inspection:** first and last rows, column names, data types, summary statistics, and missing-value percentages.
2. **Missing-data visualization:** a Seaborn heatmap.
3. **Age imputation:** scikit-learn's `SimpleImputer` with the mean strategy.
4. **Train/test split:** `train_test_split` with a 20% test set and `random_state=42`. This prepares subsets only; there is no model training or evaluation.
5. **Exploratory visualizations:**
   - Age distribution by passenger class (boxen plot).
   - Age versus fare, colored by survival (scatter plot).
   - Passenger counts by sex, passenger class, embarkation port, and `SibSp`, grouped by survival (count plots).
   - Survival rate by passenger class (bar plot).
   - Survival rate by age group and sex (line plot). Age groups are 0–12, 13–18, 19–30, 31–45, 46–60, and 61+.

The notebook's plots are made with Matplotlib and Seaborn; table operations and summary calculations use pandas and NumPy.

### Important methodological notes

- Age imputation happens **before** the train/test split. For predictive modeling, calculate the imputation value from training data only to avoid data leakage.
- `Sex` and `Embarked` are still categorical strings in the split features; the notebook does not encode them.
- The split features include `Embarked`, which has two missing values in the CSV. Those values are not handled by the notebook.
- The split is not used for a classifier, so no predictive performance is reported.

## Run the notebook

Use Python 3.10 or newer, then from the project directory run:

```bash
python -m venv .venv
```

Activate the environment:

```bash
# Windows PowerShell
.\.venv\Scripts\Activate.ps1

# macOS / Linux
source .venv/bin/activate
```

Install the dependencies and launch Jupyter:

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

Open `titanic-survival-analysis.ipynb` and run the cells from top to bottom. Keep `titanic.csv` in the same directory as the notebook because the notebook reads it using a relative path.

The notebook saves the four gallery images listed above in the current working directory when the corresponding plotting cells are run.

## Dependencies

- Python
- Jupyter Notebook
- pandas
- NumPy
- scikit-learn
- Matplotlib
- Seaborn

See [`requirements.txt`](./requirements.txt) for the installable package list.

## License

No project license has been selected. Without a license, others generally do not have permission to reuse or redistribute this project's original work. Add a license only after choosing the terms you want; also verify that the dataset can be redistributed under those terms.
