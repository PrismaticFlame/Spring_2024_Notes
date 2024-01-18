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

