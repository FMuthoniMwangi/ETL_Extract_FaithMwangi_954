# ETL Lab

**Student:** Faith Mwangi  
**Student ID:** ***954  
**Course:** DSA 2040A  
**Lab:** Extraction in ETL

---

## Project Description

This project demonstrates the development of an ETL (Extract, Transform, Load) pipeline using a synthetic Kenyan transaction dataset. The workflow covers full extraction, incremental extraction, data transformation, and data loading into a structured database.

---

## Lab 3: ETL Extract Lab

Sample M-Pesa and supermarket sales data are generated and subjected to both full and incremental extraction. Extraction timestamps are tracked to ensure only new or updated records are captured during incremental runs.

---

## Lab 4: Transform in ETL

The transformation phase includes:
- Removal of duplicate transactions.
- Addition of a `transaction_fee` column (1.5% of the transaction amount).
- Standardization of date fields to the `YYYY-MM-DD` format.
- Categorization of transactions by amount (Small, Medium, Large).

Transformed results are available in `transformed_full.csv` and `transformed_incremental.csv`.

---

## Lab 5 – Load

Transformed datasets (`transformed_full.csv` and `transformed_incremental.csv`) are loaded into structured formats using SQLite databases.

**Method:**  
- Python and pandas are used to load the data into `.db` files located in the `loaded_data/` directory.

**Sample Code:**
```python
import pandas as pd
import sqlite3

# Load the full dataset
df_full = pd.read_csv("transformed_full.csv")
conn_full = sqlite3.connect("loaded_data/full_data.db")
df_full.to_sql("full_data", conn_full, if_exists="replace", index=False)
conn_full.close()

# Load the incremental dataset
df_inc = pd.read_csv("transformed_incremental.csv")
conn_inc = sqlite3.connect("loaded_data/incremental_data.db")
df_inc.to_sql("incremental_data", conn_inc, if_exists="replace", index=False)
conn_inc.close()
```

**Outputs:**  
- SQLite: `loaded_data/full_data.db`, `loaded_data/incremental_data.db`

---

## Tools Used

- Python 3
- pandas
- Jupyter Notebook

---

## File Structure

```
ETL_Extract_FMuthoniMwangi_669954/
├── etl_extract.ipynb
├── custom_data.csv
├── last_extraction.txt
├── transformed_full.csv
├── transformed_incremental.csv
├── loaded_data/
│   ├── full_data.db
│   └── incremental_data.db
├── .gitignore
├── README.md
```

---

## How to Run

1. **Clone the Repository**

```sh
git clone https://github.com/FMuthoniMwangi/ETL_Extract_FMuthoniMwangi_669954.git
cd ETL_Extract_FMuthoniMwangi_669954
```

2. **Install Dependencies**

```sh
pip install pandas jupyter
```

3. **Start Jupyter Notebook**

```sh
jupyter notebook
```
Open `etl_extract.ipynb` and execute the cells as instructed. This will generate data and demonstrate both extraction methods.

---

## Data Source

The dataset is synthetically generated to simulate 50 M-Pesa transactions at various Kenyan supermarkets and agents.  
Fields include transaction ID, customer phone, supermarket, agent, transaction type, amount, date, and last updated timestamp.

---

## Screenshots

### Extracting

#### Dataset Preview 
![Dataset Preview](images/image.png)

#### Full Extraction
![Full Extraction](images/image-1.png)

#### Incremental Extraction
![Incremental Extraction](images/image-2.png)

#### Timestamp Update
![Timestamp Update](images/image-3.png)

---

### Transforming

#### Full Data
![Full Data](images/image-4.png)

#### Incremental Data 
![Incremental Data](images/image-5.png)

---

## License

MIT License.