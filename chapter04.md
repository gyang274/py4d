<!-- README.md is generated from README.Rmd. -->
NumPy
=====

Array Creation Function
-----------------------

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
<td align="left">array</td>
<td align="left">Convert input data (list, tuple, array, or other sequence type) to an ndarray either by inferring a dtype or explicitly specifying a dtype. Copies the input data by default.</td>
</tr>
<tr class="even">
<td align="left">asarray</td>
<td align="left">Convert input to ndarray, but do not copy if the input is already an ndarray</td>
</tr>
<tr class="odd">
<td align="left">arange</td>
<td align="left">Like the built-in range but returns an ndarray instead of a list.</td>
</tr>
<tr class="even">
<td align="left">ones, ones_like</td>
<td align="left">Produce an array of all 1’s with the given shape and dtype. ones_like takes another array and produces a ones array of the same shape and dtype.</td>
</tr>
<tr class="odd">
<td align="left">zeros, zeros_like</td>
<td align="left">Like ones and ones_like but producing arrays of 0’s instead</td>
</tr>
<tr class="even">
<td align="left">empty, empty_like</td>
<td align="left">Create new arrays by allocating new memory, but do not populate with any values like ones and zeros</td>
</tr>
<tr class="odd">
<td align="left">eye, identity</td>
<td align="left">Create a square N x N identity matrix (1’s on the diagonal and 0’s elsewhere)</td>
</tr>
</tbody>
</table>

NumPy Data Types
----------------

<table style="width:38%;">
<colgroup>
<col width="6%" />
<col width="13%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Type</th>
<th align="left">Type Code</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">int8, uint8</td>
<td align="left">i1, u1</td>
<td align="left">Signed and unsigned 8-bit (1 byte) integer types</td>
</tr>
<tr class="even">
<td align="left">int16, uint16</td>
<td align="left">i2, u2</td>
<td align="left">Signed and unsigned 16-bit integer types</td>
</tr>
<tr class="odd">
<td align="left">int32, uint32</td>
<td align="left">i4, u4</td>
<td align="left">Signed and unsigned 32-bit integer types</td>
</tr>
<tr class="even">
<td align="left">int64, uint64</td>
<td align="left">i8, u8</td>
<td align="left">Signed and unsigned 32-bit integer types</td>
</tr>
<tr class="odd">
<td align="left">float16</td>
<td align="left">f2</td>
<td align="left">Half-precision floating point</td>
</tr>
<tr class="even">
<td align="left">float32</td>
<td align="left">f4 or f</td>
<td align="left">Standard single-precision floating point. Compatible with C float</td>
</tr>
<tr class="odd">
<td align="left">float64, float128</td>
<td align="left">f8 or d</td>
<td align="left">Standard double-precision floating point. Compatible with C double and Python <code>float</code> object</td>
</tr>
<tr class="even">
<td align="left">float128</td>
<td align="left">f16 or g</td>
<td align="left">Extended-precision floating point</td>
</tr>
<tr class="odd">
<td align="left">complex64, complex128, complex256</td>
<td align="left">c8, c16, c32</td>
<td align="left">Complex numbers represented by two 32, 64, or 128 floats, respectively</td>
</tr>
<tr class="even">
<td align="left">bool</td>
<td align="left">?</td>
<td align="left">Boolean type storing True and False values</td>
</tr>
<tr class="odd">
<td align="left">object</td>
<td align="left">O</td>
<td align="left">Python object type</td>
</tr>
<tr class="even">
<td align="left">string_</td>
<td align="left">S</td>
<td align="left">Fixed-length string type (1 byte per character). For example, to create a string dtype with length 10, use 'S10'.</td>
</tr>
<tr class="odd">
<td align="left">unicode_</td>
<td align="left">U</td>
<td align="left">Fixed-length unicode type (number of bytes platform specific). Same specification semantics as string_ (e.g. 'U10').</td>
</tr>
</tbody>
</table>

-   Calling ndarray's `astype` method can convert or `cast` an array from one dtype to another.

-   Calling `astype` always creates a new array (a copy of the data), even if the new dtype is the same as the old dtype.

NumPy Basic Indexing and Slicing
--------------------------------

-   An important first distinction from lists is that array slices are views on the original array. This means that the data is not copied, and any modifications to the view will be reflected in the source array.

-   If you want a copy of a slice of an ndarray instead of a view, you will need to explicitly copy the array; for example `arr[5:8].copy()`.

-   Indexing with integer and indexing with slice, like in `R`, as a consequence on result's dimension - an `3 x 3` array, `arr[2, :]` gives a view of one dimension array whereas `arr[2:, :]` gives a view of two dimension `1 x 3` array.

-   Selecting data from an array by boolean indexing always creates a copy of the data, even if the returned array is unchanged.

NumPy Fancy Indexing
--------------------

-   Fancy indexing is a term adopted by NumPy to describe indexing using integer arrays.

-   Passing multiple index arrays selects a 1D array of elements corresponding to each tuple of indices. To select the rectangular region formed by selecting a subset of the matrix’s rows and columns, either use chan rule or use the `np.ix_` function, which converts two 1D integer arrays to an indexer that selects the square region.

``` python
import numpy as np

arr = np.arange(32).reshape((8, 4))

arr[[1, 5, 7, 2], [0, 3, 1, 2]]

arr[[1, 5, 7, 2]][:, [0, 3, 1, 2]]

arr[np.ix_([1, 5, 7, 2], [0, 3, 1, 2])]
```

Universal Functions: Fast Element-wise Array Functions
------------------------------------------------------

-   Unary ufuncs

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
<td align="left">abs, fabs</td>
<td align="left">Compute the absolute value element-wise for integer, floating point, or complex values. Use fabs as a faster alternative for non-complex-valued data</td>
</tr>
<tr class="even">
<td align="left">sqrt</td>
<td align="left">Compute the square root of each element. Equivalent to arr ** 0.5</td>
</tr>
<tr class="odd">
<td align="left">square</td>
<td align="left">Compute the square of each element. Equivalent to arr ** 2</td>
</tr>
<tr class="even">
<td align="left">exp</td>
<td align="left">Compute the exponent ex of each element</td>
</tr>
<tr class="odd">
<td align="left">log, log10, log2, log1p</td>
<td align="left">Natural logarithm (base e), log base 10, log base 2, and log(1 + x), respectively</td>
</tr>
<tr class="even">
<td align="left">sign</td>
<td align="left">Compute the sign of each element: 1 (positive), 0 (zero), or -1 (negative)</td>
</tr>
<tr class="odd">
<td align="left">ceil</td>
<td align="left">Compute the ceiling of each element, i.e. the smallest integer greater than or equal to each element</td>
</tr>
<tr class="even">
<td align="left">floor</td>
<td align="left">Compute the floor of each element, i.e. the largest integer less than or equal to each element</td>
</tr>
<tr class="odd">
<td align="left">rint</td>
<td align="left">Round elements to the nearest integer, preserving the dtype</td>
</tr>
<tr class="even">
<td align="left">modf</td>
<td align="left">Return fractional and integral parts of array as separate array</td>
</tr>
<tr class="odd">
<td align="left">isnan</td>
<td align="left">Return boolean array indicating whether each value is NaN (Not a Number)</td>
</tr>
<tr class="even">
<td align="left">isfinite, isinf</td>
<td align="left">Return boolean array indicating whether each element is finite (non-inf, non-NaN) or infinite, respectively</td>
</tr>
<tr class="odd">
<td align="left">cos, cosh, sin, sinh, tan, tanh</td>
<td align="left">Regular and hyperbolic trigonometric functions</td>
</tr>
<tr class="even">
<td align="left">arccos, arccosh, arcsin, arcsinh, arctan, arctanh</td>
<td align="left">Inverse trigonometric functions</td>
</tr>
<tr class="odd">
<td align="left">logical_not</td>
<td align="left">Compute truth value of not x element-wise. Equivalent to -arr.</td>
</tr>
</tbody>
</table>

-   Binary ufuncs

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
<td align="left">add</td>
<td align="left">Add corresponding elements in arrays</td>
</tr>
<tr class="even">
<td align="left">subtract</td>
<td align="left">Subtract elements in second array from first array</td>
</tr>
<tr class="odd">
<td align="left">multiply</td>
<td align="left">Multiply array elements</td>
</tr>
<tr class="even">
<td align="left">divide, floor_divide</td>
<td align="left">Divide or floor divide (truncating the remainder)</td>
</tr>
<tr class="odd">
<td align="left">power</td>
<td align="left">Raise elements in first array to powers indicated in second array</td>
</tr>
<tr class="even">
<td align="left">maximum, fmax</td>
<td align="left">Element-wise maximum. fmax ignores NaN</td>
</tr>
<tr class="odd">
<td align="left">minimum, fmin</td>
<td align="left">Element-wise minimum. fmin ignores NaN</td>
</tr>
<tr class="even">
<td align="left">mod</td>
<td align="left">Element-wise modulus (remainder of division)</td>
</tr>
<tr class="odd">
<td align="left">copysign</td>
<td align="left">Copy sign of values in second argument to values in first argument</td>
</tr>
<tr class="even">
<td align="left">greater, greater_equal, less, less_equal, equal, not_equal</td>
<td align="left">Perform element-wise comparison, yielding boolean array. Equivalent to infix operators &gt;, &gt;=, &lt;, &lt;=, ==, !=</td>
</tr>
<tr class="odd">
<td align="left">logical_and, logical_or, logical_xor</td>
<td align="left">Compute element-wise truth value of logical operation. Equivalent to infix operators &amp;</td>
</tr>
</tbody>
</table>

Data Processing Using Arrays
----------------------------

-   The `np.meshgrid` function takes two 1D arrays and produces two 2D matrices corresponding to all pairs of (x, y) in the two arrays.

-   The `numpy.where` function is a vectorized version of the ternary expression `x if condition else y`.

<!-- -->

    result = [(x if c else y) for x, y, c in zip(xarr, yarr, cond)]

    result = np.where(cond, xarr, yarr)

Mathematical and Statistical Methods
------------------------------------

-   Basic array statistical methods

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
<td align="left">sum</td>
<td align="left">Sum of all the elements in the array or along an axis. Zero-length arrays have sum 0.</td>
</tr>
<tr class="even">
<td align="left">mean</td>
<td align="left">Arithmetic mean. Zero-length arrays have NaN mean.</td>
</tr>
<tr class="odd">
<td align="left">std, var</td>
<td align="left">Standard deviation and variance, respectively, with optional degrees of freedom adjustment (default denominator n).</td>
</tr>
<tr class="even">
<td align="left">min, max</td>
<td align="left">Minimum and maximum.</td>
</tr>
<tr class="odd">
<td align="left">argmin, argmax</td>
<td align="left">Indices of minimum and maximum elements, respectively.</td>
</tr>
<tr class="even">
<td align="left">cumsum</td>
<td align="left">Cumulative sum of elements starting from 0</td>
</tr>
<tr class="odd">
<td align="left">cumprod</td>
<td align="left">Cumulative product of elements starting from 1</td>
</tr>
</tbody>
</table>

Sorting
-------

-   NumPy arrays can be sorted *in-place* using the `sort` method.

-   The top level method `np.sort` returns a *sorted copy* of an array instead of modifying the array in place.

Unique and Other Set Logic
--------------------------

-   Array set operations

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
<td align="left">unique(x)</td>
<td align="left">Compute the sorted, unique elements in x</td>
</tr>
<tr class="even">
<td align="left">intersect1d(x, y)</td>
<td align="left">Compute the sorted, common elements in x and y</td>
</tr>
<tr class="odd">
<td align="left">union1d(x, y)</td>
<td align="left">Compute the sorted union of elements</td>
</tr>
<tr class="even">
<td align="left">in1d(x, y)</td>
<td align="left">Compute a boolean array indicating whether each element of x is contained in y</td>
</tr>
<tr class="odd">
<td align="left">setdiff1d(x, y)</td>
<td align="left">Set difference, elements in x that are not in y</td>
</tr>
<tr class="even">
<td align="left">setxor1d(x, y)</td>
<td align="left">Set symmetric differences; elements that are in either of the arrays, but not both</td>
</tr>
</tbody>
</table>

File Input and Output with Arrays
---------------------------------

-   Storing Arrays on Disk in Binary Format

    -   `np.save` and `np.load` are the two workhorse functions for efficiently saving and loading array data on disk. Arrays are saved by default in an uncompressed raw binary format with file extension `.npy`.

    -   `np.savez` saves multiple arrays in a zip archive, passing the arrays as keyword arguments: `np.savez('array_archive.npz', a=arr, b=arr)`. When loading an `.npz` file, you get back a dict-like object which loads the individual arrays lazily: `arch = np.load('array_archive.npz'); arch['b']`.

-   Saving and Loading Text Files

    -   `np.loadtxt` or the more specialized `np.genfromtxt` will at times be useful to load data into vanilla NumPy arrays.

    -   `np.savetxt` performs the inverse operation: writing an array to a delimited text file. `genfromtxt` is similar to loadtxt but is geared for structured arrays and missing data handling.

Linear Algebra: `numpy.linalg`
------------------------------

-   `numpy.linalg` has a standard set of matrix decompositions and things like inverse and determinant. These are implemented under the hood using the same industry-standard `Fortran` libraries used in other languages like `MATLAB` and `R`, such as like `BLAS`, `LAPACK`, or possibly (depending on your NumPy build) the `Intel MKL`.

-   Commonly-used `numpy.linalg` functions

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
<td align="left">diag</td>
<td align="left">Return the diagonal (or off-diagonal) elements of a square matrix as a 1D array, or convert a 1D array into a square matrix with zeros on the off-diagonal</td>
</tr>
<tr class="even">
<td align="left">dot</td>
<td align="left">Matrix multiplication</td>
</tr>
<tr class="odd">
<td align="left">trace</td>
<td align="left">Compute the sum of the diagonal elements</td>
</tr>
<tr class="even">
<td align="left">det</td>
<td align="left">Compute the matrix determinant</td>
</tr>
<tr class="odd">
<td align="left">eig</td>
<td align="left">Compute the eigenvalues and eigenvectors of a square matrix</td>
</tr>
<tr class="even">
<td align="left">inv</td>
<td align="left">Compute the inverse of a square matrix</td>
</tr>
<tr class="odd">
<td align="left">pinv</td>
<td align="left">Compute the Moore-Penrose pseudo-inverse inverse of a square matrix</td>
</tr>
<tr class="even">
<td align="left">qr</td>
<td align="left">Compute the QR decomposition</td>
</tr>
<tr class="odd">
<td align="left">svd</td>
<td align="left">Compute the singular value decomposition (SVD)</td>
</tr>
<tr class="even">
<td align="left">solve</td>
<td align="left">Solve the linear system Ax = b for x, where A is a square matrix</td>
</tr>
<tr class="odd">
<td align="left">lstsq</td>
<td align="left">Compute the least-squares solution to y = Xb</td>
</tr>
</tbody>
</table>

Random Number Generation
------------------------

-   Partial list of numpy.random functions

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
<td align="left">seed</td>
<td align="left">Seed the random number generator</td>
</tr>
<tr class="even">
<td align="left">permutation</td>
<td align="left">Return a random permutation of a sequence, or return a permuted range</td>
</tr>
<tr class="odd">
<td align="left">shuffle</td>
<td align="left">Randomly permute a sequence in place</td>
</tr>
<tr class="even">
<td align="left">rand</td>
<td align="left">Draw samples from a uniform distribution</td>
</tr>
<tr class="odd">
<td align="left">randint</td>
<td align="left">Draw random integers from a given low-to-high range</td>
</tr>
<tr class="even">
<td align="left">randn</td>
<td align="left">Draw samples from a normal distribution with mean 0 and standard deviation 1 (MATLAB-like interface)</td>
</tr>
<tr class="odd">
<td align="left">binomial</td>
<td align="left">Draw samples a binomial distribution</td>
</tr>
<tr class="even">
<td align="left">normal</td>
<td align="left">Draw samples from a normal (Gaussian) distribution</td>
</tr>
<tr class="odd">
<td align="left">beta</td>
<td align="left">Draw samples from a beta distribution</td>
</tr>
<tr class="even">
<td align="left">chisquare</td>
<td align="left">Draw samples from a chi-square distribution</td>
</tr>
<tr class="odd">
<td align="left">gamma</td>
<td align="left">Draw samples from a gamma distribution</td>
</tr>
<tr class="even">
<td align="left">uniform</td>
<td align="left">Draw samples from a uniform [0, 1) distribution</td>
</tr>
</tbody>
</table>
