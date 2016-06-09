<!-- README.md is generated from README.Rmd. -->
file.io
=======

Reading and Writing Data in Text Format
---------------------------------------

-   Parsing functions in `pandas`:

<table style="width:29%;">
<colgroup>
<col width="12%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Function</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">read_csv</td>
<td align="left">Load delimited data from a file, URL, or file-like object. Use comma as default delimiter</td>
</tr>
<tr class="even">
<td align="left">read_table</td>
<td align="left">Load delimited data from a file, URL, or file-like object. Use tab ('') as default delimiter</td>
</tr>
<tr class="odd">
<td align="left">read_fwf</td>
<td align="left">Read data in fixed-width column format (that is, no delimiters)</td>
</tr>
<tr class="even">
<td align="left">read_clipboard</td>
<td align="left">Version of read_table that reads data from the clipboard. Useful for converting tables from web pages</td>
</tr>
</tbody>
</table>

-   `read_csv` and `read_table` function arguments

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
<td align="left">path</td>
<td align="left">String indicating filesystem location, URL, or file-like object</td>
</tr>
<tr class="even">
<td align="left">sep or delimiter</td>
<td align="left">Character sequence or regular expression to use to split fields in each row</td>
</tr>
<tr class="odd">
<td align="left">header</td>
<td align="left">Row number to use as column names. Defaults to 0 (first row), but should be None if there is no header row</td>
</tr>
<tr class="even">
<td align="left">index_col</td>
<td align="left">Column numbers or names to use as the row index in the result. Can be a single name/number or a list of them for a hierarchical index</td>
</tr>
<tr class="odd">
<td align="left">names</td>
<td align="left">List of column names for result, combine with header=None</td>
</tr>
<tr class="even">
<td align="left">skiprows</td>
<td align="left">Number of rows at beginning of file to ignore or list of row numbers (starting from 0) to skip</td>
</tr>
<tr class="odd">
<td align="left">na_values</td>
<td align="left">Sequence of values to replace with NA</td>
</tr>
<tr class="even">
<td align="left">comment</td>
<td align="left">Character or characters to split comments off the end of lines</td>
</tr>
<tr class="odd">
<td align="left">parse_dates</td>
<td align="left">Attempt to parse data to datetime; False by default. If True, will attempt to parse all columns. Otherwise can specify a list of column numbers or name to parse. If element of list is tuple or list, will combine multiple columns together and parse to date (for example if date/time split across two columns)</td>
</tr>
<tr class="even">
<td align="left">keep_date_col</td>
<td align="left">If joining columns to parse date, drop the joined columns. Default True converters Dict containing column number of name mapping to functions. For example {'foo': f} would apply the function f to all values in the 'foo' column</td>
</tr>
<tr class="odd">
<td align="left">dayfirst</td>
<td align="left">When parsing potentially ambiguous dates, treat as international format (e.g. 7/6/2012 -&gt; June 7, 2012). Default False date_parser Function to use to parse dates</td>
</tr>
<tr class="even">
<td align="left">nrows</td>
<td align="left">Number of rows to read from beginning of file</td>
</tr>
<tr class="odd">
<td align="left">iterator</td>
<td align="left">Return a TextParser object for reading file piecemeal</td>
</tr>
<tr class="even">
<td align="left">chunksize</td>
<td align="left">For iteration, size of file chunks</td>
</tr>
<tr class="odd">
<td align="left">skip_footer</td>
<td align="left">Number of lines to ignore at end of file</td>
</tr>
<tr class="even">
<td align="left">verbose</td>
<td align="left">Print various parser output information, like the number of missing values placed in non-numeric columns</td>
</tr>
<tr class="odd">
<td align="left">encoding</td>
<td align="left">Text encoding for unicode. For example 'utf-8' for UTF-8 encoded text</td>
</tr>
<tr class="even">
<td align="left">squeeze</td>
<td align="left">If the parsed data only contains one column return a Series</td>
</tr>
<tr class="odd">
<td align="left">thousands</td>
<td align="left">Separator for thousands, e.g. ',' or '.'</td>
</tr>
</tbody>
</table>

<<<<<<< HEAD
-   Q: How to specify a index\_col while still kepping the column in DataFrame?
=======
    - Q: How to specify a index\_col while still kepping the column in DataFrame?
>>>>>>> a05b8e730f0cbdc8f66a7f4d107f55aad5302f85

Manually Working with Delimited Formats
---------------------------------------

-   The built-in csv module, `csv.reader` method takes any open file or file-like object, and processes any file with a single-character delimiter.

-   CSV files come in many different flavors. Defining a new format with a different delimiter, string quoting convention, or line terminator is done by defining a simple subclass of `csv.Dialect`:

<!-- -->

    class my_dialect(csv.Dialect):
      lineterminator = '\n'
      delimiter = ';'
      quotechar = '"'
    reader = csv.reader(f, dialect=my_dialect)

-   Individual CSV dialect parameters can also be given as keywords to `csv.reader` without having to define a subclass: `reader = csv.reader(f, delimiter='|')`.

-   CSV dialect options

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
<td align="left">delimiter</td>
<td align="left">One-character string to separate fields. Defaults to ','.</td>
</tr>
<tr class="even">
<td align="left">lineterminator</td>
<td align="left">Line terminator for writing, defaults to ''. Reader ignores this and recognizes cross-platform line terminators.</td>
</tr>
<tr class="odd">
<td align="left">quotechar</td>
<td align="left">Quote character for fields with special characters (like a delimiter). Default is '&quot;'.</td>
</tr>
<tr class="even">
<td align="left">quoting</td>
<td align="left">Quoting convention. Options include csv.QUOTE_ALL (quote all fields), csv.QUOTE_MINIMAL (only fields with special characters like the delimiter), csv.QUOTE_NONNUMERIC, and csv.QUOTE_NON (no quoting). See Python's documentation for full details. Defaults to QUOTE_MINIMAL.</td>
</tr>
<tr class="odd">
<td align="left">skipinitialspace</td>
<td align="left">Ignore whitespace after each delimiter. Default False.</td>
</tr>
<tr class="even">
<td align="left">doublequote</td>
<td align="left">How to handle quoting character inside a field. If True, it is doubled. See online documentation for full detail and behavior.</td>
</tr>
<tr class="odd">
<td align="left">escapechar</td>
<td align="left">String to escape the delimiter if quoting is set to csv.QUOTE_NONE. Disabled by default.</td>
</tr>
</tbody>
</table>

-   Use `csv.writer` to write delimited files manually. It accepts an open, writable file object and the same dialect and format options as `csv.reader`:

<!-- -->

    with open('mydata.csv', 'w') as f:
      writer = csv.writer(f, dialect=my_dialect)
      writer.writerow(('one', 'two', 'three'))
      writer.writerow(('1', '2', '3'))
      writer.writerow(('4', '5', '6'))
      writer.writerow(('7', '8', '9'))

JSON Data
---------

-   Library `json` is built into Python standard library, use `import json`, `json.loads([JSON-Object])` and `json.dumps([Python-Dict])`.

-   `pandas` has fast native JSON decoding `read_json` and exporting `to_json`.

XML and HTML: Web Scraping
--------------------------

-   `lxml` <http://lxml.de>

-   Parse HTML using `lxml.html`

<!-- -->

    from lxml.html import parse
    from urllib2 import urlopen

    parsed = parse(urlopen('http://finance.yahoo.com/q/op?s=AAPL+Options'))

    doc = parsed.getroot()

    links = doc.findall('.//a')

    lnk = links[2]

    lnk.get('href')

    lnk.text_content()

    lnkdict = { lnk.text_content(): lnk.get('href') for lnk in doc.findall('.//a') }

    tables = doc.findall('.//table')

-   Parse XML using `lxml.objectify`

Binary Data Formats
-------------------

-   The built-in `pickle` serialization stores data efficiently in binary format. All `pandas` objects have a `save` method which writes the data to disk as a `pickle`, read it back with `pandas.load`.

    -   `pickle` is only recommended as a short-term storage format. The problem is that it is hard to guarantee that the format will be stable over time; an object pickled today may not unpickle with a later version of a library. I have made every effort to ensure that this does not occur with pandas, but at some point in the future it may be necessary to "break" the pickle format.
-   HDF5 format where HDF stands for *hierarchical data format*. There are not one but two interfaces to the HDF5 library in Python, PyTables and h5py, each of which takes a different approach to the problem.

    -   h5py provides a direct, but high-level interface to the HDF5 API.

    -   PyTables abstracts many of the details of Binary Data Formats HDF5 to provide multiple flexible data containers, table indexing, querying capability, and some support for out-of-core computations.

    -   `pandas` has a minimal dict-like `HDFStore` class, which uses PyTables to store `pandas` objects.

    -   HDF5 is not a database. It is best suited for write-once, read-many datasets. While data can be added to a file at any time, if multiple writers do so simultaneously, the file can become corrupted.

Reading Microsoft Excel Files
-----------------------------

-   `pandas` also supports reading tabular data stored in Excel 2003 (and higher) files using the ExcelFile class. Interally ExcelFile uses the xlrd and openpyxl packages, so one may have to install them first.

<!-- -->

    xls_file = pd.ExcelFile('data.xls')

    table = xls_file.parse('Sheet1')

Interacting with Databases
--------------------------

-   `sqlite3`

-   `import pandas.io.sql as sql; sql.read_sql('select * from test', con)`
