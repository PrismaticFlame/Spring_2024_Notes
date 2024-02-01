# Syllabus Class
[[Doctor Conner's Stuff]]

Robotics is a lot of things! The definition is here, in [[What is meant by robots and robotics]] which helps us understand better what we are talking about.

Dr. Conner's Def: **A machine that uses its intelligence to interact with its changing environment.** (He said this!)

Lots of math, programming, *its math, not magic*

## Course Structure
- First half sem:
	- 3 lectures
	- Homework + midterm
- Second half:
	- 1 or 2 lectures per week
	- 1 or 2 "labtures" per week
		- Intro to ROS - "Robot Operating System" (You know this one!)
			- Not really an OS
		- Robotics in simulation in Hunter Creech
		- Robot demos
- Final exam will be heavily weighted toward front of course

## Grading
Homework and lab projects :                  30%
Course Project ( & 572 presentation):    10%
Midterm Exam:                                         30%
Final Exam:                                               30%

# Homework
[[Homework for Intro to Robotics]]

# Robot Navigation
[[How might a robot navigate]]?

Generally, we will define a reference frame in the world, either in 2D or 3D, and then use some math to do some path planning.

Using a cartesian coordinate system, we'll have two points on the plane and we need to find the distance between them for starters. But how do we do that? [[We find the distance between points like this]].

[[Workspace]]: Where the robot lives, where the robot works.

Finding a path in a workspace is easy when you have a simply shaped object, but what happens when you have a shaped object? [[The piano movers problem]].

==**Configuration:** of an object is the specification of all points on the object relative to its *workspace*.==

In this example, [[Rigid body motion]], there are multiple reference frames to be aware of.

His [Dr Conner's Robot] robot *Atlas* had 28 degrees of freedom:
- 6 per leg
- 6 per arm
- 3 torso
- 1 head

[[Configuration of an object]] and [[configuration space]] are set like that.

There are two distinct "spaces" we are dealing with!

Configuration Space vs. Workspace, [[What's the difference between configuration and work spaces]] 

All of that is nice, but how do I get the [[configuration of object]] in order?

For reference frames, Red for x, Green for y, and Blue for Z (RGB). Another way to help with understanding is the right hand rule.

**Homework:** Make a coordinate frame?

# 1/10/24
# Configuration Space Review
- **Configuration of an object is the specification of all points on the object relative to its workspace**

==Mildly Important:== In this course, when reference frames are mentioned then it is more likely taking a "snapshot" and talking about the [[Body Frame]] 

# Grubler's Equation for Degrees of Freedom
*Not on the exam*
[[Grublers Equation for Degrees of Freedom]]


Not terribly important, but might be important in the future.

## So, how many degrees of freedom is necessary?
- Kinova Robot Arm
	- Designed for assistive use
	- We have on in lab!
But the JACO arm improved upon this and created an arm that has 7 degrees of freedom.


There will be lots of Greek symbols in here, but physics has prepared for you this!

# Linear Algebra Review: Vectors
- "vector" : a "tuple" or "array" of real numbers
- Transpose
- Dot product* of two vectors of same size
	- $u \cdot v$ (They are vectors)
# Linear Algebra Review: Matrix Multiplication
[[Matrix Multiplication]] 

# Vector Review: Cross Products in 3D
Here is it explained with a few examples: [[Cross Products in 3D]]

# Rigid Body Transformations
The order of operations (per say) matters! They are *not communitive*.

Slide 30 will display that this matters, as well as a number of preceding slides.
## 2D Rotation Matrices
- $q_b = \begin{bmatrix} x_b \\ y_b \end{bmatrix}$ point in body frame (Slide 31)

### Basis Vectors
- $\hat{x} = \begin{bmatrix} \cos\theta \\ \sin \theta \end{bmatrix}$
- $\hat{y} = \begin{bmatrix} - \sin\theta \\ \cos \theta \end{bmatrix}$
Those basis vectors can be considered in the "World Frame" but is eventually dropped for succinctness. 

#todo There will be more matrix operations written here later from slide 31

... This rotation matrix changes the "basis" of vector from body frame to world frame; e.g., $^w R_b : q_b -> q_w$

## 2D Homogeneous Transformations
- $q_b = \begin{bmatrix} x_b \\ y_b \\ 1\end{bmatrix}$ point in body frame (Slide 33)

### Translation
$$q_w = \begin{bmatrix} 1 & 0 & x \\ 0 & 1 & y \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x_b \\ y_b \\ 1 \end{bmatrix} = \begin{bmatrix} x_b + x \\ y_b + y \\ 1 \end{bmatrix}$$

### Rotation

### How to write this overall
$$^wT_B = \begin{bmatrix} R & \hat{t} \\ \hat{0} & 1 \end{bmatrix}$$

- This is a 1x2 row vector of zeros (0 with hat)
- This is a 2x2 block matrix (R)
- This is a 2x1 column vector (t with hat)

#todo Make sure to grab slides 30-38 and all their details.

## Duality of Transforms
- **Represent configuration** of one frame w.r.t (with respect to) another 
- **Transform points** from one frame into the other

## Composition of Homogeneous Transforms
- Compose transforms using matrix multiplication 
- Order of transformation matters

## "Fixed" vs "Moving" Axes
- Consider the transformations as being with respect to the "fixed" world axes (Slide 40)


# 1/12/24

# 2-link Planar Arm: Transformations
**Forward map:** C-space to Workspace
$$q=\begin{bmatrix}\alpha \\ \beta \end{bmatrix}$$
Transformation composition bookkeeping: End effector to world $$q_w = ^wT_1 \cdot ^1T_2 \cdot ^2T_{ee} \cdot q_{ee} = ^wT_{ee} \cdot q_{ee}$$
*Slide 7 continues this, will not be writing during class*
*Should definitely go to office hours about this specific slide*

*Slide 8 as well.*

# Inverse Transformations
- Given point in world frame, what is the relative position in body frame?
*Slide 9, on iPad*

## Inverse of 'Special Orthogonal' Matrices
- SO(2) - rotation matrix in 2D
	- Determinant = +1 (No scaling/stretching and relative positions stay same)
	$$R(\theta) = \begin{bmatrix} \cos \theta & - \sin \theta \\ \sin \theta & \cos \theta \end{bmatrix}$$
	- $|R|$ = $\cos^2 \theta + \sin^2 \theta = 1$ (Trigonometry identity and Pythagorean theorem) 
*Rest on slide 10*


*Slides 11-15*

# 1/19/24

# [[Quaternion]] Representation
- Extends complex numbers from 2 to 4 dimensions
	- 3D rotation embedded in 4D yields smooth representation
	- No gimble lock
- Hamilton (1843)
	- Not the Hamilton that threw away his shot!
	- [[Hamiltonian]]
	- Hamilton understood complex point in plane
	- Looking for same in 3D space
	- $i^2 = j^2 = k^2 = i \cdot j \cdot k = -1$
- Cross products
	- $i \cdot j = k$, and so on...

# 1/24/24
# [[2-Link Planar Arm- Differential Kinematics]]

# [[Differential Kinematics]]

# [[Differential Kinematics]] - [[Jacobian Map]]

Jacobian map is **linear** map between tangent spaces

# [[Differential Kinematics]] - [[Manipulability]]
$M = \sqrt{\text{det}(J \cdot J^T)}$

Linear algebra/systems terms
- Rank of matrix (e.g., "loses rank if not invertible)
- Condition number of matrix (how numerically stable the calculations are)
	- 1 is ideal ("circle") ... (Slide 9)
## [[Eigenvalues and Eigenvectors]]

# [[Differential Kinematics]] - [[Singularities]]

- If wiggling either joint (partial derivative), the resulting velocity is the same
- Can only generate motion in 1 direction
- Have lost a degree of freedom in my system
- Jacobian Map $\dot{q}\ \epsilon \ T_qQ -> \dot{p}\ \epsilon \ T_p W$ 
	- $\dot{p} = J(q)\dot{q}$
- has "dropped rank"
- There is a "null space"

# Rigid Body in a 2D Plane Kinematics

# [[Rigid Body Kinematics]]
- Simple derivative and integrals for unconstrained

- What about constrained motion
	- Constrained motion (velocities) in 2D place
		- Move (forward or backward) and turn (left right) about reference point
		- Cannot move sideways
	- Q) Can we get to any ($x, y, \theta$)
	- Q) 

# [[Nonholonomically Constrained Rigid Body]]
Slides 17-19?

# [[Vector Field Representation (Unicycle model)]]

[[Affine Control System]] : $\dot{q} = g_0 (q) + \sum_i g_i (q) u_i$

# [[Rolling Disk Model]]
- Let $\psi$ be the angle of the disk's head rotating about the body y-axis
- Let $R$ be the radius of the disk
- Constraints
	- No side slip and rolls without slipping (spinning)
- Inputs
	- Rotation of the disk (e.g. wheel drive)
	- Rotation about the vertical

# [[Differential-Drive Model]]
- Left and right drive wheels
	- Assume we don't care about rotation angle of wheels
	- Wheel radius R
	- Use wheel velocities as inputs
		- $\dot{\psi}_L$ and $\dot{\psi}_R$ 

## Body Rotation
$v = R \dot{\psi}$ for velocity of wheels
Euler's Theorem: any displacement equivalent to rotation about a fixed point!
Distance between wheels and the center of the robot: $c$
Distance from center of body to fixed point (not necessarily on the robot): $\rho$ 
Center body velocity: $v_b$
Angle between robot and fixed point: $\dot{\theta} = \omega_z$

$$\omega_z(\rho - c) = R\dot{\psi}_L$$
$$\omega_z\rho = v_b$$
$$\omega_z(\rho + c) = R\dot{\psi}_R$$
$$\rho - c = \frac{R\dot{\psi}_L}{\omega_z}$$
$$\omega_z(\rho - c + 2c) = R\dot{\psi}_R$$
$$\omega_z(\frac{R\dot{\psi}_L}{\omega_z}) + \omega_z2c = R\dot{\psi}_R$$
$$R\dot{\psi}_L + \omega_z2c = R\dot{\psi}_R$$
$$\omega_z = \frac{R\dot{\psi}_R - R\dot{\psi}_L}{2c}$$
$$v_b = \omega_z\rho = \omega_z(\frac{R\dot{\psi}_L}{\omega_z} + c)$$
$$v_b = R\dot{\psi}_L + \frac{R\dot{\psi}_R - R\dot{\psi}_L}{2c}c$$
$$v_b = \frac{R\dot{\psi}_L}{2} + \frac{R\dot{\psi}_R}{2}$$

# 1/29/24
# Example Block Diagram
## [[Feedback (Closed-loop) Control]]
## [[Feedback Control]]


# Mathematical Model: (<mark style="background: #FF5582A6;">Won't be on test</mark>)

R - Resistance
L - Inductance
V - Voltage
K - Voltage/Torque constant
$\tau$ - Torque
$i$ - Current
$f$ - Friction Constant
$\omega$ - Motor Rotation Rate
G - Gear Ratio
$J$ - Inertia

## [[State Space Form]]

## Control Tasks
- Velocity Control:     $error(t) = \dot{\theta}_{SP} - \dot{\theta}(t)$
- Position Control:    $error(t) = \theta_{SP} - \theta(t)$
- Setpoint tracking:   $error(t) = \theta_{SP} - \theta(t)$
	- Could have velocity or combination
- [[Disturbance Rejection]]

#  [[Proportional-Integral-Derivative Control]] (PID) Controller
- Error = setpoint - process variable
	- $e(t) = SP - PV$
- Control:
	- $V_c = V_{bias} + K_pe(t) + K_i\int_0^te(t)dt + K_d\dot{e}(t)$

- Bias              - constant term
- Proportional - control effort proportional to the error at this point in time
- Integral        - control effort proportional to the integral of error over time
- Derivative     - control effort proportional to the rate of change in error

| Parameter | Rise Time | Overshoot | Setting Time | Steady-state Error | Stability |
| ---- | ---- | ---- | ---- | ---- | ---- |
| $K_p$ | Decrease | Increase | Small change | Decrease | Degrade |
| $K_i$ | Decrease | Increase | Increase | Eliminate | Degrade |
| $K_d$ | Minor Change | Decrease | Decrease | No effect in theory | Improve if $K_d$ small |

## Standard Forms
- Control
	- $V_c = V_{bias} + K_pe(t) + K_i\int_0^te(t)dt + K_d\dot{e}(t)$
	- $V_c = V_{bias} + K (e(t) + \frac{1}{T_1}\int_0^te(t)dt + T_d\dot{e}(t))$

# [[State Space Equations]]

# [[Frequency Response]]

# Computers are discrete time
- Sample sensor data
	- Takes time to process data after sensing
- Estimate current state
	- Calculations take time
- Calculate control output
	- Calculations take time
- Send output to motor
	- Data conversion and transmission takes time

- Typical control rates of 10-1000Hz (samples per second)
- Need discrete approximations to derivatives and integrals

## [[Discrete Time Calculations]]
- Sample Period
	- $\Delta t = t_k - t_{k-1}$
- Derivative (Euler's method)
	- $\dot{e} \approx \frac{e_k - e_{k-1}}{\Delta t}$
- Integral (Trapezoid Rule)
	- $\int_o^t e dt \approx$ 
- Control Calculations


