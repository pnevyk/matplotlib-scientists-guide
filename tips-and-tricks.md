# Tips and tricks

This section kind of violates the statement that this guide is not a reference of how to do things in Matplotlib.
Nevertheless, below are few examples of how to do (neat) things in Matplotlib.

### Artificial legend handles

Problem: *Set arbitrary styles of legend items different from actual appearance of points in axes.*

```python
from matplotlib.lines import Line2D

# scatter plot of almost transparent small blue circles
ax.plot(x, y, color='blue', alpha=0.25, marker='o', markersize=1, linewidth=0, markeredgewidth=0)

# create artificial handle of non-transparent bigger circles
handle = Line2D([0], [0], color='blue', marker='o', markersize=4, linewidth=0, markeredgewidth=0)

# make legend
ax.legend([handle], ['Blue circles'])
```

### Colorbar fixed to axes

Problem: *Place colorbar right next to the axes and make it to have the same size.*

```python
from mpl_toolkits.axes_grid1 import make_axes_locatable

im = ax.imshow(matrix)

divider = make_axes_locatable(ax)
cax = divider.append_axes('right', size='5%', pad=0.2)
fig.colorbar(im, ax=ax, cax=cax)
```

### No axes border and ticks

Problem: *Hide border of axes and axis ticks.*

```python
ax.axis('off')  # border
ax.xaxis.set_visible(False)  # x axis
ax.yaxis.set_visible(False)  # y axis
```
