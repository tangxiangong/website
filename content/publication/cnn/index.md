---
title: "Classification of stochastic processes by convolutional neural networks"
authors:
- Eman A AL-hada
- admin
- Weihua Deng
# author_notes:
# - "Equal contribution"
# - "Equal contribution"
date: "2022-06-24T00:00:00Z"
doi: "10.1088/1751-8121/ac73c5"

# Schedule page publish date (NOT publication's date).
# publishDate: "2022-06-24T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "Journal of Physics A: Mathematical and Theoretical, **55** 274006"
publication_short: "J. Phys. A: Math. Theor."

abstract: Stochastic processes (SPs) appear in a wide field, such as ecology, biology, chemistry, and computer science. In transport dynamics, deviations from Brownian motion leading to anomalous diffusion (AnDi) are found, including transport mechanisms, cellular organization, signaling, and more. For various reasons, identifying AnDi is still challenging; for example, (i) a system can have different physical processes running simultaneously, (ii) the analysis of the mean-squared displacements (MSDs) of the diffusing particles is used to distinguish between normal diffusion and AnDi. However, MSD calculations are not very informative because different models can yield curves with the same scaling exponent. Recently, proposals have suggested several new approaches. The majority of these are based on the machine learning (ML) revolution. This paper is based on ML algorithms known as the convolutional neural network to classify SPs. To do this, we generated the dataset from published paper codes for 12 SPs. We use a pre-trained model, the ResNet-50, to automatically classify the dataset. Accuracy of 99% has been achieved by running the ResNet-50 model on the dataset. We also show the comparison of the Resnet18 and GoogleNet models with the ResNet-50 model. The ResNet-50 model outperforms these models in terms of classification accuracy.
# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags: []
# - Source Themes
featured: false

# links:
# - name: ""
#   url: ""
# url_pdf: ""
url_code: 'https://github.com/tangxiangong/ClassTop'
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