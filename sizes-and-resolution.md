# Setting figure sizes and resolution

You probably know how to set the size of a figure. However, if you are not careful, the figure does not fit its place
and it needs to be somehow scaled (by tex, Jupyter notebook, whatever). In that case, the font size, width of lines,
etc. look different in different figures. If you have all figures the same size, then you are fine, but that is usually
not the case. So the question is, how to create a figure with desired aspect ratio which has exactly the same styles as
other ones.

First, note that `figsize` of a figure is its size in inches, in a metaphore, the physical size of your paper you want
to draw on. The goal is to set this size to be exactly the same as the size of its destination. You can get the width in
your LaTeX document by `\showthe` command with e.g. `\textwidth` or `\columnwidth` (depends if you use columnar layout
or not) as follows:

```tex
\documentclass{article}

\begin{document}
  \showthe\textwidth
\end{document}
```

And the output (that we are interested in) should look similar to this:

```
> 345.0pt.
l.4   \showthe\textwidth
```

The actual value depends on your layout (margins, etc.).

Now we need to convert points into inches. There are these rules: `1pt = 1/72.27in` and `1px = 1/96in`. Let us create an
utility function which accepts width as the fraction to the maximum width, and height as the fraction to the figure's
height.

```python
from math import sqrt

MAX_WIDTH = 345 / 72.27  # pt -> inches, change 345 appropriately to your use case
GOLDEN_RATIO = 2 / (1 + sqrt(5))  # 1 / phi

def figsize(width=1, height=GOLDEN_RATIO):
    '''
    Return proper figure size with desired width and aspect ratio.

    Parameters
    ----------
    width : float [width > 0, width <= 1]
        Width as fraction to the maximum available width.

    height : float
        Height as the fraction to the figure width.

    Returns
    -------
    size : (float, float)
        Figure size in inches.

    Examples
    --------
    >>> import matplotlib.pyplot as plt
    >>> fig = plt.figure(figsize=figsize(0.5, 0.5))
    '''

    figure_width = width * MAX_WIDTH
    figure_height = height * figure_width

    return (figure_width, figure_height)
```

When we already have proper-sized paper, we need a suffiently thin brush to make our drawings look good. In other words,
we need to set DPI (dots per inch). Minimal recommended value for quality figures is 300.

```python
fig.savefig('image.pdf', dpi=300)
# or
plt.rcParams({'figure.dpi': 300})
fig.savefig('image.pdf')
```

At the end, all figures you produce for one particular document should look the same.

## See further

* [SciPy Cookbook](http://scipy-cookbook.readthedocs.io/items/Matplotlib_LaTeX_Examples.html)
