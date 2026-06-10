# 🛍️ Online Retail Customer Segmentation (RFM + K-Means)

An unsupervised machine learning project that segments online retail customers based on their purchasing behavior using **RFM analysis** (Recency, Frequency, Monetary Value) and **K-Means clustering**. The project covers the full pipeline — from raw transaction data cleaning and feature engineering to cluster visualization with PCA.

---

## 📁 Dataset

- **File:** `online_retail_II.xlsx`
- **Source:** UCI Online Retail II dataset
- **Sheets:** `Year 2009-2010`, `Year 2010-2011` (Sheet 1 used)
- **Features:** 8 columns representing transactional records

| Feature | Description |
|---|---|
| `Invoice` | Invoice number (6-digit = valid; prefixed with 'C' = cancellation, 'A' = adjustment) |
| `StockCode` | Product code (5-digit numeric, optionally followed by letters) |
| `Description` | Product name |
| `Quantity` | Number of units per transaction |
| `InvoiceDate` | Date and time of the invoice |
| `Price` | Unit price in GBP |
| `Customer ID` | Unique customer identifier |
| `Country` | Country of the customer |

---

## 🔍 Project Workflow

### 1. Exploratory Data Analysis (EDA)
- Null value checks across all columns
- Inspection of negative quantities (returns/cancellations)
- Invoice format analysis — identifying adjustment (`A`) and cancellation (`C`) prefixes
- StockCode format validation using regex patterns

### 2. Data Cleaning
- Filtered invoices to only valid 6-digit numeric invoices (removed cancellations and adjustments)
- Filtered StockCodes to standard numeric/alphanumeric formats
- Dropped rows with missing `Customer ID`
- Removed records where `Price == 0`
- Retained ~77% of original records after cleaning

### 3. Feature Engineering — RFM
Created a customer-level aggregated table with three RFM metrics:

| Feature | Definition |
|---|---|
| `MonetaryValue` | Total spend per customer (`Price × Quantity`) |
| `Frequency` | Number of unique invoices per customer |
| `Recency` | Days since last purchase relative to the most recent transaction in the dataset |

### 4. Preprocessing
- IQR-based outlier removal on `MonetaryValue` and `Frequency`
- `StandardScaler` applied to all three RFM features
- 3D scatter plots before and after scaling for visual validation

### 5. Optimal Cluster Selection
- Tested K from 2 to 12
- **Elbow Method** — inertia plotted across K values
- **Silhouette Score** — cohesion and separation measured across K values
- **Chosen K: 4**

### 6. Final Model & Visualization
- K-Means with `k=4`, `init='k-means++'`, `n_init=12`, `max_iter=1000`
- Cluster labels assigned back to the customer-level DataFrame
- **PCA** (2 components) applied for 2D cluster visualization

---

## 📊 Evaluation

| Method | Purpose |
|---|---|
| Inertia (Elbow) | Identifies the point of diminishing returns for increasing K |
| Silhouette Score | Measures cluster quality — how well-separated and cohesive clusters are |
| PCA Plot | 2D visualization of cluster structure after dimensionality reduction |

---

## 🛠️ Tech Stack

- **Language:** Python 3
- **Libraries:** pandas, NumPy, scikit-learn, Matplotlib, Seaborn, openpyxl

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/mahmoudibrahim55033/<repo-name>.git
   cd <repo-name>
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Launch the notebook:
   ```bash
   jupyter notebook retail.ipynb
   ```

> Make sure `online_retail_II.xlsx` is in the same directory as the notebook.

---

## 👤 Author

**mahmoudibrahim55033** — [GitHub Profile](https://github.com/mahmoudibrahim55033)
