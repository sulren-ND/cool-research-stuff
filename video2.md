studying how fast/accurate a nuclear model runs matters because models need to be run through a bayesian pipeline: model to posterior distribution to comparison with data. getting good uncertainty quantification means running the model an enormous number of times, so a fast "emulated" version has to swap in for the expensive "high fidelity" one.
dimensionality reduction breaks down into two clear steps: finding good reduced coordinates, then finding the equations/dynamics that govern how those coordinates change over time.

the reduction toolbox includes reduced basis methods 
- ~eigenvector continuation
-  dynamic mode decomposition
-   eural implicit flow
-   gaussian processes
-   neural networks
-   normalizing flows
all  falling under the umbrella of "model order reduction."

- in a single channel scattering example, a long, high-dimensional solution vector actually lives on a much lower-dimensional "solution manifold"
- - PCA finds the reduced basis, and galerkin projection turns the original huge problem into just a couple of coefficients and equations.

- in a real production pipeline for optical potential scattering, the high fidelity model uses about 5,000 variables while the reduced model only needs about 100, and still reproduces the cross section observable accurately.
- 
the reduced basis + galerkin approach breaks down for three reasons:
  - the operators are too mathematically challenging to work with
  - linear embedding doesn't represent the data well when the underlying shape is nonlinear
  - or there are no clean equations to project onto in the first place (like a purely experimental setup)

when that traditional approach breaks down, the fix is learning the reduced coordinates and their governing equations directly from data instead of deriving them by hand.
  - comparing least squares fitting, full galerkin projection, and learned equations from data shows that learned equations can match or outperform galerkin, including when extrapolating.
  - autoencoders handle non-linear embedding when PCA-style linear reduction isn't good enough, especially for time dynamics problems.
  - SINDy (sparse identification of nonlinear dynamics) finds the governing equations after autoencoder-based reduction.
  - neural implicit flow (NIF) was used in a "vibrating calcium" example, which won an undergrad research award.
  - genetic programming discovers equations from data for nuclear density functional theory, applied to 48Ca skyrme and RMF DFT models.

reduced basis method in summary:
- find good reduced coordinates
- find dynamics
- if linearly embeddable, use the galerkin approach

for antennas- need nonlinear approach, so autoencoding?
