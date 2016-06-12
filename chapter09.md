<!-- README.md is generated from README.Rmd. -->
split-apply-combine
===================

GroupBy Mechanics
-----------------

-   Each grouping key can take many forms, and the keys do not have to be all of the same type:

    -   A list or array of values that is the same length as the axis being grouped

    -   A value indicating a column name in a DataFrame

    -   A dict or Series giving a correspondence between the values on the axis being grouped and the group names

    -   A function to be invoked on the axis index or the individual labels in the index

    -   The latter three methods are all just shortcuts for producing an array of values to be used to split up the object.

<!-- -->

    import numpy as np
    import pandas as pd
    from pandas import Series, DataFrame

    df = DataFrame({'key1' : ['a', 'a', 'b', 'b', 'a'],
                    'key2' : ['c', 'd', 'c', 'd', 'c'],
                    'data1' : np.random.randn(5),
                    'data2' : np.random.randn(5)})
                    
    grouped = df['data1'].groupby(df['key1'])
    grouped.mean()

    s1 = np.array(['NJ', 'WA', 'WA', 'NJ', 'NJ'])
    s2 = np.array([2015, 2015, 2016, 2015, 2016])
    df['data1'].groupby([s1, s2]).mean()

    means = df['data1'].groupby([df['key1'], df['key2']]).mean()
    means.unstack()

    df.groupby('key1').mean()
    df.groupby(['key1', 'key2']).mean()

    df.groupby(['key1', 'key2']).size()

-   Iterating Over Groups

The GroupBy object supports iteration, generating a sequence of 2-tuples containing the group name along with the chunk of data.

    ## iterate over key and group
    for name, group in df.groupby('key1'):
      print name
      print group
      
    ## multiple keys: first element in the tuple will be a tuple of key values
    for (k1, k2), group in df.groupby(['key1', 'key2']):
      print k1, k2
      print group

    ## a recipe of computing a dict of the data pieces as a one-liner
    pieces = dict(list(df.groupby('key1')))
    pieces['b']

    ## groupby groups on axis=0 by default, yet can group on any other axes
    grouped = df.groupby(df.dtypes, axis=1)
    dict(list(grouped))

-   Selecting a Column or Subset of Columns

Indexing a GroupBy object created from a DataFrame with a column name or array of column names has the effect of selecting those columns for aggregation.

    df.groupby('key1')['data1']
    df.groupby('key1')[['data2']]

    ## syntactic sugar as
    df['data1'].groupby(df['key1'])
    df[['data2']].groupby(df['key1'])

-   Grouping with Dicts and Series

<!-- -->

    people = DataFrame(np.random.randn(5, 5), columns=['a', 'b', 'c', 'd', 'e'], 
                       index=['Jobs', 'Steve', 'Wes', 'Jim', 'Travis'])
                       
    people.ix[2:3, ['b', 'c']] = np.nan

    mapping = {'a': 'red', 'b': 'red', 'c': 'blue', 'd': 'blue', 'e': 'red', 'f' : 'orange'}
    people.groupby(mapping, axis=1).sum()

    map_series = Series(mapping)
    people.groupby(map_series, axis=1).count()

-   Grouping with Functions

<!-- -->

    people.groupby(len).sum()

    ## mixing functions with arrays, dicts, or Series is not a problem as everything gets converted to arrays internally:
    key_list = ['one', 'one', 'one', 'two', 'two']
    people.groupby([len, key_list]).min()

-   Grouping by Index Levels

Hierarchically-indexed data sets can be aggregated using one of the levels of an axis index by passing the level number or name using the level keyword.

    columns = pd.MultiIndex.from_arrays([['US', 'US', 'US', 'JP', 'JP'], [1, 3, 5, 1, 3]], names=['cty', 'tenor'])
    hier_df = DataFrame(np.random.randn(4, 5), columns=columns)
    hier_df.groupby(level='cty', axis=1).count()
    hier_df.groupby(level='tenor', axis=1).count()

Data Aggregation
----------------

-   Optimized groupby methods

| Function    | Description                                                  |
|-------------|--------------------------------------------------------------|
| count       | Number of non-NA values in the group                         |
| sum         | Sum of non-NA values                                         |
| mean        | Mean of non-NA values                                        |
| median      | Arithmetic median of non-NA values                           |
| std, var    | Unbiased (n - 1 denominator) standard deviation and variance |
| min, max    | Minimum and maximum of non-NA values                         |
| prod        | Product of non-NA values                                     |
| first, last | First and last non-NA values                                 |

-   Other aggregation functions can be used by passing to to the `aggregate` or `agg` method

<!-- -->

    def peak_to_peak(arr):
      return arr.max() - arr.min()

    grouped.agg(peak_to_peak)

Group-wise Operations and Transformations
-----------------------------------------

-   `transform` applies a function to each group, and then places the results in the appropriate locations. If each group produces a scalar value, it will be propagated (broadcasted).

    -   Like aggregate, transform is a more specialized function having rigid requirements: the passed function must either produce a scalar value to be broadcasted (like np.mean) or a transformed array of the same size.
-   `apply` is the most general purpose GroupBy method:

    -   *`apply` splits the object being manipulated into pieces, invokes the passed function on each piece, and then attempts to concatenate the pieces together (split-apply-combine)*.

Pivot Tables and Cross-Tabulation
---------------------------------

-   DataFrame has a `pivot_table` method, as well as a top-level `pandas.pivot_table` function. It provides a convenience interface to `groupby`, and also can add partial totals, also known as margins.

-   `pivot_table` options

<table style="width:29%;">
<colgroup>
<col width="12%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Argument</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">values</td>
<td align="left">Column name or names to aggregate. By default aggregates all numeric columns</td>
</tr>
<tr class="even">
<td align="left">rows</td>
<td align="left">Column names or other group keys to group on the rows of the resulting pivot table</td>
</tr>
<tr class="odd">
<td align="left">cols</td>
<td align="left">Column names or other group keys to group on the columns of the resulting pivot table</td>
</tr>
<tr class="even">
<td align="left">aggfunc</td>
<td align="left">Aggregation function or list of functions; 'mean' by default. Can be any function valid in a groupby context</td>
</tr>
<tr class="odd">
<td align="left">fill_value</td>
<td align="left">Replace missing values in result table</td>
</tr>
<tr class="even">
<td align="left">margins</td>
<td align="left">Add row/column subtotals and grand total, False by default</td>
</tr>
</tbody>
</table>

-   The `pandas.crosstab` function is a special case of `pandas.pivot_table` that computes group frequencies.

-   Trick: `dict.get(x, x)` allows `x` with no mapping to "pass through" - if dict contains {'x' : 'y'} then get 'y' else 'x'.
