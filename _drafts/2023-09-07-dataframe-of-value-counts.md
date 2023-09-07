---
title: Pandas DataFrame of value_counts() for data exploration.
categories: [Snippets, Code]
tags: [python, pandas, dataframe]
date: 2023-09-07 15:05:00 +0530
---


## Code
```python
def value_counts_df(
        data: pd.DataFrame,
        cols: list
)-> pd.DataFrame:
    """
    # Create a Dataframe of column value_counts().
    # Helps review data distributions.
    :param data: DataFrame of data.
    :param cols: List of categorical columns exempt all date columns.
    :return: The value_count() DataFrame.
    """
    df = pd.DataFrame()
    for col in cols:
        val = data[col].value_counts()
        ser = pd.Series(dtype='object')

        for index, rows in val.iteritems():
            ser = pd.concat(
                [
                    ser,
                    pd.Series(f'{index} - {rows}')
                ]
            )
            ser = ser.reset_index(drop=True)

        df = pd.concat(
            [df, ser],
            axis=1
        )
    df.columns = cols
    return df
```

> This goes against [tidyverse rules](https://byuidatascience.github.io/python4ds/tidy-data.html#fig:tidy-structure)
... oops 🤭.  
But it's fine since we're using the DataFrame only for a visual review 
of the data distribution.
{: .prompt-warning}

## Output

|  | hotel | is\_canceled | meal | country | market\_segment | distribution\_channel | reserved\_room\_type | assigned\_room\_type | deposit\_type | agent | company | customer\_type | reservation\_status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | City Hotel - 79330 | 0 - 75166 | BB - 92310 | PRT - 48590 | Online TA - 56477 | TA/TO - 97870 | A - 85994 | A - 74053 | No Deposit - 104641 | 9.0 - 31961 | 40.0 - 927 | Transient - 89613 | Check-Out - 75166 |
| 1 | Resort Hotel - 40060 | 1 - 44224 | HB - 14463 | GBR - 12129 | Offline TA/TO - 24219 | Direct - 14645 | D - 19201 | D - 25322 | Non Refund - 14587 | 240.0 - 13922 | 223.0 - 784 | Transient-Party - 25124 | Canceled - 43017 |
| 2 | NaN | NaN | SC - 10650 | FRA - 10415 | Groups - 19811 | Corporate - 6677 | E - 6535 | E - 7806 | Refundable - 162 | 1.0 - 7191 | 67.0 - 267 | Contract - 4076 | No-Show - 1207 |
| 3 | NaN | NaN | Undefined - 1169 | ESP - 8568 | Direct - 12606 | GDS - 193 | F - 2897 | F - 3751 | NaN | 14.0 - 3640 | 45.0 - 250 | Group - 577 | NaN |
| 4 | NaN | NaN | FB - 798 | DEU - 7287 | Corporate - 5295 | Undefined - 5 | G - 2094 | G - 2553 | NaN | 7.0 - 3539 | 153.0 - 215 | NaN | NaN |
| 5 | NaN | NaN | NaN | ITA - 3766 | Complementary - 743 | NaN | B - 1118 | C - 2375 | NaN | 6.0 - 3290 | 174.0 - 149 | NaN | NaN |
| 6 | NaN | NaN | NaN | IRL - 3375 | Aviation - 237 | NaN | C - 932 | B - 2163 | NaN | 250.0 - 2870 | 219.0 - 141 | NaN | NaN |
| 7 | NaN | NaN | NaN | BEL - 2342 | Undefined - 2 | NaN | H - 601 | H - 712 | NaN | 241.0 - 1721 | 281.0 - 138 | NaN | NaN |
| 8 | NaN | NaN | NaN | BRA - 2224 | NaN | NaN | P - 12 | I - 363 | NaN | 28.0 - 1666 | 154.0 - 133 | NaN | NaN |
| 9 | NaN | NaN | NaN | NLD - 2104 | NaN | NaN | L - 6 | K - 279 | NaN | 8.0 - 1514 | 405.0 - 119 | NaN | NaN |
| 10 | NaN | NaN | NaN | USA - 2097 | NaN | NaN | NaN | P - 12 | NaN | 3.0 - 1336 | 233.0 - 114 | NaN | NaN |

