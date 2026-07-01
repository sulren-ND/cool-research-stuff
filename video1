dimensionality reduction- quick notes

the problem: describing a nucleus (or any complex system) fully requires a huge number of variables
 could be thousands
 
 - this is "high-dimensional" and expensive to compute.

the fix: even though the full space is huge, the actual solutions don't use all of it, they trace out a much smaller, simpler shape called the solution manifold

- dimensionality reduction = finding and using that smaller shape instead of the full space.
  
result: same (or nearly same) accuracy, way less computation


degrees of freedom- what it means

a "degree of freedom" is basically one independent variable you need to fully describe the state of a system.
example: a point moving freely in 3d space has 3 degrees of freedom (x, y, z). a pendulum swinging on a fixed arm has just 1 (the angle).
in physics, picking the right degrees of freedom = picking which variables actually matter to describe your system.

- too few – model's too simple, misses real behavior.

- too many – model's technically accurate but computationally impossible to run.
  
this ties directly to dimensionality reduction: reduction techniques are basically a systematic way of finding the smallest set of "true" degrees of freedom a system needs
instead of guessing by intuition/experience like physicists traditionally did ("more art than science").

how they actually do it 

nuclear models = parameterized differential equations (like schrodinger's equation) whose solutions are high-dimensional vectors (proton/neutron wave functions).
reduced basis methods (RBM): solve the problem in a small subspace that approximates the full solution manifold

machine learning approaches: neural networks, normalizing flows, genetic algorithms
used to find the reduced coordinates and simplified equations automatically.

applications mentioned
-nuclear structure studies
-neutron star dynamics (massive, dense systems)
-recoil separators (used in real detector experiments)
