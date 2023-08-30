---
title: "A sharp $\\alpha$-robust $L1$ scheme on graded meshes for two-dimensional time tempered fractional Fokker-Planck equation"
authors:
- Can Wang
- Weihua Deng
- admin
# author_notes:
# - "Equal contribution"
# - "Equal contribution"
date: "2023-08-23T00:00:00Z"
# doi: "10.1088/1751-8121/ac73c5"

# Schedule page publish date (NOT publication's date).
# publishDate: "2022-06-24T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "International Journal of Numerical Analysis and Modeling (**Accepted**)"
publication_short: "Int. J. Numer. Anal. Mod. (**Accepted**)"

abstract: In this paper, we are concerned with the numerical solution for the two-dimensional time fractional Fokker-Planck equation with the tempered fractional derivative of order $\alpha$. Although some of its variants are considered in many recent numerical analysis works, there are still some significant differences. Here we first provide the regularity estimates of the solution. Then a modified $L1$ scheme inspired by the middle rectangle quadrature formula on graded meshes is employed to compensate for the singularity of the solution at $t\to 0+$, while the five-point difference scheme is used in space. Stability and convergence are proved in the sense of $L^{\infty}$ norm, getting a sharp error estimate $O(τ^{\min\\{2−\alpha,r\alpha\\}})$ on graded meshes. Furthermore, the constant multipliers in the analysis do not blow up as the order of Caputo fractional derivative α approaches the classical value of 1. Finally, we perform the numerical experiments to verify the effectiveness and convergence orders of the presented schemes.
# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags: []
# - Source Themes
featured: false

# links:
# - name: ""
#   url: ""
# url_pdf: ""
# url_code: 'https://github.com/tangxiangong/ClassTop'
# url_dataset: ''
# url_poster: ''
# url_project: ''
# url_slides: ''
# url_source: ''
# url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# image:
#   caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/jdD8gXaTZsc)'
#   focal_point: ""
#   preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []
draft: false
# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
#  slides: example
---