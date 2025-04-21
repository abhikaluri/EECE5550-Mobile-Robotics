

```markdown
# MPPI Controller for UAV Trajectory Tracking

## Overview

This repository contains an implementation of a Model Predictive Path Integral (MPPI) controller for UAV trajectory tracking. The project demonstrates the application of sampling-based optimization techniques for controlling a quadrotor UAV across three challenging trajectories: Circle, Figure-8, and Tilted Circle patterns.

## Key Features

- **Full 3D Quadrotor Dynamics**: Complete nonlinear dynamics with quaternion-based orientation
- **MPPI Optimization**: Sampling-based control using 500 rollouts per step
- **Hybrid Control**: MPPI combined with PID altitude control for enhanced stability
- **Trajectory-Specific Tuning**: Optimized parameters for different flight patterns
- **Physics-Accurate Simulation**: 4th-order Runge-Kutta integration with realistic constraints
- **Visual Analytics**: Rich visualization of rollouts, cost evaluation, and performance metrics

## Results

The controller successfully tracks complex trajectories with:
- Position tracking errors below 0.5m
- Sustained speeds of 10-20 km/h
- Stable tracking for 30+ loops (400+ seconds) without drift
- Smooth transitions through tight turns and altitude changes

## Implementation Details

### System Architecture

The implementation consists of five core modules:
1. **Reference Generator**: Creates time-parameterized target trajectories
2. **MPPI Controller**: Performs sampling-based optimal control computation
3. **Altitude PID**: Provides complementary height stabilization
4. **Dynamics Simulator**: Accurately propagates UAV state
5. **Visualizer**: Renders the controller's operation in real-time

### MPPI Algorithm

The MPPI controller works by:
1. Generating 500 random control sequences
2. Forward-simulating each through the UAV dynamics
3. Evaluating costs based on tracking error and control effort
4. Computing a weighted average of control disturbances
5. Applying the first control action and shifting the sequence

### Key Parameters

| Trajectory | Position Weight | Velocity Weight | Noise Parameters | Reward Structure |
|------------|----------------|-----------------|------------------|------------------|
| Circle     | 250.0          | 25.0            | [2.8, 0.7, 0.7, 0.5] | [100, 50, 25, 10, 5] |
| Figure-8   | 200.0          | 30.0            | [2.5, 0.6, 0.6, 0.4] | [80, 40, 20, 10, 5] |
| TiltedCircle | 150.0        | 30.0            | [2.5, 0.6, 0.6, 0.4] | [50, 25, 15, 8, 4] |

See the full parameter tables in the report for complete configuration details.

## Getting Started

### Prerequisites

- Python 3.8+
- NumPy
- Matplotlib
- tqdm (for progress bars)

No GPU or CUDA requirements! The entire implementation runs efficiently on CPU.

### Running the Code

1. Clone this repository:
   ```bash
   git clone https://github.com/abhikaluri/EECE5550-Mobile-Robotics.git
   cd EECE5550-Mobile-Robotics/mppi_quadrotor
   ```

2. Open and run the Jupyter notebook:
   ```bash
   jupyter notebook mppi_simulation.ipynb
   ```

3. Select different trajectory types by changing the `TRAJECTORY_TYPE` parameter:
   ```python
   # Options: 'Circle', 'Figure8', 'TiltedCircle'
   TRAJECTORY_TYPE = 'Circle'
   ```

## Project Report

The detailed project report is available in the repository:
- [MPPI_Controller_Report.pdf](MPPI_Controller_Report.pdf)

## Demo Video

A demonstration of the controller's performance is available on YouTube:
[MPPI Controller Demo Video](https://youtu.be/QovEdDXMJhE)

## Future Work

Planned extensions to this project include:
- Porting to run entirely on onboard UAV computers
- Gazebo simulation integration for hardware-in-loop testing
- Obstacle avoidance implementation in cluttered environments
- Adaptive parameter tuning based on tracking error

## References

1. T. P. Nascimento and M. Saska, "Position and attitude control of multirotor aerial vehicles: A survey," Annual Reviews in Control, pp. 129–146, 2019.
2. I. S. Mohamed, G. Allibert and P. Martinet, "Model Predictive Path Integral Control Framework for Partially Observable Navigation: A Quadrotor Case Study," 2020 16th International Conference on Control, Automation, Robotics and Vision (ICARCV), 2020, pp. 196-203.
3. J. Pravitra, K. A. Ackerman, C. Cao, N. Hovakimyan, and E. A. Theodorou, "L1-adaptive MPPI architecture for robust and agile control of multirotors," IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), 2020, pp. 7661–7666.
4. M. W. Mueller, M. Hehn, and R. D'Andrea, "A computationally efficient motion primitive for quadrocopter trajectory generation," IEEE Transactions on Robotics, vol. 31, no. 6, pp. 1294–1310, 2015.
5. S. Sun, A. Romero, P. Foehn, E. Kaufmann, and D. Scaramuzza, "A comparative study of nonlinear MPC and differential-flatness-based control for quadrotor agile flight," IEEE Transactions on Robotics, vol. 38, no. 6, pp. 3357–3373, 2022.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

This project was completed as part of the EECE5550 Mobile Robotics course.
```

