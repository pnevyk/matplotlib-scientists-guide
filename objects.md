# "Object-oriented" Matplotlib

Matplotlib is built to support stateful procedural interface, useful for quick prototyping. However, if you are serious
about your figures' plotting, there is another way which is more flexible and less black-box-like.

### Figures

[Figure](https://matplotlib.org/api/_as_gen/matplotlib.figure.Figure.html) represents the whole canvas you are drawing
on. It can contain one or more axes - parts of the canvas from which the visualization is composed of.

```python
fig = plt.figure()  # the most straightforward how to create a figure
fig, ax = plt.subplots(nrows=2, ncols=2)  # create figure with defined axes grid
```

```python
fig.suptitle('Visualization')
```

```python
fig.savefig('image.pdf')
plt.close(fig)  # Matplotlib keeps references to all created figures,
                # closing them makes the generation less memory consuming
```

### Axes

[Axes](https://matplotlib.org/api/axes_api.html) represents a part of the canvas on which you are plotting.

```python
ax = fig.add_subplot(2, 2, 1)  # add the first subplot of 2x2 grid
ax = fig.add_axes((0.1, 0.1, 0.8, 0.8))  # add axes on the specific position and with certain size
ax = fig.gca()  # get current axes, if you need to cooperate with other libraries that use the procedural way
fig, axes = plt.subplots(nrows=2, ncols=2)  # create axes already with figure (axes is array of shape [2, 2])
```

```python
ax.plot(x, y)
ax.set_xlabel('x')
ax.set_ylabel('y')
```

## See further

* [Advanced plotting](https://python4astronomers.github.io/plotting/advanced.html) by python4astronomers
