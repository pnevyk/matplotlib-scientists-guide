# Styling

Although the default style of Matplotlib does not look so bad, there is certainly room for improvement. Before you start
diving into the configuration, I recommend to set one of predefined styles which you like and later only tweak it to
your absolute satisfaction.

You can get the list of available styles via `plt.style.available` array. There are many of them, if you do not have a
special requirement, I recommend to look on `bmh`, `ggplot` and `seaborn`. Then the style of your choice is set simply
as follows:

```python
plt.style.use('bmh')
```

If you are not fully satisfied, you can change plenty of style options:

```python
params = {
    'font.family': 'lmodern'  # set the same font as you use in your document
    'font.size': '11'  # set the font size to be reasonably proportional to the font size of your document
    'lines.linewidth': 1,  # in pt
    'axes.facecolor': '#ffffff',
}

plt.rcParams.update(params)  # rcParams is just a dictionary with the configuration
```

If you set size of your figures properly (as described in [Setting figure sizes and
resolution](sizes-and-resolution.md)), all appearance settings will look the same in all your figures (because they will
not be scaled).

## See further

* [Documentation](https://matplotlib.org/users/customizing.html)
