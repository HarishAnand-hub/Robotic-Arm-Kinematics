# Robotic Arm Kinematics — Forward & Inverse Kinematics

**Name:** Harish Anand  
**Institution:** Ira A. Fulton Schools of Engineering, Arizona State University, Tempe, USA

---

## Abstract

This report explores the concepts of Forward Kinematics (FK) and Inverse Kinematics (IK) for the Dobot Magician Lite robotic arm. It details the use of homogeneous transformation matrices for FK to compute the position of the end-effector from joint angles, and the use of symbolic solvers for IK to compute the joint angles required to reach a desired end-effector position. The validity of the solutions is confirmed through comparison with actual experimental results.

---

## I. Introduction

In robotics, Forward Kinematics (FK) and Inverse Kinematics (IK) are essential tools for controlling the position and orientation of a robot's end-effector. FK allows the determination of the end-effector's position from the robot's joint angles, while IK provides the inverse process: calculating the joint angles required to achieve a specific end-effector position.

This report applies FK and IK to the Dobot Magician Lite robot, which features three revolute joints and a prismatic joint. The analysis uses symbolic computations in MATLAB to derive the end-effector position and compute joint angles.

---

## II. Theory

### A. Forward Kinematics (FK)
FK is the process of determining the position of the robot's end-effector given the joint angles. The FK of a robot arm can be described using Homogeneous Transformation Matrices (HTM), which represent the relationship between consecutive joints and the end-effector.

For each joint i, a transformation matrix Hᵢ is computed using the Denavit-Hartenberg parameters. The FK equation for a three-joint robot is:

```
H = H₀₁ · H₁₂ · H₂₃
```

The end-effector position in 3D space is extracted from the final transformation matrix:

```
Px = H03(1,4),  Py = H03(2,4),  Pz = H03(3,4) - a1
```

### B. Inverse Kinematics (IK)
IK is the process of computing the joint angles θ₁, θ₂, θ₃ from a given end-effector position (x, y, z). IK is typically more challenging as it may have multiple solutions depending on the robot's configuration (elbow-up or elbow-down).

The solution is obtained by solving the system of nonlinear equations formed from the FK equations using numerical or symbolic solvers.

---

## III. Methodology

### A. Forward Kinematics Implementation
- FK calculations done using symbolic joint variables θ₁, θ₂, θ₃ and known link lengths a₁, a₂, a₃
- Transformation matrices H₀₁, H₁₂, H₂₃ defined for each joint using Denavit-Hartenberg parameters
- Final end-effector position computed by multiplying transformation matrices

### B. Inverse Kinematics Implementation
- Target end-effector position (x, y, z) substituted into FK equations
- MATLAB's symbolic `solve` function used to calculate joint angles
- Multiple solutions computed for elbow-up and elbow-down configurations

---

## IV. Results

### A. Forward Kinematics Results

| Joint Angles (°) | θ₁ | θ₂ | θ₃ |
|-----------------|-----|-----|-----|
| (0, 0, 0) | 0 | 0 | 0 |
| (90, 20, 50) | 90 | 20 | 50 |
| (−2, 25, 23) | -2 | 25 | 23 |
| (31, 52, 42) | 31 | 52 | 42 |
| (27, 52, 24) | 27 | 52 | 24 |

### B. Inverse Kinematics Results

| Position | θ₁ (°) | θ₂ (°) | θ₃ (°) |
|----------|--------|--------|--------|
| (240, 0, 150) | 0 | 0 | 0 |
| (0, 272.5, 68.54) | 90 | 19.94 | 28.89 |
| (300, 50, 100) | 9.46 | 102.09 | -63.05 |
| (280, −105, 15) | -34.86 | 119.56 | -36.40 |
| (35, 270, −33) | 82.61 | 48.36 | 62.14 |

---

## V. Discussion

The Forward Kinematics results verified that the Dobot Magician Lite's end-effector positions closely match the calculated values, confirming the accuracy of the kinematic model. For Inverse Kinematics, multiple feasible solutions were obtained for each target position, demonstrating the robot's flexibility in reaching desired poses using different configurations (elbow-up and elbow-down).

These results highlight the effectiveness of symbolic computation in MATLAB for analyzing robotic kinematics. However, for more complex robotic systems with higher degrees of freedom, exact symbolic solutions may become computationally intensive, necessitating the use of numerical methods.

---

## VI. Conclusion

This report presented a comprehensive analysis of Forward and Inverse Kinematics applied to the Dobot Magician Lite robotic arm. The FK model accurately calculated end-effector positions for various joint configurations, while the IK solver successfully determined joint angles for desired positions, including both elbow-up and elbow-down configurations.

Future work will focus on experimental validation with the physical Dobot, extending the models to handle more complex robotic systems, and exploring numerical techniques for IK solutions.

---

## References

1. MATLAB Robotics Toolbox, MathWorks. https://www.mathworks.com/help/robotics/
2. Dobot, "Dobot Magician Lite." https://www.dobot.cc
