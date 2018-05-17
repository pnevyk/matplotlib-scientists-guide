# File format

One important rule at the beginning: always use vector formats for your plots. What possibilities we have (among
others)?

* EPS - Often seen in tutorials, however, it has some considerable disadvantages. If using eps for a document which is
  intended to be compiled into pdf, then the tool (`pdftex`, `pdflatex`, `xelatex`) must first do a conversion and this
  is not without [problems](https://tex.stackexchange.com/questions/2092/which-figure-type-to-use-pdf-or-eps).
* SVG - Good vector format, but suitable for web pages and similar use cases.
* **PDF** - Portable and widely used binary format which supports vector graphics. Straightforward integration with PDF
  generating tools (such a surprise!). Good choice.
* **PGF** - A low-level language for describing vector graphics, well-supported in LaTeX. Although with complex figures,
  compilation can go slow, this can be a good option as it better integrates with LaTeX compilation (fonts, etc.). And
  subjectively, it feels more cleaner to include a graphics script than a binary file.

### PDF

Figure script:

```python
import matplotlib.pyplot as plt

plt.rcParams({'text.usetex': True, 'text.latex.unicode': True}) # optionally font of your document

fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)
ax.plot([1, 3, 1])
ax.set_xlabel(r'$x_i$')  # `r` prefix is used to preserve escape sequences to be processed by LaTeX itself
fig.savefig('image.pdf')
```

LaTeX source:

```tex
\documentclass{article}

\usepackage{graphicx}

\begin{document}
  \begin{figure}
    \includegraphics{image}
    \caption{Image}
  \end{figure}
\end{document}
```

#### See further

* [Documentation](https://matplotlib.org/users/usetex.html)

### PGF

Figure script:

```python
import matplotlib.pyplot as plt

# rcParams: pgf.texsystem defaults to 'xelatex', you might want to set it to 'luatex' or 'pdflatex'

fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)
ax.plot([1, 3, 1])
ax.set_xlabel(r'$x_i$')  # `r` prefix is used to preserve escape sequences to be processed by LaTeX itself
fig.savefig('image.pgf')
```

LaTeX source:

```tex
\documentclass{article}

\usepackage{pgf}

\begin{document}
  \begin{figure}
    \input{image.pgf}
    \caption{Image}
  \end{figure}
\end{document}
```

#### See further

* [Documentation](https://matplotlib.org/users/pgf.html)

## Notes

These basic templates work for basic usage. If you need something more advanced (like specific LaTeX packages), you need
to appropriately set `text.latex.preamble` or `pgf.preamble`, respectively.
