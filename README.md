# SBI JOSS paper

## PDF Preview

The paper can be compiled at https://whedon.theoj.org, providing the repository link:
```
https://github.com/mackelab/sbi_joss.git
```


## Author instructions

> Begin your paper with a summary of the high-level functionality of your software for a non-specialist reader. Avoid jargon in this section.

JOSS welcomes submissions from broadly diverse research areas. For this reason, we require that authors include in the paper some sentences that explain the software functionality and domain of use to a non-specialist reader. We also require that authors explain the research applications of the software. The paper should be between 250-1000 words.

Your paper should include:

- A list of the authors of the software and their affiliations, using the correct format (see the example below).
- A summary describing the high-level functionality and purpose of the software for a diverse, non-specialist audience.
- A clear Statement of Need that illustrates the research purpose of the software.
- A list of key references, including to other software addressing related needs.
- Mention (if applicable) a representative set of past or ongoing research projects using the software and recent scholarly publications enabled by it.
- Acknowledgement of any financial support.

As this short list shows, JOSS papers are only expected to contain a limited set of metadata (see example below), a Statement of Need, Summary, Acknowledgements, and References sections. You can look at an example accepted paper. Given this format, a “full length” paper is not permitted, and software documentation such as API (Application Programming Interface) functionality should not be in the paper and instead should be outlined in the software documentation.

> Your paper will be reviewed by two or more reviewers in a public GitHub issue. Take a look at the review checklist and review criteria to better understand how your submission will be reviewed. https://joss.readthedocs.io/en/latest/review_criteria.html


## Formatting

### Citations

Citations to entries in paper.bib should be in
[rMarkdown](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html)
format.

For a quick reference, the following citation commands can be used:
- `@author:2001`  ->  "Author et al. (2001)"
- `[@author:2001]` -> "(Author et al., 2001)"
- `[@author1:2001; @author2:2001]` -> "(Author1 et al., 2001; Author2 et al., 2002)"

If you want to cite a software repository URL (e.g. something on GitHub without a preferred
citation) then you can do it with an entry like this:

```bibtex
@misc{fidgit,
  author = {​A. Smith},
  title = {Fidgit: An ungodly union of GitHub and Figshare},
  year = {2020},
  publisher = {​GitHub},
  journal = {​GitHub repository},
  url = {​https://github.com/arfon/fidgit}
}
```

### Mathematics

Single dollars (`$`) are required for inline mathematics e.g. `$f(x) = e^{\pi/x}$`

Double dollars make self-standing equations:

```
$$\Theta(x) = \left\{\begin{array}{l}
0\textrm{ if } x < 0\cr
1\textrm{ else}
\end{array}\right.$$
```

You can also use plain LaTeX for equations
```
\begin{equation}\label{eq:fourier}
\hat f(\omega) = \int_{-\infty}^{\infty} f(x) e^{i\omega x} dx
\end{equation}
```
and refer to ``\autoref{eq:fourier}`` from text.


### Figures

Figures can be included like this: `![Caption for example figure.\label{fig:example}](figure.png)` and referenced from text using `\autoref{fig:example}`.


### Code

Fenced code blocks are rendered with syntax highlighting:
```python
for n in range(10):
    yield f(n)
```


## Conversion to TeX
