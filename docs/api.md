# API reference

[← Back to the README](../README.md)

- [Drawing](#drawing)
- [Labels and settings](#labels-and-settings)
- [Figures](#figures)
- [Format strings](#format-strings)
- [Colours and colormaps](#colours-and-colormaps)
- [Limitations](#limitations)

## Drawing

Each of these is a method of an axes (`ax plot(...)`) and of `Plot` (the current axes). They
return the artist they add, a Dict (`line get("color")`, `line set("label", "new")`).

| | |
|---|---|
| `plot(ys)`, `plot(xs, ys)`, `plot(xs, ys, fmt)` | Lines and markers. Options: `color`, `label`, `linewidth` (`lw`), `linestyle` (`ls`), `marker`, `markersize` (`ms`), `markerfacecolor`, `markeredgecolor`, `alpha`. `nil` (or `nan`) values leave a gap. Rows of numbers (`net history`) plot one line per column; `label` may then be an Array. |
| `scatter(xs, ys, opts)` | Markers. `s`: area in points² (one number or one per point); `c`: a colour, a colour per point, or a number per point mapped through `cmap` (with `vmin`, `vmax`); `marker`, `alpha`, `edgecolors`, `label`. |
| `bar(xs, heights, opts)` | Vertical bars. `xs` may be strings, which label bars at 0, 1, 2, ... Options: `width` (0.8), `bottom`, `align` (`"center"` or `"edge"`), `color` (one, or one per bar), `edgecolor`, `linewidth`, `label`, `alpha`. |
| `barh(ys, widths, opts)` | Horizontal bars; `height` and `left` instead of `width` and `bottom`. Category labels read top to bottom. |
| `hist(values, bins, opts)` | A histogram. `bins` is a count (10) or an Array of edges. Options: `bins`, `range: [lo, hi]`, `density`, `histtype` (`"bar"` or `"step"`), `color`, `alpha`, `label`. Returns `[counts, edges, artist]`. |
| `fillBetween(xs, y1, y2, opts)` | Shades between two curves (`y2` is 0 if left out, or a number). `color`, `alpha`, `edgecolor`, `label`. |
| `fillBetweenx(ys, x1, x2, opts)` | The same across: between two curves of x over y. |
| `fill(xs, ys, opts)` | A filled polygon through the points (closed for you), or several: `fill([xs1, xs2], [ys1, ys2])`. `color`, `alpha`, `edgecolor`, `linewidth`, `label`. |
| `pcolormesh(C)`, `pcolormesh(X, Y, C, opts)` | A grid of coloured cells, `C` as rows (row 0 at the bottom). `X` and `Y` are the cells' edges (one more than `C`'s columns and rows), or their centres, or mesh grids of the corners for cells that aren't rectangles. `cmap`, `vmin`, `vmax`, `alpha`, `edgecolors`, `linewidth`; `nil` and `nan` cells are empty. `pcolor` is the same. |
| `quiver(U, V)`, `quiver(X, Y, U, V, C, opts)` | Arrows of a vector field. `U`, `V` as rows (`X`, `Y` one value per column / row, mesh grids, or left out) or flat lists (`X`, `Y` the points); `C` colours them through `cmap`. `scale` is the vector length per data unit (by default the longest arrow is about a grid step), `width` (points, 1.5), `headwidth`, `headlength`, `pivot` (`"tail"`, `"mid"`, `"tip"`), `color`, `alpha`, `label`. |
| `step(xs, ys, fmt, opts)` | A step line. `where`: `"pre"` (the default), `"post"` or `"mid"`; and `plot`'s options. |
| `errorbar(xs, ys, opts)` | Points or a line with error bars. `yerr`, `xerr`: a number, one per point, or `[lows, highs]`; `fmt` (`"o"`, `"s--"`; `"none"` for bars only), `capsize` (points), `ecolor`, `elinewidth`, and `plot`'s options. Returns `[line, bars]`. |
| `axhline(y, opts)`, `axvline(x, opts)` | A line across the whole axes. `color`, `linestyle`, `linewidth`, `alpha`, `label`. |
| `axhspan(y0, y1, opts)`, `axvspan(x0, x1, opts)` | A band across the whole axes, from `y0` to `y1` (or `x0` to `x1`). Two more numbers before the options limit it to fractions of the axes' width (height): `axhspan(y0, y1, 0.25, 0.75)`. `color` (`facecolor`), `alpha`, `edgecolor`, `linewidth`, `label`. |
| `hexbin(xs, ys, opts)` | Points binned into hexagons, coloured by how many fall in each. `gridsize` (hexagons across, 100; or `[nx, ny]`), `bins: "log"` (colour by log10 count; the colour bar is ticked in powers of ten), `C` (a value per point, reduced per hexagon by `reduceC`: `"mean"`, `"sum"`, `"max"`, `"min"`, `"median"` or a block), `mincnt` (1: empty hexagons are left out), `cmap`, `vmin`, `vmax`, `alpha`, `edgecolors`, `extent`, `label`. |
| `hist2d(xs, ys, bins, opts)` | A 2-D histogram. `bins`: a count (10), `[nx, ny]`, or `[xEdges, yEdges]`. `range: [[x0, x1], [y0, y1]]`, `density`, `cmin` / `cmax` (cells outside are left empty), `cmap`, `vmin`, `vmax`, `alpha`. Returns `[counts, xEdges, yEdges, artist]` as numpy does: `counts at(i) at(j)` is x bin `i`, y bin `j`. |
| `text(x, y, s, opts)` | Text at data coordinates, or axes fractions with `transform: "axes"`. `fontsize`, `color`, `ha` (`"left"`, `"center"`, `"right"`), `va` (`"baseline"`, `"center"`, `"top"`, `"bottom"`), `rotation`, `fontweight`. |
| `annotate(s, xy, xytext, opts)` | Text at `xytext` with an arrow to `xy` (`[x, y]` each; without `xytext` the text goes at `xy`). `xycoords` and `textcoords`: `"data"` (the default), `"axes fraction"`, `"figure fraction"`, or for the text `"offset points"` from `xy`. `arrowprops: #{arrowstyle:, color:, linewidth:, linestyle:, shrink:, shrinkA:, shrinkB:}` draws the arrow; `arrowstyle` is `"-|>"` (the default), `"->"`, `"-"`, `"<-"`, `"<->"`, `"<|-"` or `"<|-|>"`. `bbox: #{fc:, ec:, lw:, pad:, alpha:}` puts a box behind the text. Also `fontsize`, `color`, `ha`, `va`, `fontweight`. |
| `imshow(data, opts)` | An image or heatmap: rows of numbers (through `cmap`, scaled to `vmin`..`vmax`; `nil` and `nan` cells are transparent) or rows of `[r, g, b]` or `[r, g, b, a]` pixels (0..1, or 0..255). A flat Array needs `shape: [rows, cols]` unless it is square: 784 numbers show as 28 x 28. An `Image` from [clay-image](https://github.com/mseminatore/clay-image) works too. Options: `cmap`, `vmin`, `vmax`, `aspect` (`"equal"` or `"auto"`), `origin` (`"upper"` or `"lower"`), `extent`. |
| `pie(values, opts)` | A pie chart (the axes become round, without a frame). `labels`, `colors`, `autopct` (`"%1.1f%%"`, `"{:.0f}%"` or a block given the percentage), `startangle` (degrees, anticlockwise from 3 o'clock), `counterclock`, `explode` (an offset per wedge), `radius`, `pctdistance` (0.6), `labeldistance` (1.1), `wedgeprops: #{width:, edgecolor:, linewidth:}` (a `width` makes a donut), `textprops: #{fontsize:, color:}`. Returns `[wedges, texts, autotexts]`; `legend` lists the wedges. |
| `stackplot(xs, [ys1, ys2, ...], opts)` | Stacked areas, bottom first (the series may also be separate arguments). `labels`, `colors`, `alpha`, `edgecolor`, `baseline` (`"zero"` or `"sym"`). Returns the areas. |
| `boxplot(data, opts)` | Box plots of one data set (an Array of numbers), several (an Array of Arrays) or named ones (a Dict; its keys label the boxes). Boxes run from the first to the third quartile (numpy's quantiles) with a line at the median; whiskers reach the furthest data within `whis` box lengths (1.5), or `whis: [5, 95]` percentiles, and points beyond are fliers. Options: `positions`, `widths` (0.5), `labels`, `orientation` (`"vertical"` or `"horizontal"`; `vert: false` works too), `notch`, `showmeans`, `showfliers`, `showcaps`, `showbox`, `sym` (`""` hides fliers), `patchArtist` (filled boxes), `colors` (a fill per box), `label`, and `boxprops`, `medianprops`, `whiskerprops`, `capprops`, `flierprops`, `meanprops`. Returns the artist; `get("stats")` has each box's numbers. |
| `violinplot(data, opts)` | The shape of each data set's distribution (a Gaussian kernel density estimate), mirrored about its position. Data as for `boxplot`. Options: `positions`, `widths` (0.5), `labels`, `orientation`, `showextrema` (true), `showmeans`, `showmedians`, `quantiles` (`[0.25, 0.75]` for every set, or one list per set), `points` (100), `bwMethod` (`"scott"`, `"silverman"` or a number), `color`, `colors`, `alpha` (0.3), `label`. |
| `contour(Z)`, `contour(X, Y, Z, levels, opts)` | Contour lines of `Z`, rows of numbers (`Z at(i) at(j)` is at row `i`, column `j`; row 0 at the bottom). `X` and `Y` place the columns and rows: one value per column / row, or rows like `Z`'s (a mesh grid); without them columns and rows are at 0, 1, 2, ... `levels` is about how many (7) or a list. Options: `levels`, `colors` (one for every line, which dashes the negative levels, or one per level), `cmap`, `linewidths`, `linestyles`, `alpha`, `label`. `nil` and `nan` cells are left out. Returns the artist, for `clabel` and `colorbar`. |
| `contourf(...)` | Filled contours, bands of colour between the levels; arguments as `contour`'s. Given a number of levels, the bands cover all the data. `colors` (one per band), `cmap`, `alpha`, `label`. `colorbar` shows the bands, ticked at the levels. |
| `clabel(cs, opts)` | Write each level on its contour lines, turned to follow them, in a gap cut for the text. `fmt` (`"%.1f"`, `"{:.0f}"` or a block), `fontsize`, `colors`, `inline` (true). Lines too short for their label stay unlabelled. |
| `barLabel(bars, opts)` | Write values on the bars `bar`, `barh` or `hist` returned. `fmt` (`"%g"`, `"%d%%"`, `"{:,.0f}"`, or a block), `labels` (your own text instead), `labelType` (`"edge"` or `"center"`), `padding` (points), `fontsize`, `color`. |
| `colorbar(artist, opts)` | A colour bar beside the axes for an image or a colour-mapped scatter (the last one if you leave the artist out). `label`. |

## Labels and settings

| | |
|---|---|
| `title(s, opts)` | `fontsize`, `loc` (`"center"`, `"left"`, `"right"`) |
| `xlabel(s)`, `ylabel(s)` | Axis labels |
| `xlim(lo, hi)`, `ylim(lo, hi)` | Set the range shown (`nil` keeps an end automatic; an Array works too). With no arguments, returns the range in use. |
| `xticks(values, labels, opts)`, `yticks(...)` | Choose the ticks; `labels` names them, `rotation` turns them. `xticks([])` hides them. |
| `grid(on, opts)` | Grid lines at the ticks: `grid`, `grid(false)`, `grid(#{axis: "y", color:, linestyle:, alpha:})` |
| `legend(opts)`, `legend(labels)` | A legend of the labelled artists. `loc`: `"best"` (the default: the corner covering the least data), `"upper right"`, `"upper left"`, `"lower left"`, `"lower right"`, `"right"`, `"center left"`, `"center right"`, `"lower center"`, `"upper center"`, `"center"`. `bboxToAnchor: [x, y]` (axes fractions, 1.02 just past the right edge) puts the legend's `loc` corner there, outside the axes if you like, and the layout makes room for it. `ncol` lays the entries out in columns. Also `fontsize`, `title`, `framealpha`, `frameon`. An Array of labels names the artists in order. |
| `twinx`, `twiny` | A second axes over this one sharing its x axis, with its own y axis on the right (`twinx`); or sharing y, with an x axis along the top (`twiny`). Returns the new axes (`Plot twinx` also makes it current). The two share one colour cycle and one title, and a legend on either lists the labelled artists of both. |
| `axis(mode)` | `"off"` hides the frame, ticks and labels; `"equal"` makes a unit the same length on both axes; `"auto"`; `"tight"`; or `[x0, x1, y0, y1]`. |
| `invertYaxis` | Turn the y axis upside down |
| `clear` | Remove everything drawn and set on the axes, to draw it afresh (`Plot cla` for the current axes) |
| `xscale(kind)`, `yscale(kind)` | `"log"` or `"linear"`. Log axes are ticked at powers of ten (with minor ticks between) and leave out values at or below zero. `semilogy(...)`, `semilogx(...)` and `loglog(...)` are `plot` on log axes. |
| `set(opts)` | Several at once: `title`, `xlabel`, `ylabel`, `xlim`, `ylim`, `xticks`, `yticks`, `xscale`, `yscale`, `aspect` |

## Figures

| | |
|---|---|
| `Plot figure(opts)` | A new current figure. `figsize: [width, height]` in inches (6.4 x 4.8), `dpi` (100), `facecolor`. |
| `Plot subplots(rows, cols, opts)` | A new figure with a grid of axes: `[fig, axs]`. `axs` is one axes for 1 x 1, an Array for one row or column, and an Array of rows otherwise. `sharex`, `sharey`: `true` (all the axes), `"col"` or `"row"` share one range and scale (`xlim`, `xscale` on one set them all), and inner tick labels are left out: x labels but the bottom row's when columns share, y labels but the first column's when rows share. |
| `Plot subplotMosaic(layout, opts)` | A new figure of named axes: `layout` has a String a row (a character a cell; `"."` is empty) or Arrays of names; a name filling a rectangle of cells is one axes over all of them. Returns `[fig, axs]`, `axs` a Dict by name. |
| `Plot subplot(rows, cols, index)` | Make the axes at `index` (1-based, along rows) of the current figure current, adding it if needed |
| `projection: "polar"` | In `Plot subplots(..., opts)`, `Plot subplot(r, c, i, opts)` and `fig addSubplot`: polar axes (see the [guide](guide.md#fields-and-polar-axes)). `Plot polar(thetas, rs, fmt, opts)` plots on them. |
| `Plot subplot2grid(shape, loc, opts)` | An axes spanning cells: `[rows, cols]`, the top left cell `[row, col]` (0-based), `#{rowspan:, colspan:}` |
| `fig legend(opts)`, `Plot figlegend(opts)` | One legend for all the axes (each label once). `loc`: the corners, sides and centre of the figure, or `"outside right"`, `"outside left"`, `"outside upper center"`, `"outside lower center"` (and `"outside right upper"` / `"outside right lower"`), beside the axes, which make room for it. Also `ncol`, `title`, `fontsize`. |
| `Plot gcf`, `Plot gca`, `Plot sca(ax)` | The current figure and axes; make an axes current |
| `fig axes`, `fig ax(row, col)` | All the figure's axes; the one at a grid position |
| `suptitle(s, opts)` | A title above all the subplots |
| `savefig(path, opts)` | Save; the extension picks the format, `.png`, `.svg`, `.pdf` or `.html` (an [interactive page](output.md#interactive-web-pages-and-svg)). `opts`: `dpi`, to save at another resolution than the figure's (`#{dpi: 200}` for print; a PDF is vector graphics and has none); `interactive` (`.svg`: tooltips and legend toggles); `title` (`.html`). |
| `toPng(dpi)`, `toSvg(opts)`, `toPdf` | The figure as a PNG file's bytes, as SVG text or as a PDF file's bytes, e.g. to return from a web handler. `toSvg` takes the dpi or `#{dpi:, interactive:}`. |
| `toHtml(opts)` | The figure as an interactive web page (a String). `opts`: `dpi`, `interactive` (`false`: static), `title`. `Plot toHtml` is the current figure's. |
| `drawPdf(page, x, y, width)` | Draw the figure on a clay-pdf page with its top-left corner at (x, y), in points, scaled to `width` (default: its size at 72 points an inch); returns the height it takes. See [PDF](output.md#pdf). |
| `toCanvas(dpi)` | The figure drawn on a clay-image `Canvas`, to draw more on it, or `toImage` for an `Image` |
| `show` | Save to a temporary PNG and open it in the system's image viewer. `Plot show` then starts a fresh figure. Returns the file's path. |
| `Plot close`, `Plot clf` | Forget the current figure; clear its axes |
| `Plot rc` | The default settings, a Dict of dotted names: `figure.figsize`, `figure.dpi`, `font.size`, `axes.titlesize`, `axes.labelsize`, `xtick.labelsize`, `ytick.labelsize`, `legend.fontsize`, `lines.linewidth`, `lines.markersize`, `axes.linewidth`, `axes.grid`, `axes.xmargin`, `axes.ymargin`, `grid.color`, `grid.linewidth`, `grid.alpha`, `image.cmap` |

Layout is automatic: each axes gets the room its tick labels,
axis labels, title and colour bar need, and subplots in one column or row line up.

## Format strings

A format string is any of a colour, a marker and a line style, in any order: `"r"`, `"o"`
(markers only), `"g^-"`, `"k--"`, `"b.:"`, `"C1--"`.

- Colours: `b` `g` `r` `c` `m` `y` `k` `w`, and `C0` to `C9`, the colour cycle's
- Markers: `.` `,` `o` `s` `^` `v` `<` `>` `D` `d` `p` `h` `*` `+` `x` `|` `_`
- Lines: `-` solid, `--` dashed, `:` dotted, `-.` dash-dot (and `"none"` as a `linestyle`)

## Colours and colormaps

A colour is any of `"#1f77b4"`, `"#abc"`, the one-letter colours, `"C0"` to `"C9"` (the
default cycle, tab10), `"tab:blue"` and the other tab10 names, common CSS names
(`"steelblue"`, `"crimson"`, ...), a gray level as a string (`"0.75"`), or `[r, g, b]` in 0..1.
Lines, bars and fills without a colour take the next one in the cycle.

Colormaps: `viridis` (the default), `plasma`, `inferno`, `magma`, `cividis`, `gray`, `binary`,
`Greys`, `Blues`, `Reds`, `Greens`, `coolwarm`, `RdBu`; add `_r` to reverse one
(`"gray_r"`). `PlotColor colormap("viridis", 0.3)` gives the `[r, g, b]` at a point, and
`PlotColor hex(spec)` turns any colour into `"#rrggbb"`.

## Limitations

- Polar axes start their radius at 0 and have no log radius or twin axes; `quiver` points
  arrows by their data units.
- Math text is a subset of TeX: no stacked fractions, roots or matrices, and one font.
  PNG and SVG lack a few symbols (≠ ≈ ∂ ∇ √ ∫ → and others), drawn as `!=`, `~`, `d`...; PDF
  draws them, and Greek, in its Symbol font.
- Text is DejaVu Sans only (Helvetica in PDF), in one weight (`fontweight` applies to SVG and PDF alone). SVG asks the
  viewer for DejaVu Sans and the layout measures text with it; a viewer without the font uses
  another sans-serif, which may sit a little closer or further than intended.
- In SVG, images are embedded as base64 PNG, about a third larger than the PNG itself (a
  128 x 400 spectrogram is about 200 KB).
- Interactive output gives tooltips for lines, points, bars, pie wedges and heatmaps only, and
  none on polar axes; there is no zoom or pan.
- Dates go on the x axis only. No symlog scales or 3-D yet. Log axes label only powers of ten (and 1, 2, 5 when less than two decades show).
