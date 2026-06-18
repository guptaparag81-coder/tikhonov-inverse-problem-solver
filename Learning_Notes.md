# Tikhonov Regularisation for Ill-Posed Inverse Problems - Learning Notes

Author: Parag Gupta

---

# 1. Purpose of the Project

The purpose of this project is to recover an unknown source profile from noisy measurements.

The workflow includes:

1. Building a forward model
2. Creating synthetic measurements
3. Adding measurement noise
4. Solving an inverse problem
5. Applying Tikhonov regularisation
6. Performing L-curve analysis
7. Evaluating solution accuracy

This type of problem is commonly encountered in environmental monitoring, medical imaging, geophysics, and quantitative modelling.

---

# 2. What is an Inverse Problem?

An inverse problem attempts to recover unknown causes from observed effects.

Forward Problem:

Source → Measurements

Inverse Problem:

Measurements → Recover Source

Examples:

- Methane leak estimation
- CT scan reconstruction
- MRI reconstruction
- Seismic imaging
- Financial signal extraction

Inverse problems are often difficult because small measurement errors can produce large solution errors.

---

# 3. Forward Model

Code:

```python
A
```

Purpose:

The matrix A represents the physical relationship between source locations and sensor measurements.

The forward model is:

L = Aq

where:

L = measurements

A = system matrix

q = unknown source

---

# 4. What is an Ill-Posed Problem?

A problem is ill-posed if:

- Multiple solutions exist
- Small measurement noise causes large errors
- Stable inversion is difficult

Ill-posed problems frequently occur in real-world scientific applications.

---

# 5. Measurement Noise

Definition:

Noise represents uncertainty or errors in sensor measurements.

Examples:

- Instrument noise
- Environmental fluctuations
- Data acquisition errors

In this project:

5% Gaussian noise is added to measurements.

---

# 6. Naive Inversion

Code:

```python
np.linalg.pinv(A)
```

Purpose:

Attempts to recover the source directly from measurements.

Problem:

Noise is amplified dramatically.

Result:

The recovered source often becomes unstable and unrealistic.

---

# 7. What is Tikhonov Regularisation?

Tikhonov regularisation stabilises inverse problems by penalising large solution values.

Objective Function:

min ||Aq − L||² + λ||q||²

where:

λ = regularisation parameter

The additional penalty discourages unstable solutions.

---

# 8. Lambda Parameter

Lambda controls the balance between:

Data Fit

and

Solution Smoothness

Small λ:

- Fits noise
- Unstable solution

Large λ:

- Over-smooths solution
- Loses detail

Optimal λ:

- Best balance between stability and accuracy

---

# 9. Tikhonov Solution

Formula:

q = (AᵀA + λI)⁻¹AᵀL

Purpose:

Produces a stable estimate of the unknown source.

This is one of the most widely used regularisation methods in inverse modelling.

---

# 10. L-Curve Analysis

Definition:

The L-curve plots:

Residual Norm

vs

Solution Norm

for different λ values.

Purpose:

Helps identify the optimal regularisation parameter.

---

# 11. Residual Norm

Definition:

Measures how well the model fits the data.

Formula:

||Aq − L||

Small residual:

Good data fit.

---

# 12. Solution Norm

Definition:

Measures the size or complexity of the recovered solution.

Formula:

||q||

Large solution norms often indicate overfitting or noise amplification.

---

# 13. L-Curve Corner

The corner of the L-curve typically corresponds to the optimal λ.

Interpretation:

Best compromise between:

- Data accuracy
- Solution stability

---

# 14. Recovery Error

Definition:

Measures how close the recovered source is to the true source.

Formula:

Relative Error =
||q_recovered − q_true||
/
||q_true||

Lower error indicates better recovery.

---

# 15. Scientific Interpretation

Without Regularisation:

- Noise dominates
- Solution becomes unstable

With Tikhonov Regularisation:

- Solution becomes smooth
- Noise is suppressed
- Source recovery improves

---

# 16. Applications

Tikhonov regularisation is widely used in:

- Environmental Monitoring
- Methane Quantification
- Medical Imaging
- Geophysical Exploration
- Remote Sensing
- Financial Signal Recovery

---

# 17. Overall Workflow

True Source
↓
Forward Model
↓
Synthetic Measurements
↓
Add Noise
↓
Naive Inversion
↓
Tikhonov Regularisation
↓
L-Curve Analysis
↓
Optimal Source Recovery

---

# Interview Summary

If asked about the project:

"I implemented a Tikhonov regularisation framework in Python to solve an ill-posed inverse problem. The project demonstrates how noisy measurements can be used to recover an unknown source profile while avoiding instability caused by noise amplification. I also implemented L-curve analysis to identify an optimal regularisation parameter and evaluated recovery accuracy using relative error metrics."
