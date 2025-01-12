# SQL/Panda Mappings

# **Basic Operation**

## 1. select

   SQL: use  `SELECT * FROM tab`
   
   PANDAS: use `df['col1', 'col2']`
   
## 2. filter

   SQL: use `WHERE`
   
   PANDAS: use `df[df['col']> value]`


## 3. order

   SQL: use `ORDER BY`
   
   PANDAS: use `df.sort_values(by = 'col')`

## 4. group

   SQL: use `GROUP BY`
   
   PANDAS: use `df.groupby('col')`, additionally could be `df.groupby('col').agg`

## 5. functions

   SQL: use `GROUP BY` plus `SUM/AVG`
   
   PANDAS: use `groupby()` or `agg()` functions

## 6. join tables

   SQL: use `JOIN`
   
   PANDAS: use `merge()`
   

## 6. update/delete

   SQL: use `UPDATE` or `DELETE`
   
   PANDAS: use `drop` functions

   - pandas modify single value `df.at[row_index, 'col'] = new_value`

   - pandas modify multiple values `df.loc[df['col'] == condition, 'column_to_update'] = new_value`
   
   - pandas dropping rows `df.drop(index_labels, inplace=True)`
   
   - pandas dropping columns `df.drop(columns=['col1', 'col2'], inplace=True)`
   
# **Table Summary**


| Command | SQL | Python |
| --- | --- | --- |
| select all columns | `SELECT * FROM tab;` | `df` |
| select specific columns| `SELECT col1, col2 FROM tab;` | `df['col1', 'col2']`|
| adding new calculated column| `SELECT col1, col2, col1/col2 as new_col FROM tab;` | `df.assign(new_col = df['col1']/df['col2']` )` |
| order columns in ASC| `SELECT * FROM tab ORDER BY col1 ASC;` | `df.sort_values(by = 'col1, ascending=True')` |
| order columns in DESC| `SELECT * FROM tab ORDER BY col1 DESC;` | `df.sort_values(by = 'col1', assending=False)` |
| filter by one column| `SELECT * FROM tab WHERE co1 = 11;` | `df[df['col1'] == 11]` |
| filter using AND| `SELECT * FROM tab WHERE col1 = 11 AND col2 > 5;` | `df[df['col1'] == 11] & df[df['col2'] > 5]` |
| filter using OR | `SELECT * FROM tab WHERE col1 = 11 OR col2 > 5;` | `result = df[(df['col1'] == 11) \| (df['col2'] > 5)]` |
| filter NULL| `SELECT * FROM tab WHERE col2 IS NULL;` | `df[df['col2'].isna()]` |
| filter values NOT NULL| `SELECT * FROM tab WHERE col1 IS NOT NULL;` | `df[df['col1'].notna()]`|
| filter by use query| `SELECT * FROM tab WHERE co1 = 4;` | `df.query('col1 == 4')]` |
| compare 2 columns| `SELECT * FROM tab WHERE col1 > col2;` | `df[df['col1'] > df['col2']]` |
| find records include values| `WHERE col1 LIKE '%i%'` | `df[df['col1'].str.contains('i', case=False, regex=False, na=False)]` |
| find records include multiple values| `WHERE col1 LIKE '%i%' OR col1 LIKE '%sh%'` | `df[df['col1'].str.contains('i\|sh', case=False, regex=True, na=False)]` |
| find records starts with values| `WHERE col1 LIKE 'h%'` | `df[df['col1'].str.startswith('h', na=False)]` |
| find records ends with values| `WHERE col1 LIKE '%k'` | `df[df['col1'].str.endswith('k', na=False)]` |
| find records in certain values| `WHERE col1 IN (1,2,3)` | `result = df[df['col1'].isin([1, 2, 3])]` |
| find records in certain range| `WHERE col1 BETWEEN 1 AND 5` | `result = df[(df['col1'] >= 1) & (df['col1'] <= 5)]` |
| limit first N rows| `SELECT * FROM tab LIMIT 10` | `df.head(10)` |
| limit last N rows| `SELECT * FROM tab ORDER BY id DESC LIMIT 10` | `df.tail(10)` |
| function - offset| `SELECT * FROM tab ORDER BY col1 DESC LIMIT 2 OFFSET 5` | `result = df.sort_values('col1', ascending=False).iloc[5:7]` |
| function - count| `SELECT col1, count(*) FROM tab GROUP BY col1` | `` |
| function - AVG| `SELECT col1, AVG(col2) FROM tab GROUP BY col1` | `` |
| function - HAVING| `SELECT col1, AVG(col2) FROM tab GROUP BY col1 HAVING COUNT(*)>10` | `` |
