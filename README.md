# Kalman Filter — Water Tank (Mathematical Notes)

## Overview
This project applies the (discrete) Kalman filter to estimate the water-tank state (e.g., fluid height and possibly flow) from noisy measurements. The README summarizes the state-space model, Kalman recursion, and parameter interpretation.

## State-Space Model
We use a linear discrete-time state-space model:
$$
x_{k+1} = A x_k + B u_k + w_k,
\\
z_k = H x_k + v_k,
$$
where
- \(x_k\) is the state vector at time k (e.g., tank level, derivative),
- \(u_k\) is the control input (e.g., inlet valve),
- \(z_k\) is the measurement (sensor reading),
- \(w_k\) ~ \(N(0,Q)\) is process noise (covariance Q),
- \(v_k\) ~ \(N(0,R)\) is measurement noise (covariance R).

## Kalman Filter Equations
Prediction (time update):
$$
\hat x_{k|k-1} = A \hat x_{k-1|k-1} + B u_{k-1},
\\
P_{k|k-1} = A P_{k-1|k-1} A^T + Q.
$$
Update (measurement update):
$$
K_k = P_{k|k-1} H^T (H P_{k|k-1} H^T + R)^{-1},
\\
\hat x_{k|k} = \hat x_{k|k-1} + K_k (z_k - H \hat x_{k|k-1}),
\\
P_{k|k} = (I - K_k H) P_{k|k-1}.
$$
Interpretation: the Kalman gain K_k balances trust between model prediction and measurement according to their covariances.

## Parameter Tuning and Physical Meaning
- Q models unmodeled process disturbances (e.g., turbulent inflow), larger Q → filter trusts measurements more.
- R models sensor noise; larger R → filter trusts model more.

## Example: Single-State Tank Level
A very simple continuous-to-discrete linearization for a single tank level h with inflow u and outflow proportional to h can be written as:
$$
\dot h = -\alpha h + \beta u.
$$
Discretize with sampling Δt to obtain A ≈ e^{-αΔt}, B ≈ (1 - e^{-αΔt}) (β/α).

## Extensions
- Extended Kalman Filter (EKF) for nonlinear models; linearize dynamics around current estimate.
- Unscented Kalman Filter (UKF) for improved nonlinear performance.

## References
- Maybeck, Stochastic Models, Estimation, and Control.
- Welch & Bishop, "An Introduction to the Kalman Filter." 1995.

## Files
Check Jupyter notebooks (mini_project_6*.ipynb) for experiments and simulations.
