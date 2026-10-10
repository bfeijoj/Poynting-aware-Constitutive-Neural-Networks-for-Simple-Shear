# Poynting-Aware Constitutive Artificial Neural Networks (PA-CANN)

Implementation of the **Poynting-Aware Constitutive Artificial Neural Network (PA-CANN)** developed for interpretable hyperelastic constitutive model discovery under incompressible simple shear.

The framework is designed to identify compact analytical strain-energy density functions from experimental shear- and normal-stress data, with particular emphasis on the representation of **positive and negative Poynting effects**.

## Overview

The PA-CANN combines:

- a **weight-shared Valanis–Landel principal-stretch branch** for the isotropic response;
- a **sign-flexible $I_2$ correction** designed to represent changes in the Poynting response;
- a reparameterization that preserves **positive reference-state isotropic shear stiffness**;
- **orientation-modulated principal-stretch features** for fiber-reinforced materials;
- the anisotropic pseudo-invariants $I_4$ and $I_5$;
- linear, quadratic, exponential, and sublinear square-root activation functions;
- simultaneous fitting of shear and normal stresses;
- $L_1$ regularization and post-training pruning to promote compact constitutive representations.

The framework is evaluated for isotropic and unidirectional fiber-reinforced materials under incompressible simple shear, including fiber orientations of $0^\circ$, $45^\circ$, and $90^\circ$.

## Constitutive formulation

For the isotropic contribution, the PA-CANN uses

$$
\psi_{\mathrm{isotropic}}
=
\psi_{\mathrm{VL}} + c_2(I_2-3),
$$

with

$$
\psi_{\mathrm{VL}}
=
\sum_{i=1}^{3} w_{\mathrm{VL}}(\xi_{\lambda_i}),
\qquad
\xi_{\lambda_i}
=
\left(\lambda_i-\lambda_i^{-1}\right)^2.
$$

The same scalar map $w_{\mathrm{VL}}$ is shared across the three principal stretches.

The Poynting-aware correction is constrained so that the reference-state isotropic shear stiffness remains positive while still allowing either sign of the normal-stress response.

For fiber-reinforced materials, the anisotropic branch additionally uses orientation-dependent stretch features together with

$$
\xi_{I_4}=(I_4-1)^2,
\qquad
\xi_{I_5}=(I_5-1)^2.
$$

## Main capabilities

- Constitutive model discovery directly from experimental data.
- Simultaneous fitting of $\tau_{12}$ and $\sigma_{22}$.
- Representation of both positive and negative Poynting responses.
- Explicit treatment of anisotropic fiber orientation effects.
- Joint calibration using multiple fiber orientations.
- Extraction of compact analytical strain-energy density functions.
- Sensitivity analysis with respect to training hyperparameters and initialization.
- Scatter-normalized model assessment using experimental variability.

## Scope

The models provided in this repository are developed and validated for **incompressible simple shear**.

Although the architecture is written in terms of constitutive deformation measures, the present work does **not** establish generalization to arbitrary three-dimensional loading paths.

Similarly, leave-one-orientation-out tests showed that the currently available angular sampling is insufficient for reliable prediction of unseen fiber orientations. A denser experimental sampling of fiber directions is expected to be necessary for a stronger assessment of angular generalization.

## Installation

Clone the repository:

```bash
git clone <REPOSITORY_URL>
cd <REPOSITORY_NAME>
```

Create and activate a Python environment, then install the required dependencies.

If a `requirements.txt` file is provided:

```bash
pip install -r requirements.txt
```

> Replace the commands above if a different environment manager is used in this repository.

## Usage

The repository contains the routines used to train, evaluate, and post-process the PA-CANN models presented in the associated study.

Typical workflow:

1. Load the experimental simple-shear dataset.
2. Select the isotropic or anisotropic PA-CANN formulation.
3. Define the training hyperparameters.
4. Train the model using the combined shear- and normal-stress loss.
5. Evaluate the fitted stresses.
6. Extract the identified strain-energy density function.
7. Apply post-training pruning, when appropriate.
8. Compute goodness-of-fit and scatter-normalized error metrics.

Exact execution commands depend on the scripts included in the repository.

## Experimental data

The experimental datasets analyzed in the associated study were obtained from previously published works by the authors and are cited in the manuscript.

The original experimental data are not redistributed as part of this repository but may be made available by the authors upon reasonable request, subject to the conditions associated with the original studies.

## Reproducibility

The study includes analyses of:

- multiple random initialization seeds;
- learning-rate sensitivity;
- normal-stress loss weighting;
- $L_1$-regularization sensitivity;
- pruning-threshold sensitivity;
- separate and combined calibration of fiber orientations.

For stochastic training, exact numerical results may vary slightly between runs unless the same random seed and computational environment are used.

## Model assessment

The reported performance metrics include:

- coefficient of determination $R^2$;
- root mean squared error (RMSE);
- mean absolute error (MAE);
- scatter-normalized error $E_{\mathrm{scatter}}$.

The scatter-normalized error is defined as

$$
E_{\mathrm{scatter}}
=
\sqrt{
\frac{1}{N}
\sum_{i=1}^{N}
\left(
\frac{y_i^{\mathrm{pred}}-\bar{y}_i^{\mathrm{exp}}}
{s_i^{\mathrm{exp}}}
\right)^2
}.
$$

Values near unity indicate model discrepancies of approximately the same order as one experimental standard deviation.

## Associated publication

**Poynting-Aware Constitutive Artificial Neural Networks: Hyperelastic Model Discovery under Simple Shear**

Authors: `<AUTHOR LIST>`

Journal: `<JOURNAL>`

DOI: `<DOI>`

If you use this code, please cite the associated publication.

```bibtex
@article{<CITATION_KEY>,
  title   = {Poynting-Aware Constitutive Artificial Neural Networks: Hyperelastic Model Discovery under Simple Shear},
  author  = {<AUTHOR LIST>},
  journal = {<JOURNAL>},
  year    = {<YEAR>},
  doi     = {<DOI>}
}
```

## Code availability

The source code used to implement, train, and evaluate the PA-CANN models is provided in this repository for research and reproducibility purposes.

## License

`<LICENSE INFORMATION>`

## Contact

For questions regarding the implementation, experimental data, or associated publication, please contact:

`<CORRESPONDING AUTHOR>`  
`<EMAIL>`
