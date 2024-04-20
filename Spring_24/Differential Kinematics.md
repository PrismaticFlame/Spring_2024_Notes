Certainly! Let's delve into the details of differential kinematics, provide three examples, and format the equations using LaTeX.

### Differential Kinematics:

Differential kinematics deals with the relationship between joint velocities and end-effector velocities in a robotic system. The Jacobian matrix is a key tool in representing this relationship.

### Jacobian Matrix (\(J\)):

The Jacobian matrix relates the joint velocities \(\dot{\theta}\) to the end-effector velocities \(\dot{x}\) and \(\dot{y}\):

\[ J = \begin{bmatrix} \frac{\partial x}{\partial \theta_1} & \frac{\partial x}{\partial \theta_2} & \ldots & \frac{\partial x}{\partial \theta_n} \\ \frac{\partial y}{\partial \theta_1} & \frac{\partial y}{\partial \theta_2} & \ldots & \frac{\partial y}{\partial \theta_n} \\ \vdots & \vdots & \ddots & \vdots \\ \frac{\partial z}{\partial \theta_1} & \frac{\partial z}{\partial \theta_2} & \ldots & \frac{\partial z}{\partial \theta_n} \end{bmatrix} \]

### Examples:

#### 1. 2-Link Planar Arm:

For a 2-link planar arm with joint angles \(\theta_1\) and \(\theta_2\) and end-effector position \((x, y)\):

\[ J = \begin{bmatrix} -l_1 \sin(\theta_1) - l_2 \sin(\theta_1 + \theta_2) & -l_2 \sin(\theta_1 + \theta_2) \\ l_1 \cos(\theta_1) + l_2 \cos(\theta_1 + \theta_2) & l_2 \cos(\theta_1 + \theta_2) \end{bmatrix} \]

#### 2. 3-Link Planar Arm:

For a 3-link planar arm with joint angles \(\theta_1\), \(\theta_2\), and \(\theta_3\) and end-effector position \((x, y)\):

\[ J = \begin{bmatrix} -l_1 \sin(\theta_1) - l_2 \sin(\theta_1 + \theta_2) - l_3 \sin(\theta_1 + \theta_2 + \theta_3) & -l_2 \sin(\theta_1 + \theta_2) - l_3 \sin(\theta_1 + \theta_2 + \theta_3) & -l_3 \sin(\theta_1 + \theta_2 + \theta_3) \\ l_1 \cos(\theta_1) + l_2 \cos(\theta_1 + \theta_2) + l_3 \cos(\theta_1 + \theta_2 + \theta_3) & l_2 \cos(\theta_1 + \theta_2) + l_3 \cos(\theta_1 + \theta_2 + \theta_3) & l_3 \cos(\theta_1 + \theta_2 + \theta_3) \end{bmatrix} \]

#### 3. SCARA Robot:

For a SCARA (Selective Compliance Assembly Robot Arm) robot with joint angles \(\theta_1\), \(\theta_2\), \(\theta_3\) (elbow), and \(\theta_4\) (wrist) and end-effector position \((x, y, z)\):

\[ J = \begin{bmatrix} -l_1 \sin(\theta_1) - l_2 \sin(\theta_1 + \theta_2) - l_3 \sin(\theta_1 + \theta_2 + \theta_3) & -l_2 \sin(\theta_1 + \theta_2) - l_3 \sin(\theta_1 + \theta_2 + \theta_3) & -l_3 \sin(\theta_1 + \theta_2 + \theta_3) & 0 \\ l_1 \cos(\theta_1) + l_2 \cos(\theta_1 + \theta_2) + l_3 \cos(\theta_1 + \theta_2 + \theta_3) & l_2 \cos(\theta_1 + \theta_2) + l_3 \cos(\theta_1 + \theta_2 + \theta_3) & l_3 \cos(\theta_1 + \theta_2 + \theta_3) & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \]

In these examples, \(l_1\), \(l_2\), \(l_3\) represent the lengths of the robot links. The Jacobian matrix allows us to compute the end-effector velocities given joint velocities and is crucial for robot control and trajectory planning.