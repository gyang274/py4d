<!-- README.md is generated from README.Rmd. -->
pandas
======

Series and DataFrame
--------------------

-   `Series` is like a `dict`, and DataFrame is like a nested `dict` of `dicts with common keys`.

<!-- -->

    import pandas as pd
    from pandas import Series, DataFrame

    sdata1 = {'Ohio': 2, 'Texas': 3, 'Nevada': 5, 'Utah': 8}
    series1 = Series(sdata1)

    fdata1 = {'Nevada': {           2001: 2.2, 2002: 2.3},
              'Ohio'  : {2000: 1.4, 2001: 1.7, 2002: 3.8}}
           
    frame1 = DataFrame(fdata1)

-   Possible data inputs to DataFrame constructor

<table style="width:15%;">
<colgroup>
<col width="6%" />
<col width="8%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Type</th>
<th align="left">Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">2D ndarray</td>
<td align="left">A matrix of data, passing optional row and column labels</td>
</tr>
<tr class="even">
<td align="left">dict of arrays, lists, or tuples</td>
<td align="left">Each sequence becomes a column in the DataFrame. All sequences must be the same length.</td>
</tr>
<tr class="odd">
<td align="left">NumPy structured/record array</td>
<td align="left">Treated as the &quot;dict of arrays&quot; case</td>
</tr>
<tr class="even">
<td align="left">dict of Series</td>
<td align="left">Each value becomes a column. Indexes from each Series are unioned together to form the result's row index if no explicit index is passed.</td>
</tr>
<tr class="odd">
<td align="left">dict of dicts</td>
<td align="left">Each inner dict becomes a column. Keys are unioned to form the row index as in the &quot;dict of Series&quot; case.</td>
</tr>
<tr class="even">
<td align="left">list of dicts or Series</td>
<td align="left">Each item becomes a row in the DataFrame. Union of dict keys or Series indexes become the DataFrame's column labels</td>
</tr>
<tr class="odd">
<td align="left">list of lists or tuples</td>
<td align="left">Treated as the &quot;2D ndarray&quot; case</td>
</tr>
<tr class="even">
<td align="left">another DataFrame</td>
<td align="left">The DataFrame's indexes are used unless different ones are passed</td>
</tr>
<tr class="odd">
<td align="left">NumPy MaskedArray</td>
<td align="left">Like the &quot;2D ndarray&quot; case except masked values become NA/missing in the DataFrame result</td>
</tr>
</tbody>
</table>

Index Objects
-------------

-   pandas's Index objects are responsible for holding the axis labels and other metadata (like the axis name or names).

-   Index objects are immutable and thus can't be modified by the user. Immutability is important so that Index objects can be safely shared among data structures.

-   Main Index objects in `pandas`

<table style="width:25%;">
<colgroup>
<col width="8%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Class</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Index</td>
<td align="left">The most general Index object, representing axis labels in a NumPy array of Python objects.</td>
</tr>
<tr class="even">
<td align="left">Int64Index</td>
<td align="left">Specialized Index for integer values.</td>
</tr>
<tr class="odd">
<td align="left">MultiIndex</td>
<td align="left">&quot;Hierarchical&quot; index object representing multiple levels of indexing on a single axis. Can be thought of as similar to an array of tuples.</td>
</tr>
<tr class="even">
<td align="left">DatetimeIndex</td>
<td align="left">Stores nanosecond timestamps (represented using NumPy’s datetime64 dtype).</td>
</tr>
<tr class="odd">
<td align="left">PeriodIndex</td>
<td align="left">Specialized Index for Period data (timespans).</td>
</tr>
</tbody>
</table>

-   Index methods and properties

<table style="width:26%;">
<colgroup>
<col width="9%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Method</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">append</td>
<td align="left">Concatenate with additional Index objects, producing a new Index</td>
</tr>
<tr class="even">
<td align="left">diff</td>
<td align="left">Compute set difference as an Index</td>
</tr>
<tr class="odd">
<td align="left">intersection</td>
<td align="left">Compute set intersection</td>
</tr>
<tr class="even">
<td align="left">union</td>
<td align="left">Compute set union</td>
</tr>
<tr class="odd">
<td align="left">isin</td>
<td align="left">Compute boolean array indicating whether each value is contained in the passed collection</td>
</tr>
<tr class="even">
<td align="left">delete</td>
<td align="left">Compute new Index with element at index i deleted</td>
</tr>
<tr class="odd">
<td align="left">drop</td>
<td align="left">Compute new index by deleting passed values</td>
</tr>
<tr class="even">
<td align="left">insert</td>
<td align="left">Compute new Index by inserting element at index i</td>
</tr>
<tr class="odd">
<td align="left">is_monotonic</td>
<td align="left">Returns True if each element is greater than or equal to the previous element</td>
</tr>
<tr class="even">
<td align="left">is_unique</td>
<td align="left">Returns True if the Index has no duplicate values</td>
</tr>
<tr class="odd">
<td align="left">unique</td>
<td align="left">Compute the array of unique values in the Index</td>
</tr>
</tbody>
</table>

Essential Functionally
----------------------

-   Reindexing

    -   reindexing can be done more succinctly by label-indexing with `ix`.

    -   `reindex` function arguments

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
        <td align="left">index</td>
        <td align="left">New sequence to use as index. Can be Index instance or any other sequence-like Python data structure. An Index will be used exactly as is without any copying</td>
        </tr>
        <tr class="even">
        <td align="left">method</td>
        <td align="left">Interpolation (fill) method, <code>ffill</code> or <code>pad</code> to fill (or carry) values forward, <code>bfill</code> or <code>backfill</code> to fill (or carry) values backward.</td>
        </tr>
        <tr class="odd">
        <td align="left">fill_value</td>
        <td align="left">Substitute value to use when introducing missing data by reindexing</td>
        </tr>
        <tr class="even">
        <td align="left">limit</td>
        <td align="left">When forward- or backfilling, maximum size gap to fill</td>
        </tr>
        <tr class="odd">
        <td align="left">level</td>
        <td align="left">Match simple Index on level of MultiIndex, otherwise select subset of copy Do not copy underlying data if new index is equivalent to old index. True by default (i.e. always copy data).</td>
        </tr>
        </tbody>
        </table>

-   Dropping entries from an axis

    -   `data.drop([index])` is default on dropping row index, dropping column index must specifiy `axis=1`. This is inconsistent with latter indexing, selection and filtering, which is default on indexing and slicing column index, and selecting row index must specifiy `.ix`.

<!-- -->

    data.drop(['row-index'])

    data.drop(['col-index'], axis=1)

-   Indexing, selection, and filtering

<!-- -->

    data['col-index']

    data.ix['row-index'<, 'col-index'>]

    - Indexing options with DataFrame

<table style="width:15%;">
<colgroup>
<col width="6%" />
<col width="8%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Type</th>
<th align="left">Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">obj[val]</td>
<td align="left">Select single column or sequence of columns from the DataFrame. Special case conveniences: boolean array (filter rows), slice (slice rows), or boolean DataFrame (set values based on some criterion).</td>
</tr>
<tr class="even">
<td align="left">obj.ix[val]</td>
<td align="left">Selects single row of subset of rows from the DataFrame.</td>
</tr>
<tr class="odd">
<td align="left">obj.ix[:, val]</td>
<td align="left">Selects single column of subset of columns.</td>
</tr>
<tr class="even">
<td align="left">obj.ix[val1, val2]</td>
<td align="left">Select both rows and columns.</td>
</tr>
<tr class="odd">
<td align="left">reindex method</td>
<td align="left">Conform one or more axes to new indexes.</td>
</tr>
<tr class="even">
<td align="left">xs method</td>
<td align="left">Select single row or column as a Series by label.</td>
</tr>
<tr class="odd">
<td align="left">icol, irow methods</td>
<td align="left">Select single column or row, respectively, as a Series by integer location.</td>
</tr>
<tr class="even">
<td align="left">get_value, set_value methods</td>
<td align="left">Select single value by row and column label.</td>
</tr>
</tbody>
</table>

Arithmetic and data alignment
-----------------------------

-   Arithmetic such as `+ - * /` between Series and DataFrame will match index, and `NaN` is produced when nomatch.

-   Arithmetic methods suchs as `add sub mul div` with argument `fill_value=0` will fill a special value, like 0, when an axis label is found in one object but not the other.

-   Operations between DataFrame and Series: By default, arithmetic between DataFrame and Series matches the index of the Series on the DataFrame's columns, broadcasting down the rows, e.g., row-by-row operation. If one want to instead matching on the rows, broadcast over the columns, e.g., col-by-col operation, one have to use one of the arithmetic methods with argument `axis=0`. The axis number that you pass is the axis to match on. In this case we mean to match on the DataFrame’s row index and broadcast across.

<!-- -->

    #- Operations between DataFrame and Series
    frame = DataFrame(np.arange(12.).reshape((4, 3)), columns=list('bde'), index=['Ohio', 'Texas', 'Nevada', 'Utah'])

    ## row-by-row operation
    series1 = frame.ix[0]
    frame - series1

    ## reindex form union when index not match
    series2 = Series(range(3), index=['b', 'e', 'f'])
    frame + series2

    ## col-by-col operation with methods and argument axis
    series3 = frame['d']
    frame.sub(series3, axis=0)

-   Function application and mapping:

    -   NumPy ufuncs (element-wise array methods) work fine with pandas objects.

    -   DataFrame's `apply` method applys a function on 1D arrays to each column (default `axis=0`) or row (`axis=1`).

    -   DataFrame's `applymap` method and Series `map` method apply a function element-wise on a DataFrame or Series.

-   Sorting and ranking:

    -   The `sort_index` method sorts DataFrame or Series lexicographically by row (default `axis=0`) or column (`axis=1`) index, and returns a new, sorted object.

    -   The `order` method sorts a Series by its values.

    -   The `sort_index` method with argument `by=[col-index]` sorts a DataFrame w.r.t one or more columns.

    -   The `rank` methods for Series and DataFrame assigns ranks from one through the number of valid data points in an array. By default rank breaks ties by assigning each group the mean rank. Tie-breaking methods with `rank`: `average` (default) assign the average rank to each entry in the equal group, `min` use the minimum rank for the whole group, `max` use the maximum rank for the whole group, `first` assign ranks in the order the values appear in the data. Ranking is closely related to sorting, it is similar to the indirect sort indices produced by `numpy.argsort`, except that ties are broken according to a rule.

Summarizing and Computing Descriptive Statistics
------------------------------------------------

-   Descriptive and summary statistics

<table style="width:26%;">
<colgroup>
<col width="9%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Method</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">count</td>
<td align="left">Number of non-NA values</td>
</tr>
<tr class="even">
<td align="left">describe</td>
<td align="left">Compute set of summary statistics for Series or each DataFrame column</td>
</tr>
<tr class="odd">
<td align="left">min, max</td>
<td align="left">Compute minimum and maximum values</td>
</tr>
<tr class="even">
<td align="left">argmin, argmax</td>
<td align="left">Compute index locations (integers) at which minimum or maximum value obtained, respectively</td>
</tr>
<tr class="odd">
<td align="left">idxmin, idxmax</td>
<td align="left">Compute index values at which minimum or maximum value obtained, respectively</td>
</tr>
<tr class="even">
<td align="left">quantile</td>
<td align="left">Compute sample quantile ranging from 0 to 1</td>
</tr>
<tr class="odd">
<td align="left">sum</td>
<td align="left">Sum of values</td>
</tr>
<tr class="even">
<td align="left">mean</td>
<td align="left">Mean of values</td>
</tr>
<tr class="odd">
<td align="left">median</td>
<td align="left">Arithmetic median (50% quantile) of values</td>
</tr>
<tr class="even">
<td align="left">mad</td>
<td align="left">Mean absolute deviation from mean value</td>
</tr>
<tr class="odd">
<td align="left">var</td>
<td align="left">Sample variance of values</td>
</tr>
<tr class="even">
<td align="left">std</td>
<td align="left">Sample standard deviation of values</td>
</tr>
<tr class="odd">
<td align="left">skew</td>
<td align="left">Sample skewness (3rd moment) of values</td>
</tr>
<tr class="even">
<td align="left">kurt</td>
<td align="left">Sample kurtosis (4th moment) of values</td>
</tr>
<tr class="odd">
<td align="left">cumsum</td>
<td align="left">Cumulative sum of values</td>
</tr>
<tr class="even">
<td align="left">cummin, cummax</td>
<td align="left">Cumulative minimum or maximum of values, respectively</td>
</tr>
<tr class="odd">
<td align="left">cumprod</td>
<td align="left">Cumulative product of values</td>
</tr>
<tr class="even">
<td align="left">diff</td>
<td align="left">Compute 1st arithmetic difference (useful for time series)</td>
</tr>
<tr class="odd">
<td align="left">pct_change</td>
<td align="left">Compute percent changes</td>
</tr>
</tbody>
</table>

-   Options for reduction methods, like `sum`

<table style="width:26%;">
<colgroup>
<col width="9%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Method</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">axis</td>
<td align="left">Axis to reduce over. 0 for DataFrame’s rows and 1 for columns.</td>
</tr>
<tr class="even">
<td align="left">skipna</td>
<td align="left">Exclude missing values, True by default.</td>
</tr>
<tr class="odd">
<td align="left">level</td>
<td align="left">Reduce grouped by level if the axis is hierarchically-indexed (MultiIndex).</td>
</tr>
</tbody>
</table>

Correlation and Covariance
--------------------------

-   The `corr` method of Series computes the correlation of the overlapping, non-NA, aligned-by-index values in two Series. Relatedly, `cov` computes the covariance.

-   DataFrame's `corrwith` method computes pairwise correlations between a DataFrame's columns or rows with another Series or DataFrame.

    -   Passing a Series returns a Series with the correlation value computed for each column.

    -   Passing a DataFrame computes the correlations of matching column names.

    -   Passing axis=1 does things row-wise instead.

    -   In all cases, the data points are aligned by label before computing the correlation.

Unique Values, Value Counts, and Membership
-------------------------------------------

-   Unique, value counts, and binning methods

<table style="width:26%;">
<colgroup>
<col width="9%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Method</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">isin</td>
<td align="left">Compute boolean array indicating whether each Series value is contained in the passed sequence of values.</td>
</tr>
<tr class="even">
<td align="left">unique</td>
<td align="left">Compute array of unique values in a Series, returned in the order observed.</td>
</tr>
<tr class="odd">
<td align="left">value_counts</td>
<td align="left">Return a Series containing unique values as its index and frequencies as its values, ordered count in descending order.</td>
</tr>
</tbody>
</table>

-   `value_counts` like `R table()`, and also available as a top-level pandas method that can be used with any array or sequence.

-   Ex: use `pandas.value_counts()` to compute a histogram on multiple related columns in a DataFrame:

<!-- -->

    data = DataFrame({'Qu1': [1, 3, 4, 3, 4], 'Qu2': [2, 3, 1, 2, 3], 'Qu3': [1, 5, 2, 4, 4]})
    rslt = data.apply(pd.value_counts).fillna(0)

Handling Missing Data
---------------------

-   `pandas` uses the floating point value `NaN` (Not a Number) to represent missing data in both floating as well as in non-floating point arrays like string data. It is just used as a *sentinel* that can be easily detecte. Both `np.nan` and built-in `None` are treated as `NA` or `NaN` in `pandas`.

-   NA handling methods

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
<td align="left">dropna</td>
<td align="left">Filter axis labels based on whether values for each label have missing data, with varying thresholds for how much missing data to tolerate.</td>
</tr>
<tr class="even">
<td align="left">fillna</td>
<td align="left">Fill in missing data with some value or using an interpolation method such as 'ffill' or 'bfill'.</td>
</tr>
<tr class="odd">
<td align="left">isnull</td>
<td align="left">Return like-type object containing boolean values indicating which values are missing / NA.</td>
</tr>
<tr class="even">
<td align="left">notnull</td>
<td align="left">Negation of isnull.</td>
</tr>
</tbody>
</table>

-   `dropna`:

    -   Use `dropna` on a Series returns the Series with only the non-null data and index values.

    -   Use `dropna` on a DataFrame returns rows containing no missing value (default is to drop any row containing a missing value), passing `how='all'` will returns rows containing not all missing value (drop rows that are all NA). Dropping columns in the same way is only a matter of passing `axis=1`.

-   `fillna`:

    -   Calling `fillna` with a constant replaces missing values with that value.

    -   Calling `fillna` with a dict you can use a different fill value for each column.

    -   Passing `inplace=True` can modify the existing object in place, default is returning a new object.

    -   `fillna` function arguments

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
    <td align="left">value</td>
    <td align="left">Scalar value or dict-like object to use to fill missing values</td>
    </tr>
    <tr class="even">
    <td align="left">method</td>
    <td align="left">Interpolation, by default 'ffill' if function called with no other arguments</td>
    </tr>
    <tr class="odd">
    <td align="left">axis</td>
    <td align="left">Axis to fill on, default axis=0</td>
    </tr>
    <tr class="even">
    <td align="left">inplace</td>
    <td align="left">Modify the calling object without producing a copy</td>
    </tr>
    <tr class="odd">
    <td align="left">limit</td>
    <td align="left">For forward and backward filling, maximum number of consecutive periods to fill</td>
    </tr>
    </tbody>
    </table>

Hierarchical Indexing
---------------------

-   Hierarchical indexing in `pandas` enables multiple (two or more) index levels on an axis. Somewhat abstractly, it provides a way to work with higher dimensional data in a lower dimensional form. In the most simply case, two index levels, think the outer level index as row index, whereas inner level index as column index.

    -   The `stack` and `unstack` convert back and forth between MultiIndex and row-column-index.
-   Reordering and sorting levels:

    -   The `swaplevel` takes two level numbers or names and returns a new object with the levels interchanged (but the data is otherwise unaltered).

    -   The `sortlevel` sorts the data (stably) using only the index values (not data values) in a single level.

    -   Data selection performance is much better on hierarchically indexed objects if the index is lexicographically sorted starting with the outermost level, that is, the result of calling `sortlevel(0)` or `sort_index()`.

Using a DataFrame’s Columns as Index and Vice Versa
---------------------------------------------------

-   DataFrame's `set_index` function will create a new DataFrame using one or more of its columns as the index `frame2 = frame.set_index(['col1', 'col2'])`.

-   The columns used in `set_index` are removed from the DataFrame by default, though you can leave them in by passing `drop=False`.

-   `reset_index`, on the other hand, does the opposite of `set_index`, the hierarchical index levels are are moved into the columns.

Integer Indexing
----------------

-   `pandas` would fallback on integer indexing when user specified. However, it is ambiguous when Series or DataFrame also have a integer labelled index.

-   To keep things consistent, if you have an axis index containing indexers, data selection with integers will always be label-oriented. This includes slicing with ix, too.

-   In cases where reliable position-based indexing is needed regardless of the index type, use the `iget_value` method from Series and `irow` and `icol` methods from DataFrame.

Panel Data
----------

-   `pandas` design panel data as a three-dimensional analogue of DataFrame.

-   To create a Panel, use a dict of DataFrame objects or a three-dimensional ndarray - `item x major x minor`. Each item (the analogue of columns in a DataFrame) in the Panel is a DataFrame, and `ix`-based label indexing generalizes to three dimensions.

-   An alternate way to represent panel data, especially for fitting statistical models, is in "stacked" DataFrame form `paneldata.to_frame()` - stacked DataFrame data with `item as column index, major x minor as row index`, and the inverse is `stackedframedata.to_panel()`.
