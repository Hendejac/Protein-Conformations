# How to use Random Forest Importance Feature to Detect Differences Between MD Simulations. 

![](main.png)

# Table of Contents

# Introduction

Looking through esembles of molecular dynamics (MD) trajectories can be a daunting task.
Here, I show how to use the Random Forest (RF) algorithm to quickly located differences between seperate ensembles of MD simulations. 

## Example Case

![](apo_holo.png)

Here we will be looking at the malarial aspartyl protease Plasmepsin II (PDBid: 1SME) where one simulation has an inhibitor bound and the other is inhibitor free.
By training the RF classifier between two states, in this case using inhibitor bound and unbound snap shots from MD simulations, you can use the feature importance to provide insight about the protein conformation.
The features in this can can almost be anything from water positions, dihedral angles, and Cα positions.
In this example the Cα positions will be used. 
The power of using the RF algorithm to to find the conformational differences is to reduce the amount of time spent by a computational chemist rigorously groom MD simulations by eye, and it has the potential to detect allosteric conformational changes that one would think to look at. 

# Getting Started 

The first thing you need is to do is prepare the MD trajectories you are going to analyze. 

- [x] The trajecories need to be aligned, in this case the two ensmebles were aligned by the protein backbone atoms (C, Cα, N, and O).
- [x] For effeciency remove the water and ions in the aligned trajecoteries, unless you are using water as the feature of interest. 
- [x] Make a PDB file with connectivity information to view the trjectories. 
- [x] Make a PDB file of the selection you are using to detect feature importance, or one you can use to color by feature importance. 

For this process I suggest using [MDAnalysis](https://www.mdanalysis.org/).

In this example I have provide examples of the following inputs. 

- [x] apo.dcd, ligand unbound trajectories 
- [x] holo.dcd, ligand bound trajectories
- [x] check.pdb, PDB used to view the trajecotry files
- [x] pdb_for_coloring.pdb, PDB used to color by feature importance 

Note: Sometimes the check.pdb and pdb_for_color.pdb can be the same and depending on the scenerio that an be different.

# Preparing the Dataset

Now that the MD trajectories have been prepared the you can move on to making the dataset. 
A full example of this using MDAnalysis can be seen in the jupyter notebook, 'confML_apo_holo.ipynb'.
In this case the dataset will be the X, Y, and Z positions of all the Cα atoms in each frame of the trajectories.
In the example case here, I first make a dataframe from the simulation without the inhibitor (apo) and then do the same for the inhibitor bound simulation (holo).
In these dataframes the rows are the snap shots from each simulation and the columns are the X, Y, and Z coordinates.

### Sample Apo Data 

|    |   0  |   1  |   2  |   3  | ... |   986| Label |
|---:|-----:|-----:|-----:|-----:|----:|-----:|------:| 
|  0 | 5.83 | 18.58|-17.02|  7.14| ... |-18.10|  apo  |
|  1 | 7.70 |	18.93|-16.13|	 8.16| ... |-18.49|  apo  |
| ...|  ... |  ... |  ... |  ... | ... |  ... |  ...  |
|1049| 3.89 |	20.00|-12.55|	 3.21| ... |-18.90|  apo	|
 
### Sample Holo data 

|    |   0  |   1  |   2  |   3  | ... |   986| Label |
|---:|-----:|-----:|-----:|-----:|----:|-----:|------:| 
|  0 | 12.65| 17.82|-15.83|  8.84| ... |-18.06|  holo |
|  1 | 10.38|	1754 |-14.45|	 6.83| ... |-19.07|  holo |
| ...|  ... |  ... |  ... |  ... | ... |  ... |  ...  |
|1599| 9.57 |	3.87 |-18.24|	 9.24| ... |-19.14|  holo	|
