---
title: 'TDA Packages'
date: 2021-09-04
permalink: /posts/2021/09/TDA-packages/
tags:
  - TDA
  - Python
---

Topological data analysis(TDA) is a new applied mathematics area that attracts a lot of scientists. There are many packages useful online for you to perform computation. I will list some of them below with their installation recommendation:

Frist, I recommend using python with version 3.7
`conda create -n bats python=3.7`

- **[BATS.py](https://bnels.github.io/BATS.py/#/installation)** 
(This is the package that I spent a lot of time on and feel free to contact me with questions!)
Linux OS is recommended and commands are listed below, but if you insist on Mac OS, then please follow this blog [How to run BATS in Mac.md](https://yuanl12.github.io/posts/2021/08/How-to-run-BATS-in-Mac/).
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
It will be slow on some large datasets. Most functions are/will be implemented by [BATS.py](https://bnels.github.io/BATS.py/#/installation).
```
conda install pytorch=1.1 -c pytorch
pip install git+https://github.com/bruel-gabrielsson/TopologyLayer.git
```

