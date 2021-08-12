---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* B.S. in Applied Mathematics, Xi'an Jiaotong-Liverpool University, 2016 - 2020
* Visiting Student, Michigan State University, 2018 - 2019
* M.S. in Computational and Applied Mathematics, University of Chicago, 2020 - 2022(expected)
<!-- * Ph.D in Version Control Theory, GitHub University, 2018 (expected)
 -->

<!-- Research experience
======
* Summer 2015: Research Assistant
  * Github University
  * Duties included: Tagging issues
  * Supervisor: Professor Git

* Fall 2015: Research Assistant
  * Github University
  * Duties included: Merging pull requests
  * Supervisor: Professor Hub -->
  
Skills
======
* Python
  * Pandas, Numpy and Pytorch  
* C++

Publications
======
  <ul>{% for post in site.publications %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Research Experience (unpublished)
======

* **[Cubical Homology and its application in robots’ motion planning](../files/undergraduate-thesis.pdf), July 2019 - May 2020**
  * researched homology group’s application in robots’ motion planning.
  * Utilizedcubicalhomologytocomputethenumberofworkingcyclesofnrobotsonsomesimplegraphsby writing algorithms in Python and found some relationships between graphs and discretized configuration space.

* **[Functions of Perturbed Matrices, Febrarury 2019 - April 2019](../files/perturbed-matrix.pdf)**
  * Estimated the norm of f(A) − f(B) in terms of the norm of A − B and proved its boundedness on
finite-dimensional spaces.

* **[Time Series Prediction of Sales by LSTM](../files/LSTM-time-seris.pdf), July 2018 - August 2018**
  * Combined ARIMA in time series with deep learning.
  * Predicted future phone cases sales via an LSTM model implemented in Python, whose hyper-parameters are optimized by grid search.
  * Utilized both standard deviation of sales and the parameters of autoregressive models as the fitting features to create hybrid models.
  * Evaluated the performance of hybrid models to select the models with the most effective prediction of future sales.

<!-- Talks
======
  <ul>{% for post in site.talks %}
    {% include archive-single-talk-cv.html %}
  {% endfor %}</ul>
  
Teaching
======
  <ul>{% for post in site.teaching %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Service and leadership
======
* Currently signed in to 43 different slack teams -->
