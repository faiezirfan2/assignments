Attempt-Before-AI: Data Audit & Diagnostic Log

Before consulting any AI tools or writing cleaning scripts, I performed an independent diagnostic audit of the raw dataset (teaching_prices_messy.csv). I loaded the dataset using pandas and ran the following checks to understand its structure and data types:

# raw = pd.read_csv("teaching_prices_messy.csv")
# raw.shape
# raw.info()
# raw.isna().sum()
# raw.duplicated().sum()
# raw['item'].value_counts(dropna=False)
# raw[raw.duplicated(keep=False)]
# number = pd.to_numeric(raw["price"],errors="coerce")
# print("missing before", raw["price"].isna().sum())
# print("missing after", number.isna().sum())  


Diagnosed Problems & Anomalies

Problem 1: Exact Duplicate Row
# raw.duplicated().sum()
 returned 1,  Inspecting with     #  raw[raw.duplicated(keep=False)] 
showed that Row 96 is an exact duplicate of Row 8          (Staple A, City 1, 2026-01-08, price 99.5).

Problem 2: Inconsistent Text Casing
# raw['item'].value_counts()  
revealed 24 entries for "Staple A",  "Oil B",  "Pulse C",  "Sweetener D", 
but 1 entry labeled lowercase "oil b" at index 40.



Problem 3: Missing Price Value
 #  raw.isna().sum() 
showed 1 missing value in the price column, specifically at index 5 (Pulse C, City 2, 2026-01-01).

Problem 4: Malformed and Outlier Prices
Converting prices to numeric revealed a string-formatted number with a comma ("1,250" at index 17) and an extreme, unrealistic outlier value (9999 at index 30 for Sweetener D).

Problem 5: Incorrect Data Types
The date column is stored as an object/string instead of a datetime datatype.


Planned Decisions 

Issue Found: Exact Duplicate (Row 96)
Planned Decision: Exclude / Drop
Reason : Removing exact duplicate rows prevents double-counting observations in time-series aggregates.

Issue Found: Lowercase Item Name ("oil b")
Planned Decision: Correct / Standardize
Reason : Standardizing text casing ensures proper categorical grouping and ensures item counts match expectations (24 per item).

Issue Found: Missing Price (NaN at Index 5)
Planned Decision: Investigate / Retain as NaN
Reason : Do not artificially impute prices without source verification; keep as missing so downstream analysis handles it appropriately.

Issue Found: String Price with Comma ("1,250")
Planned Decision: Correct / Convert
Reason / Justification: Strip the comma and cast to numeric float so mathematical and statistical functions can process it.

Issue Found: Extreme Outlier Price (9999 at Index 30)
Planned Decision: Flag & Exclude or  Correct
Reason / Justification: An extreme value of 9999 for sugar/sweetener is a data entry error; convert to NaN or flag for review.

Issue Found: Date Column Type (object)
Planned Decision: Correct
Reason / Justification: Convert column to proper datetime64 format to enable correct chronological sorting and filtering.
