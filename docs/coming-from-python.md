# Coming from Python

[← Back to the README](../README.md)

clay-plot's API was inspired by Python's matplotlib, so if you've used it, most of what you
know carries over. clay-plot is an independent project, not affiliated with matplotlib. This
page puts common Python calls beside their clay-plot equivalents.

Keyword arguments become an options Dict at the end of the call, and tuples become Arrays.
Option names that have underscores in Python are camelCase here (`bbox_to_anchor` is
`bboxToAnchor`, `patch_artist` is `patchArtist`).

| Python | clay-plot |
|---|---|
| `import matplotlib.pyplot as plt` | `import("plot")`, then `Plot ...` (or `plt = Plot`) |
| `plt.plot(x, y, "r--", label="a", lw=2)` | `Plot plot(x, y, "r--", #{label: "a", lw: 2})` |
| `fig, ax = plt.subplots()` | `[fig, ax] = Plot subplots` |
| `fig, axs = plt.subplots(2, 3)` | `[fig, axs] = Plot subplots(2, 3)`, then `axs at(r) at(c)` |
| `plt.subplot(1, 2, 1)` | `Plot subplot(1, 2, 1)` |
| `plt.subplots(2, 2, sharex="col", sharey=True)` | `Plot subplots(2, 2, #{sharex: "col", sharey: true})` |
| `fig, axd = plt.subplot_mosaic(["AAB", "CCB"])` | `[fig, axd] = Plot subplotMosaic(["AAB", "CCB"])`, then `axd get("A")` |
| `plt.subplot2grid((3, 3), (0, 0), colspan=3)` | `Plot subplot2grid([3, 3], [0, 0], #{colspan: 3})` |
| `ax.legend(bbox_to_anchor=(1.02, 1), loc="upper left", ncol=2)` | `ax legend(#{bboxToAnchor: [1.02, 1], loc: "upper left", ncol: 2})` |
| `fig.legend(loc="outside right")` | `fig legend(#{loc: "outside right"})` or `Plot figlegend(...)` |
| `plt.ylabel(r"$\sigma^2$")` | `Plot ylabel("$\\sigma^2$")` (Clay strings escape `\` as `\\`) |
| `ax.set_title("t")`, `ax.set_xlabel("x")` | `ax title("t")`, `ax xlabel("x")` |
| `ax.set(xlim=(0, 1), title="t")` | `ax set(#{xlim: [0, 1], title: "t"})` |
| `plt.fill_between(x, y1, y2)` | `Plot fillBetween(x, y1, y2)` |
| `n, bins, patches = plt.hist(x, 20)` | `[n, bins, patches] = Plot hist(x, 20)` |
| `plt.pie(v, labels=l, autopct="%1.1f%%")` | `Plot pie(v, #{labels: l, autopct: "%1.1f%%"})` |
| `ax.bar_label(bars, fmt="{:,.0f}")` | `ax barLabel(bars, #{fmt: "{:,.0f}"})` |
| `plt.errorbar(x, y, yerr=e, fmt="o")` | `Plot errorbar(x, y, #{yerr: e, fmt: "o"})` |
| `plt.yscale("log")`, `plt.semilogy(x, y)` | `Plot yscale("log")`, `Plot semilogy(x, y)` |
| `plt.xticks(pos, labels, rotation=45)` | `Plot xticks(pos, labels, #{rotation: 45})` |
| `plt.text(0.5, 0.5, "s", transform=ax.transAxes)` | `Plot text(0.5, 0.5, "s", #{transform: "axes"})` |
| `ax.annotate("max", xy=(x, y), xytext=(tx, ty), arrowprops=dict(arrowstyle="->"))` | `ax annotate("max", [x, y], [tx, ty], #{arrowprops: #{arrowstyle: "->"}})` |
| `ax2 = ax.twinx()` | `ax2 = ax twinx` |
| `plt.boxplot([a, b], tick_labels=["a", "b"], patch_artist=True)` | `Plot boxplot([a, b], #{labels: ["a", "b"], patchArtist: true})` |
| `plt.violinplot([a, b], showmedians=True)` | `Plot violinplot([a, b], #{showmedians: true})` |
| `cs = plt.contour(X, Y, Z, 10, colors="k")`, `plt.clabel(cs)` | `cs = Plot contour(X, Y, Z, 10, #{colors: "k"})`, `Plot clabel(cs)` |
| `plt.contourf(X, Y, Z, cmap="RdBu")`, `plt.colorbar()` | `Plot contourf(X, Y, Z, #{cmap: "RdBu"})`, `Plot colorbar` |
| `plt.axvspan(x0, x1, alpha=0.3)`, `plt.axhspan(y0, y1)` | `Plot axvspan(x0, x1, #{alpha: 0.3})`, `Plot axhspan(y0, y1)` |
| `plt.hexbin(x, y, gridsize=40, bins="log")` | `Plot hexbin(x, y, #{gridsize: 40, bins: "log"})` |
| `h, xe, ye, im = plt.hist2d(x, y, 30)` | `[h, xe, ye, im] = Plot hist2d(x, y, 30)` |
| `plt.plot(pd.to_datetime(dates), y)` | `Plot plot(dates, y)`, with `Date`s or `"2024-03-15"` text |
| `ani = FuncAnimation(fig, update, frames=60, interval=50)`, `ani.save("a.gif")` | `anim = Plot animate(fig, 60, { \|i\| ... }, #{interval: 50})`, `anim save("a.gif")` |
| `ax.clear()`, `plt.cla()` | `ax clear`, `Plot cla` |
| `plt.fill(x, y)`, `plt.fill_betweenx(y, x1, x2)` | `Plot fill(x, y)`, `Plot fillBetweenx(y, x1, x2)` |
| `plt.pcolormesh(X, Y, C, cmap="RdBu")` | `Plot pcolormesh(X, Y, C, #{cmap: "RdBu"})` |
| `plt.quiver(X, Y, U, V, C)` | `Plot quiver(X, Y, U, V, C)` |
| `ax = plt.subplot(projection="polar")`, `plt.polar(t, r)` | `ax = Plot subplot(1, 1, 1, #{projection: "polar"})`, `Plot polar(t, r)` |
| `ax.set_theta_zero_location("N")`, `ax.set_theta_direction(-1)` | `ax setThetaZeroLocation("N")`, `ax setThetaDirection(-1)` |
| `plt.rcParams["font.size"] = 12` | `Plot rc set("font.size", 12)` |
| `plt.savefig("f.png", dpi=150)`, `plt.show()`, `plt.close()` | `Plot savefig("f.png", #{dpi: 150})`, `Plot show`, `Plot close` |

`Plot` keeps a current figure and axes: `Plot plot(...)` draws on
`Plot gca`, made when first needed. `Plot figure(#{figsize: [w, h], dpi: 100})` starts a new
one. You can also work with the objects directly: `fig = Plot figure`, `ax = Plot gca`, then
`ax plot(...)`, `fig savefig(...)`.

## Differences worth knowing

- Clay strings escape `\` as `\\`, so Python's raw string `r"$\sigma^2$"` is written
  `"$\\sigma^2$"`.
- `Plot rc` uses the same dotted setting names as matplotlib's `rcParams` (`figure.figsize`,
  `font.size`, ...). The [API reference](api.md#figures) lists the ones it has.
- `quiver` points arrows by their data units, as matplotlib's `angles="xy"` does.
- Layout is always automatic, much like matplotlib's tight layout; there is nothing to turn on.
- `hist2d` returns counts indexed `[x bin][y bin]`, as numpy does.
