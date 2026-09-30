# Week 3: Bootstrapping for Uncertainty

`Bootstrapping.ipynb` fits a linear regression to a synthetic dataset (`make_regression`, 1,000 rows, 3 informative features, noise=50), then runs 100 bootstrap resamples (sampling with replacement, same size as the original data) to see how much the fitted coefficients vary.

**Findings:**

- Coefficient estimates are stable across resamples — bootstrap standard deviations (~1.5–1.8) are close to the theoretical standard error (noise/√n ≈ 1.6), and bootstrap means match the single-fit baseline closely.
- All three features are consistently nonzero across every resample, but feature_1 and feature_3 are large, high-precision effects (coefficient of variation ~2%), while feature_2 is a smaller, noisier effect (coefficient of variation ~22%).
- The bootstrap distributions center on the original fit rather than the true generating coefficients, confirming that gaps between the baseline estimate and ground truth are ordinary sampling variation, not a modeling error.
