# How to use Random Forest Importance Feature to Detect Differences between MD Simulations. 

![](main.png)

# Table of Contents

# Introduction

Looking through esembles of molecular dynamics (MD) trajectories can be a daunting task.
Here, I show how to use the Random Forest (RF) algorithm to quickly located differences between seperate ensembles of MD simulations. 

## Example Case

Here we will be looking at the malarial aspartyl protease Plasmepsin II (PDBid: 1SME) where one simulation has an inhibitor bound and the other is inhibitor free.
By training the RF classifier between two states, in this case using inhibitor bound and unbound snap shots from MD simulations, you can use the feature importance to provide insight about the protein conformation.
The features in this can can almost be anything from water positions, dihedral angles, and Cα positions.
In this example the Cα positions will be used. 
The power of using the RF algorithm to to find the conformational differences is to reduce the amount of time spent by a computational chemist rigorously groom MD simulations by eye, and it has the potential to detect allosteric conformational changes that one would think to look at. 

# Getting Started 

The first thing you need is to do is prepare the MD trajectories you are going to analyze. 
```
1.) The trajecories need to be aligned, in this case the two ensmebles were aligned by the protein backbone atoms (C, Cα, N, and O).
2.) For effeciency remove the water and ions in the aligned trajecoteries, unless you are using water as the feature of interest. 
3.) Make a PDB file with connectivity information to view the trjectories. 
4.) Make a PDB file of the selection you are using to detect feature importance, or one you can use to color by feature importance. 
```

For this process I suggest using [MDAnalysis](https://www.mdanalysis.org/).

In this example I have provide examples of the following inputs. 
```
1.) apo.dcd, ligand unbound trajectories 
2.) holo.dcd, ligand bound trajectories
3.) check.pdb, PDB used to view the trajecotry files
4.) pdb_for_coloring.pdb, PDB used to color by feature importance 
```
Note: Sometimes the check.pdb and pdb_for_color.pdb can be the same and depending on the scenerio that an be different.
