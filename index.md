# How to use Random Forest Importance Feature to Detect Differences between MD Simulations. 

![](main.png)

# Table of Contents

# Purpose

Looking through esembles of molecular dynamics (MD) trajectories can be a daunting task.
Here, I show how to use the Random Forest (RF) algorithm to quickly located difference between different ensembles of MD simulations. 

## Example Case

Here we will be looking at the malarial aspartyl protease Plasmepsin II (PDBid: 1SME) where one simulation has an inhibitor bound and the other is inhibitor free.
By training the RF classifier between two states, in this case using inhibitor bound and unbound snap shots from MD simulations, you can use the feature importance to provide insight about the protein conformation.
The features in this can can almost be anything from water positions, dihedral angles, and Cα positions.
In this example the Cα positions will be used. 
The power of using the RF algorithm to to find the conformational differences is to reduce the amount of time spent by a computational chemist rigorously groom MD simulations by eye, and it has the potential to detect allosteric conformational changes that one would think to look at. 


