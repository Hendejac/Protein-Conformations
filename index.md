# How to use Random Forest Importance Feature to Detect Differences between MD Simulations. 

![](main.png)

# Table of Contents

# Purpose

How to find the difference between two molecular dynamics (MD) simulations quickly using the random forest (RF) algorithm.

## Example 

Here we will be looking at the malarial aspartyl protease Plasmepsin II where one simulation has an inhibitor bound and the other is inhibitor free.
By training the RF classifier between two states, in this case inhibitor bound and unbound snap shots from MD simulations, you can use the feature importance to provide insight about the protein conformation. 
The power of this method helps detect conformational difference in allosteric sites and quickly guides ones eye to investigate the MD simulations.

