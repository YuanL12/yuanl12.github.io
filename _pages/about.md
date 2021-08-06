---
permalink: /
title: "General Information about me"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

# About me
Yuan Luo is a Master student in the [Committee on Computational and Applied Mathematics](https://cam.uchicago.edu/) at the University of Chicago. He is interested in topological data analysis (TDA), scientific computation and machine learning.


## TDA Packages
Topological data analysis (TDA) is new applied mathematics area that attracts a lot of scientists. There are many packages useful online for you to perform computation. I will list some of them below with their installation recommendation:

Frist I recommend use python with version 3.7
`conda create -n bats python=3.7`

- **[BATS.py](https://bnels.github.io/BATS.py/#/installation)** 
(This is the package that I spent a lot of time on and feel free to contact me with questions!)
Linux OS is recommended.
```
conda install numpy matplotlib
git clone --recursive git@github.com:bnels/BATS.py.git
cd BATS.py
python setup.py install
```

- **Gudhi**
```
pip install gudhi
```

- **dionysus**
Install **cmake** and **boost** first.
```
pip install dionysus
```

- **Ripser**
```
pip install Cython
pip install Ripser
```

- **TopologyLayer**
It will be slow on some large datasets. Most functions are/will be implemented in [BATS.py](https://bnels.github.io/BATS.py/#/installation).
```
conda install pytorch=1.1 -c pytorch
pip install git+https://github.com/bruel-gabrielsson/TopologyLayer.git
```
