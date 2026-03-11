## Overview 

This repository contains the explanation and code necessary for simulating the evolution of [L-system](https://en.wikipedia.org/wiki/L-system) fractals through a parallel hill climbing method as a means of understanding tree growth. A simulation world has been developed for the fractals that attempts to mimic the 
effects of gravity, overgrowth, and light, with variables that can be modified for desired effects. 

## Installation
The code given here only requires the donwload of [Python](https://www.python.org/downloads/), as all utilizied libraries should be already be installed. 

## Determining a Simulation

Due to their similarity with real biological plants, L-systems can often provide a realistic means of modeling plant growth with the correct parameters, as both rely on the same means of random direction branching. Such a process then begs the question–can fractals be evolved? To do so, the virtual environment of growth would need to be tailored in a way that more accurately reflects natural processes. The following changes to the simulation environment were therefore made:

1. Gravity.
	In the real world, trees are not able to grow horizontally for large amounts of space, as the force exerted by gravity exerts a torque that creates bending and breaking. In simulation, this can be accomplished via two different ways: creating a light gradient that encourages growth in the up direction, or a bending force that can actively limit growth in the horizontal direction. The second method was chosen with a changeable parameter to more accurately portray the real world and provide a means of tweaking its effects. 
	
2. Growth limitation.
While L-systems are generated with a simple pattern that can continue forever, true trees are limited in growth by seasonal conditions, as well as resource management. In this simulation, growth occurs in “seasons” dictated by the amount of light that trees are able to absorb from the sun, represented by a constant value overhead the simulation. The shading created by higher branches also limits the possible growth done by a branch, so that it likely terminates more quickly. When a branch does terminate, it adds a leaf, represented by a dot, to the simulation, which is able to absorb the present as a means for capturing resources. Crowing also decreases the relative amount of branches that can be grown in a certain area, as true trees are discouraged from overgrowth in a small area, as it decreases fitness.

3. The ground.
	True L-systems are able to grow in any direction, but trees are limited by the ground, as it presents a means for their branches to be destroyed or trampled. Therefore, a constraint was added to the bottom of the simulation, preventing trees from simply growing through or along the ground. 


## Creating a genetic algorithm

While our L-systems early in the quarter were drawn from a simple set of rules, trees do not follow a simple set of angle and length dictations–their growth is truly random. However, the simulated L-systems still need to be modeled off some sort of base algorithm. Therefore, weights were assigned to different L-system structures as a means of creating a random pattern of growth.   
Both central trunks, as well as branches, have weights for each of the following L-system choices for a given iteration, found in the TRUNK CHOICES AND BRANCH CHOICES SECTION.  
	Trunks are the main growth system of the tree, creating branches as they propagate outwards. However, branches are not able to create trunks, as trunks represent the main vertical means of growing the tree. This process was created due to the fact that growth of only branches favored a diagonal structure of equal “density” that continued to propagate without limit. Both branches and trunks require equal energy to grow from photosynthesis. 
	When the tree has resources to grow during a season, each branch that extends could come from any of the above possible L-system possibilities. After the tree runs out of resources and is done growing for a season, leaves are placed on the edge of its branches. Initially, they were placed every time there was a ] bracket, but this led to leaf addition in areas that did not even exist anymore. Therefore, new leaves must be added every iteration of growth to the ends of branches that have finished growing. Only these leaves are able to absorb the energy present within the simulation to be used for growth during the next iteration. 

## Determining Fitness

As with any evolutionary system, a fitness system is required in order to score trees against each other and move up on the landscape of effective existence. The fitness developed for these L-systems is the following:

<img width="537" height="73" alt="Screenshot 2026-03-11 at 3 23 26 PM" src="https://github.com/user-attachments/assets/11b92d1b-3c66-4a25-9bb0-c3d25181d7e3" />

   S represents the amount of seasons in which the tree has evolved. The gain of the tree represents the amount of total light that is harvested by each leaf of the tree, summed to a total. The maintenance is the total amount of trunks, branches, and leaves that are present in the tree, as they require sustenance each season and subtract a baseline value from the total amount of initial energy harvested. Penalties also exist for qualities of trees that limit their effectiveness to exist. These include the length required to reach the end of a branch, as in the real world this limits the amount of nutrients that can travel to it for growth. This also includes the amount of torque force explained above, as well as the crowding value that discourages overgrowth in a small area. 

## Creating Mutations
   For each generation of trees, random mutations occur within their genotypes that affect fitness. These mutations occur in three different areas:

1. The angle measurement between branches can be modified a small amount, about 2 degrees in either direction
2. The length of segments can be changed in either direction, about 30% of the original
3. Noise can be added to both the trunk weights or the branch weights to change the amount slightly to which each pattern is chosen. These are then normalized back to 1 after the changes are made

These mutations affect the genotype of the child, giving it a slightly different fitness that may be better or worse than its parent. Parallel hill climber, as utilized in class, compares the fitness of a parent and child, preserving the individual with higher fitness.
    

