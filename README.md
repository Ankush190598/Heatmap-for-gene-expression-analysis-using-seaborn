# Description
## Heatmap for gene expression using seaborn
Heat maps represent two-dimensional tables of numbers as shades of colors. This is a popular plotting technique in biology, used to depict gene expression and other multivariate data. The dense and intuitive display makes heat maps well-suited for presentation of high-throughput data. Hundreds of rows and columns can be displayed on a screen. Heat maps rely fundamentally on color encoding and on meaningful reordering of the rows and columns.

Seaborn is a Python data visualization library based on [matplotlib](https://matplotlib.org/). It provides a high-level interface for drawing attractive and informative statistical graphics.

Seaborn.clustermap
seaborn.clustermap(data, *, pivot_kws=None, method='average', metric='euclidean', z_score=None, standard_scale=None, figsize=(10, 10), cbar_kws=None, row_cluster=True, col_cluster=True, row_linkage=None, col_linkage=None, row_colors=None, col_colors=None, mask=None, dendrogram_ratio=0.2, colors_ratio=0.03, cbar_pos=(0.02, 0.8, 0.05, 0.18), tree_kws=None, **kwargs)

seaborn.heatmap
seaborn.heatmap(data, *, vmin=None, vmax=None, cmap=None, center=None, robust=False, annot=None, fmt='.2g', annot_kws=None, linewidths=0, linecolor='white', cbar=True, cbar_kws=None, cbar_ax=None, square=False, xticklabels='auto', yticklabels='auto', mask=None, ax=None, **kwargs)


# Import packages
```bash
import pandas as pd
import seaborn as sns
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

```
# Upload gene expression data
```bash
df = pd.read_csv("hm_cot.csv", sep='\t')
df.head()
```
## Will set gene name as index
```bash
df = df.set_index(df.columns[0])
df.head()
```



# Plot a clustered heatmap for gene expression
Will use seaborn package
```bash
hmap = sns.clustermap(data=df, figsize=(10,10))
```
If want to plot heatmap without hierarchical clustering and set color box at certain position
```bash
hmap = sns.clustermap(data=df, figsize=(10,10), row_cluster=False, col_cluster=False, cbar_pos=(0, .2, .03, .4))
```
if want to change  clustering only in sample or in gene
```bash
hmap = sns.clustermap(data=df, figsize=(10,10), row_cluster=False, col_cluster=True, cbar_pos=(0, .2, .03, .4))
```

colormaps are available at https://matplotlib.org/3.1.0/tutorials/colors/colormaps.html
Here we can use YlGnBU/mako/RdYlGn/vlag
If you want to change the limit of the color map, you can use "vmin" and "vmax" 
```bash
hmap = sns.clustermap(data=df, figsize=(10,10), row_cluster=True, col_cluster=True, cmap='YlGnBu')
```

Z-score can be used to standardize value with mean 0 and var 1. Default Z-score is set to None and it applies to only heatmap with cluster. 
Here I standardize column with Z-score.
```bash
hmap = sns.clustermap(data=df, figsize=(10,10), row_cluster=True, col_cluster=True, cmap='YlGnBu', z_score=1)
```
Here I standardize row with Z-score.
```bash
hmap = sns.clustermap(data=df, figsize=(10,10), row_cluster=True, col_cluster=True, cmap='YlGnBu', z_score=0)

```
If you want to standardize the data within the column
```bash
hmap = sns.clustermap(data=df, figsize=(10,10), row_cluster=True, col_cluster=True, cmap='YlGnBu', z_score=0,standard_scale=1 )

```
If you want to use a different similarity metric:

```bash
hmap = sns.clustermap(data=df, metric = "correlation" )

```
