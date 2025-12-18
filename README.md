# Kalman Filter — Water Tank

## Overview
This project uses a Kalman filter to track the state of a water tank (level, flow, etc.) when sensors are noisy and the physics model is imperfect. It is written as a high-level guide so you can focus on intuition and tuning rather than equations.

## How the filter works
- Keep a running belief about the tank (state estimate) and how uncertain that belief is (covariance).
- At each step: predict what the tank is doing using the model, then correct that guess with the newest sensor reading.
- The Kalman gain balances trust between the model and the measurement based on their assumed noise levels.

## Model and noise intuition
- System model: how the tank level should change given inflow/outflow.
- Process noise (Q): captures unmodeled effects like turbulence or valve lag; larger values mean you lean more on measurements.
- Measurement noise (R): describes sensor accuracy; larger values mean you trust the model more than the sensor.

## Practical tips
- Start with reasonable Q/R guesses, then adjust until predictions and measurements are weighted appropriately.
- Watch residuals (measurement minus prediction) to see if noise assumptions look realistic.
- If the dynamics get nonlinear, try an Extended or Unscented Kalman Filter with the same predict/update cycle.

## Files
- `mini_project_6*.ipynb`: simulations of the tank, filtering steps, and experiments with different noise settings.
