# Contributing

## Develop

```sh
clay bricks install                # fetches clay-image and clay-pdf into bricks/
clay tests/test_plot.clay          # a brick can import itself by name
clay examples/gallery.clay         # writes example figures to examples/out/
clay examples/ml.clay
clay examples/dashboard.clay
clay examples/statistics.clay
clay examples/dates_density.clay
clay examples/animation.clay
clay examples/layout.clay
clay examples/fields.clay
clay examples/interactive.clay
```

`examples/fashion_mnist.clay` also needs clay-ann; its header says how to run it.

The code is in `src/`: `main.clay` (`Plot`, its functions and `rc`),
`figure.clay` (`PlotFigure`: layout and saving), `axes.clay` (`PlotAxes`: artists, scales,
ticks, legend, drawing), `ticks.clay` (`PlotTicks`: ticks, number formats, logarithms),
`color.clay` (`PlotColor`), `ml.clay` (`PlotML`), `live.clay` (`PlotLive`), `polar.clay`
(`PlotPolarAxes`), `mathtext.clay` (`PlotMath`: `$...$` in text), `stats.clay`, `contour.clay`,
`dates.clay` and `anim.clay`, and the backends
`svg.clay` (`PlotSvg`), `png.clay` (`PlotPng`, on clay-image's `Canvas`), `pdf.clay`
(`PlotPdf`, on a clay-pdf page) and `term.clay` (`PlotTerm`, text for terminals). Axes
draw through a handful of primitives (`line`, `polyline`, `polygon`, `rect`, `circle`, `text`,
`image`, `clip`, `measure`) listed at the top of `svg.clay`, so a new backend implements just
those.

To work on clay-image at the same time, replace `bricks/image` with a link to your checkout
(`mklink /J bricks\image ..\clay-image` on Windows, `ln -s ../../clay-image bricks/image`
elsewhere).

`.github/workflows/test.yml` runs the tests on Linux, macOS and Windows for every push and
pull request on GitHub.
