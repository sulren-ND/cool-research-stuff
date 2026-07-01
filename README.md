# cool-research-stuff
These are just notes from earlier that I'm going to paste in here:

Notes - GENETIS/JPL antenna GA paper
What the paper is
JPL progress report from Aug 2023, written w/ Ohio State GENETIS group
using genetic algorithms (GA) to evolve 3D antenna shapes instead of hand-designing them
goal long term: antennas optimized for actual science sensitivity, not just shape
quick GA refresher 
GA = mimics evolution to solve a problem
start w/ random candidate solutions ("individuals")
score each one w/ a fitness function (here: how close the shape is to a target)
best scoring ones become "parents," mix + mutate their traits
repeat over generations, population gets better over time
"genes" here = shape type (cuboid/sphere/cylinder/cone), dimensions, position, what it's connected to
how their algorithm builds shapes
shapes built like legos - base shape + stuff attached to its sides
represented as a tree structure
built/rendered in Blender to actually compare to target
merging shapes into one mesh = biggest computational cost
fitness functions they tried
Hausdorff distance - worst point mismatch
average min distance - same idea but averaged not worst-case
volume matching - compares overlap vs non-overlap volume
linear combo - blend of hausdorff + avg min distance
direct dictionary comparison - compares genes directly to known target (only works if you already know the target)
results
bicone + dipole (simple shapes, 2 components) - worked well, multiple fitness fns succeeded
volume matching failed basically every time - got stuck on stuff like two stacked spheres for the dipole
log-periodic antenna (14 components) - way harder, none of the geometric fitness fns converged, had to build the direct dictionary comparison fn specifically, took ~21,000 generations
GA runs are super stochastic - same settings can converge in 50 gens or 400+ gens
what's next per the paper
integrate XFdtd (EM simulation) so fitness = actual antenna performance, not just shape match
more primitive shapes (pyramids, toruses, helices)
allow more than one shape per side (currently capped at 1)
mentions neural nets / particle swarms as possible future speedups
surrogate model angle
biggest bottleneck right now is Blender modeling, but once XFdtd gets added that's going to be way slower per individual - that's really the thing a surrogate should target, not Blender
idea: train a model to predict gain pattern / sensitivity directly from an individual's genes instead of running full XFdtd every time
since individuals are literally trees of connected shapes, a graph neural network might fit better than a flat vector input - can handle different numbers of shapes/branches naturally
surrogate will be unreliable for weird/novel shapes from mutation or injection - might be worth an ensemble or GP model that also gives a confidence score, fall back to real sim when unsure
population keeps changing each generation so a surrogate trained once will go stale - probably needs periodic retraining / active learning loop where you keep sampling real sim results to refresh it
questions to bring up
why did volume matching fail every single time - formula issue or is volume just a bad similarity measure here
log periodic took 21k generations and a custom fitness fn - what does that mean for scaling to even harder shapes
given how random GA runs are, how do they decide a result is actually good vs just lucky
once real antenna performance is the goal, how do they plan to balance that against cost/size/weight constraints
what breaks if they remove the one-shape-per-side limit
where exactly should the surrogate go - replacing Blender or replacing the future XFdtd step
how do they plan to keep the surrogate from going stale as the population evolves
any interest in using the existing 250-individuals-per-generation data as a starting training set for the surrogate


Chatgpt’d some things for clarification:

XFdtd
It's a commercial electromagnetic simulation software made by a company called Remcom. The name breaks down as:
FDTD = Finite-Difference Time-Domain — a numerical method for solving how electromagnetic waves behave in and around structures
X = just Remcom's branding
What It Actually Does
You give it a 3D model of an antenna, and it simulates how radio waves interact with it — how well it transmits and receives in different directions, at different frequencies, how much energy is wasted as heat, etc. It essentially answers "does this antenna actually work well?" from a physics standpoint.
It does this by breaking space up into a tiny 3D grid and simulating how electromagnetic fields evolve through that grid over time, step by step. Accurate, but very computationally heavy.


https://dr.ascsn.net/landing.html
https://arxiv.org/pdf/2203.05284
https://arxiv.org/abs/2406.04279 

Frib summer school- jupyter notebooks
Pablo’s github
Notebook lm

https://github.com/ascsn/2023-FRIB-TA-Summer-School 
