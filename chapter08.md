<!-- README.md is generated from README.Rmd. -->
matplotlib
==========

A Brief matplotlib API Primer
-----------------------------

-   Figures and Subplots

<!-- -->

    import matplotlib.pyplot as plt

    - pyplot.subplots options

        Argument | Description
        -------- | -----------
        nrows | Number of rows of subplots
        ncols | Number of columns of subplots
        sharex | All subplots should use the same X-axis ticks (adjusting the xlim will affect all subplots)
        sharey | All subplots should use the same Y-axis ticks (adjusting the ylim will affect all subplots)
        subplot\_kw | Dict of keywords for creating the subplots
        **fig\_kw | Additional keywords to subplots are used when creating the figure, such as plt.subplots(2, 2, figsize=(8, 6))

    - The `subplots_adjust` method on Figure, also available as a top-level function, adjusts the spacing around subplots.

        - matplotlib leaves a certain amount of padding around the outside of the subplots and spacing between subplots by default.
        
        - `subplots_adjust(left=None, bottom=None, right=None, top=None, wspace=None, hspace=None)`, `wspace` and `hspace` controls the percent of the figure width and figure height, respectively, to use as spacing between subplots.

-   Colors, Markers, and Line Styles

<!-- -->

    ## colors and linestyles

    ax.plot(x-coordindate, y-coordindate, <string abbreviation indicating color and line style>'k--')

    ax.plot(x-coordindate, y-coordindate, linestyle='--', color='k')

    ## markers and drawstyles

    plt.plot(data, color='k', linestyle='dashed', marker='o')

    plt.plot(data, 'k-', drawstyle='steps-post', label='steps-post')

-   Ticks, Labels, and Legends

    -   Two options: `pyplot` interface, Matlab like, designed for interactive use, and `native matplotlib API`, more object-oriented.
-   Annotations and Drawing on a Subplot

    -   Annotations and text can be added using the text, arrow, and annotate functions.

<!-- -->

    ## text draws text at given coordinates (x, y) on the plot with optional custom styling:

    ax.text(x, y, 'Hello world!', family='monospace', fontsize=10)

    ## annotate

    ax.annotate(s=[label], xy=[(x, y): position of element to annotate], 
                xytext=[(x, y): optional, default: None, position of the label `s`],
                arrowprops=[`matplotlib.lines.Line2D` properties, optional],
                horizontalalignment='left', verticalalignment='top')

    - `matplotlib` has objects that represent many common shapes, referred to as patches. Some of these, like Rectangle and Circle are found in matplotlib.pyplot, but the full set is located in `matplotlib.patches`. To add a shape to a plot, one create the patch object `shp` and add it to a subplot by calling `ax.add_patch(shp)`.

-   Saving Plots to File

`plt.savefig` function and `fig.savefig` method options

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
<td align="left">fname</td>
<td align="left">String containing a filepath or a Python file-like object. The figure format is inferred from the file extension, e.g. .pdf for PDF or .png for PNG.</td>
</tr>
<tr class="even">
<td align="left">dpi</td>
<td align="left">The figure resolution in dots per inch; defaults to 100 out of the box but can be configured</td>
</tr>
<tr class="odd">
<td align="left">facecolor, edgecolor</td>
<td align="left">The color of the figure background outside of the subplots. 'w' (white), by default</td>
</tr>
<tr class="even">
<td align="left">format</td>
<td align="left">The explicit file format to use ('png', 'pdf', 'svg', 'ps', 'eps', ...)</td>
</tr>
<tr class="odd">
<td align="left">bbox_inches</td>
<td align="left">The portion of the figure to save. If 'tight' is passed, will attempt to trim the empty space around the figure</td>
</tr>
</tbody>
</table>

`matplotlib` Configuration
--------------------------

-   `plt.rc` method: `plt.rc('figure', figsize=(10, 10))`

-   `matplotlib` comes with a configuration file `matplotlibrc` in the `matplotlib/mpl-data` directory that can be used for more extensive customization and to see a list of all the options. One can customize this file and place it in home directory titled `.matplotlibrc`, and it will be loaded each time when using `matplotlib`.

Plotting Functions in pandas
----------------------------

-   Line Plots

    -   Series and DataFrame each have a `plot` method for making many different plot types, and make line plots by default.

    -   `Series.plot` method arguments

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
        <td align="left">label</td>
        <td align="left">Label for plot legend</td>
        </tr>
        <tr class="even">
        <td align="left">ax</td>
        <td align="left">matplotlib subplot object to plot on. If nothing passed, uses active matplotlib subplot</td>
        </tr>
        <tr class="odd">
        <td align="left">style</td>
        <td align="left">Style string, like 'ko--', to be passed to matplotlib.</td>
        </tr>
        <tr class="even">
        <td align="left">alpha</td>
        <td align="left">The plot fill opacity (from 0 to 1)</td>
        </tr>
        <tr class="odd">
        <td align="left">kind</td>
        <td align="left">Can be 'line', 'bar', 'barh', 'kde'</td>
        </tr>
        <tr class="even">
        <td align="left">logy</td>
        <td align="left">Use logarithmic scaling on the Y axis</td>
        </tr>
        <tr class="odd">
        <td align="left">use_index</td>
        <td align="left">Use the object index for tick labels</td>
        </tr>
        <tr class="even">
        <td align="left">rot</td>
        <td align="left">Rotation of tick labels (0 through 360)</td>
        </tr>
        <tr class="odd">
        <td align="left">xticks</td>
        <td align="left">Values to use for X axis ticks</td>
        </tr>
        <tr class="even">
        <td align="left">yticks</td>
        <td align="left">Values to use for Y axis ticks</td>
        </tr>
        <tr class="odd">
        <td align="left">xlim</td>
        <td align="left">X axis limits (e.g. [0, 10])</td>
        </tr>
        <tr class="even">
        <td align="left">ylim</td>
        <td align="left">Y axis limits</td>
        </tr>
        <tr class="odd">
        <td align="left">grid</td>
        <td align="left">Display axis grid (on by default)</td>
        </tr>
        </tbody>
        </table>

    -   `DataFrame.plot` method specific arguments

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
        <td align="left">subplots</td>
        <td align="left">Plot each DataFrame column in a separate subplot</td>
        </tr>
        <tr class="even">
        <td align="left">sharex</td>
        <td align="left">If subplots=True, share the same X axis, linking ticks and limits</td>
        </tr>
        <tr class="odd">
        <td align="left">sharey</td>
        <td align="left">If subplots=True, share the same Y axis</td>
        </tr>
        <tr class="even">
        <td align="left">figsize</td>
        <td align="left">Size of figure to create as tuple</td>
        </tr>
        <tr class="odd">
        <td align="left">title</td>
        <td align="left">Plot title as string</td>
        </tr>
        <tr class="even">
        <td align="left">legend</td>
        <td align="left">Add a subplot legend (True by default)</td>
        </tr>
        <tr class="odd">
        <td align="left">sort_columns</td>
        <td align="left">Plot columns in alphabetical order; by default uses existing column order</td>
        </tr>
        </tbody>
        </table>

-   Bar Plots

    -   Pass kind='bar' (vertical bars) or kind='barh' (horizontal bars) to make bar plots, instead of line plots. The Series or DataFrame index will be used as the X (bar) or Y (barh) ticks.

<!-- -->

    ## A useful recipe for bar plots (as seen in an earlier chapter) is to visualize a Series’s value frequency using value_counts:

    s.value_counts().plot(kind='bar')

-   Histograms and Density Plots

    -   The `hist` method on Series plots a histogram, passing `bin=40` for number of bins.

    -   The `plot` method on Series with parameter `kind='kde'` makes a density plot using the standard mixture-of-normals KDE (kernel density estimate) plot.

-   Scatter Plots

    -   The `matplotlib` has a `scatter` plotting function: `plt.scatter(data1, data2)`.

    -   The `pandas` has a `scatter_matrix` function for creating all the scatter plots among variables from a DataFrame, also known as a pairs plot or scatter plot matrix. It also supports placing histograms or density plots of each variable along the diagonal by passing `diagonal='kde'`.

Maps Plot
---------

-   The `basemap` toolkit <http://matplotlib.github.com/basemap>, an add-on to `matplotlib`, enables plotting 2D data on maps in Python.

<!-- -->

    from mpl_toolkits.basemap import Basemap
