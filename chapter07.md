<!-- README.md is generated from README.Rmd. -->
data wrangling
==============

Combining and Merging Data Sets
-------------------------------

-   `pandas.merge` connects rows in DataFrames based on one or more keys. It implements database `join` operations.

    -   `pd.merge(df1, df2, on=['key' or 'keys'])` default is on all overlapping column names as the keys.

    -   `pd.merge(df3, df4, left_on='lkey', right_on='rkey')` when column names are different in each object.

    -   `pd.merge` does an 'inner' join by default, passing `how=<'left'|'right'|'outer'>` options for 'left', 'right', and 'outer' join.

    -   `pd.merge` has a `suffixes` option for specifying strings to append to overlapping names in the left and right DataFrame objects.

-   `pandas.merge` function arguments

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
<td align="left">left</td>
<td align="left">DataFrame to be merged on the left side</td>
</tr>
<tr class="even">
<td align="left">right</td>
<td align="left">DataFrame to be merged on the right side</td>
</tr>
<tr class="odd">
<td align="left">how</td>
<td align="left">One of 'inner', 'outer', 'left' or 'right'. 'inner' by default</td>
</tr>
<tr class="even">
<td align="left">on</td>
<td align="left">Column names to join on. Must be found in both DataFrame objects. If not specified and no other join keys given, will use the intersection of the column names in left and right as the join keys</td>
</tr>
<tr class="odd">
<td align="left">left_on</td>
<td align="left">Columns in left DataFrame to use as join keys</td>
</tr>
<tr class="even">
<td align="left">right_on</td>
<td align="left">Analogous to left_on for left DataFrame</td>
</tr>
<tr class="odd">
<td align="left">left_index</td>
<td align="left">Use row index in left as its join key (or keys, if a MultiIndex)</td>
</tr>
<tr class="even">
<td align="left">right_index</td>
<td align="left">Analogous to left_index</td>
</tr>
<tr class="odd">
<td align="left">sort</td>
<td align="left">Sort merged data lexicographically by join keys; True by default. <em>Disable to get better performance in some cases on large datasets</em></td>
</tr>
<tr class="even">
<td align="left">suffixes</td>
<td align="left">Tuple of string values to append to column names in case of overlap; defaults to ('_x', '_y'). For example, if 'data' in both DataFrame objects, would appear as 'data_x' and 'data_y' in result</td>
</tr>
<tr class="odd">
<td align="left">copy</td>
<td align="left">If False, avoid copying data into resulting data structure in some exceptional cases. By default always copies</td>
</tr>
</tbody>
</table>

Concatenating Along an Axis
---------------------------

-   `numpy.concatenate`.

-   `pandas.concat`: `pd.concat([s1, s2, s3], axis=1)` default is along `axis=0`.

-   `pandas.concat` function arguments

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
<td align="left">objs</td>
<td align="left">List or dict of pandas objects to be concatenated. The only required argument</td>
</tr>
<tr class="even">
<td align="left">axis</td>
<td align="left">Axis to concatenate along; defaults to 0</td>
</tr>
<tr class="odd">
<td align="left">join</td>
<td align="left">One of 'inner', 'outer', defaulting to 'outer'; whether to intersection (inner) or union (outer) together indexes along the other axes</td>
</tr>
<tr class="even">
<td align="left">join_axes</td>
<td align="left">Specific indexes to use for the other n-1 axes instead of performing union/intersection logic</td>
</tr>
<tr class="odd">
<td align="left">keys</td>
<td align="left">Values to associate with objects being concatenated, forming a hierarchical index along the concatenation axis. Can either be a list or array of arbitrary values, an array of tuples, or a list of arrays (if multiple level arrays passed in levels)</td>
</tr>
<tr class="even">
<td align="left">levels</td>
<td align="left">Specific indexes to use as hierarchical index level or levels if keys passed</td>
</tr>
<tr class="odd">
<td align="left">names</td>
<td align="left">Names for created hierarchical levels if keys and / or levels passed</td>
</tr>
<tr class="even">
<td align="left">verify_integrity</td>
<td align="left">Check new axis in concatenated object for duplicates and raise exception if so. By default (False) allows duplicates</td>
</tr>
<tr class="odd">
<td align="left">ignore_index</td>
<td align="left">Do not preserve indexes <em>along concatenation axis</em>, instead producing a new range(total_length) index</td>
</tr>
</tbody>
</table>

Combining Data with Overlap
---------------------------

-   `combine_first` on Series `a.combine_first(b)` is like `np.where(pd.isnull(a), b, a)`.

-   `combine_first` on DataFrames does the same thing column by column, think it as "patching" missing data in the calling object with data from the object passed.

Reshaping and Pivoting
----------------------

-   Reshaping with Hierarchical Indexing:

    -   `stack`: rotates or pivots from the columns in the data to the rows. Stacking filters out missing data by default, yet can keep it by passing `dropna=False`.

    -   `unstack`: pivots from the rows into the columns. The innermost level is unstacked (same with stack) by default, yet can unstack a different level by passing a level number or name.

-   Pivoting "long" to "wide" Format

    -   `pivot`: convert long format data into wide format: `ldata.pivot('row-index', 'col-index', ['val-index'])`, val-index is optional, without it multiple values will be filled in as outer column index.

    -   `pivot` is just a shortcut for creating a hierarchical index using `set_index` and reshaping with `unstack`: `ldata.pivot('row-index', 'col-index')` is equivalent to `ldata.set_index(['row-index', 'col-index']).unstack('col-index')`.

Data Transformation
-------------------

-   Removing Duplicates

    -   The DataFrame method `duplicated` returns a boolean Series indicating whether each row is a duplicate or not.

    -   Relatedly, `drop_duplicates` returns a DataFrame where the `duplicated` array is `True`.

    -   Both of these methods consider all of the columns by default; alternatively one can specify any subset of columns to detect duplicates.

    -   Both of these methods keep the first observed value combination by default. Passing `take_last=True` will return the last one.

-   Transforming Data Using a Function or Mapping

    -   The Series method `map` accepts a function or dict-like object containing a mapping.

    -   The Series method `replace` provide a simpler way of replacing one or several values: `data.replace(['list-of-value-to-be-replaced'], ['one-or-list-of-value-in-replacing'])`, can also pass a dict as argument.

-   Renaming Axis Indexes

    -   The axis indexes have a `map` method like Series.

    -   Modify the DataFrame in place by assigning to index.

    -   The DataFrame method `rename` create a transformed version of a data set without modifying the original.

    -   The `rename` method can be used in conjunction with a dict-like object providing new values for a subset of the axis labels.

    -   The `rename` copies the DataFrame manually and assign to its index and columns attributes, pass `inplace=True` to modify a data set in place.

-   Discretization and Binning

    -   The `pandas.cut` method works like `R cut`.

    -   The `pandas.qcut` method work like `R cut` but on quantiles or percentiles.

-   Permutation and Random Sampling

    -   `numpy.random.permutation` can be used to produce an array of integers indicating the new ordering.

    -   `numpy.random.randint` draws random integers and can be used to generate a sample with replacement.

-   Computing Indicator/Dummy Variables

    -   `pandas.get_dummies` function can convert a categorical variable into a dummy or indicator matrix: if a column in a DataFrame has k distinct values, it derives a matrix or DataFrame containing k columns containing all 1's and 0's.

    -   `pandas.get_dummies` can be passed prefix to the columns in the indicator DataFrame: `pd.get_dummies(df['key'], prefix='key')`.

    -   Use `set`, `set.union`, `enumerate` and `pandas.get_dummies` create dummy matrix when a row in a DataFrame can belong to multiple categories.

String Manipulation
-------------------

-   String Object Methods (string)

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
<td align="left">count</td>
<td align="left">Return the number of non-overlapping occurrences of substring in the string.</td>
</tr>
<tr class="even">
<td align="left">endswith, startswith</td>
<td align="left">Returns True if string ends with suffix (starts with prefix).</td>
</tr>
<tr class="odd">
<td align="left">join</td>
<td align="left">Use string as delimiter for concatenating a sequence of other strings.</td>
</tr>
<tr class="even">
<td align="left">index</td>
<td align="left">Return position of first character in substring if found in the string. Raises ValueError if not found.</td>
</tr>
<tr class="odd">
<td align="left">find</td>
<td align="left">Return position of first character of first occurrence of substring in the string. Like index, but returns -1 if not found.</td>
</tr>
<tr class="even">
<td align="left">rfind</td>
<td align="left">Return position of first character of last occurrence of substring in the string. Returns -1 if not found.</td>
</tr>
<tr class="odd">
<td align="left">replace</td>
<td align="left">Replace occurrences of string with another string.</td>
</tr>
<tr class="even">
<td align="left">strip, rstrip, lstrip</td>
<td align="left">Trim whitespace, including newlines; equivalent to x.strip() (and rstrip, lstrip, respectively) for each element.</td>
</tr>
<tr class="odd">
<td align="left">split</td>
<td align="left">Break string into list of substrings using passed delimiter.</td>
</tr>
<tr class="even">
<td align="left">lower, upper</td>
<td align="left">Convert alphabet characters to lowercase or uppercase, respectively.</td>
</tr>
<tr class="odd">
<td align="left">ljust, rjust</td>
<td align="left">Left justify or right justify, respectively. Pad opposite side of string with spaces (or some other fill character) to return a string with a minimum width.</td>
</tr>
</tbody>
</table>

-   Regular Expressions Methods (re)

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
<td align="left">findall, finditer</td>
<td align="left">Return all non-overlapping matching patterns in a string. findall returns a list of all patterns while finditer returns them one by one from an iterator.</td>
</tr>
<tr class="even">
<td align="left">match</td>
<td align="left">Match pattern at start of string and optionally segment pattern components into groups. If the pattern matches, returns a match object, otherwise None.</td>
</tr>
<tr class="odd">
<td align="left">search</td>
<td align="left">Scan string for match to pattern; returning a <em>match object</em> if so. Unlike match, the match can be anywhere in the string as opposed to only at the beginning.</td>
</tr>
<tr class="even">
<td align="left">split</td>
<td align="left">Break string into pieces at each occurrence of pattern.</td>
</tr>
<tr class="odd">
<td align="left">sub, subn</td>
<td align="left">Replace all (sub) or first n occurrences (subn) of pattern in string with replacement expression. Use symbols \1, \2, ... to refer to match group elements in the replacement string.</td>
</tr>
</tbody>
</table>
