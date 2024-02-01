Differential kinematics, also known as velocity kinematics or Jacobian, deals with the relationship between joint velocities and end-effector velocities in a robotic system. For a 2-link planar arm, we can describe the differential kinematics using the Jacobian matrix.

### 2-Link Planar Arm Description:

Let's consider a 2-link planar arm with two revolute joints. The arm has joint angles \(\theta_1\) and \(\theta_2\), and the end effector (tip of the arm) is located at the point \((x, y)\) in a Cartesian coordinate system.

### Kinematic Equations:

1. **Forward Kinematics:**
   \[ x = l_1 \cos(\theta_1) + l_2 \cos(\theta_1 + \theta_2) \]
   \[ y = l_1 \sin(\theta_1) + l_2 \sin(\theta_1 + \theta_2) \]

2. **Joint Velocities:**
   The joint velocities \(\dot{\theta}_1\) and \(\dot{\theta}_2\) represent the rates at which the joint angles are changing.

3. **End-Effector Velocities:**
   The velocities of the end effector (\(\dot{x}\) and \(\dot{y}\)) are related to the joint velocities through the Jacobian matrix.

### Jacobian Matrix:

The Jacobian matrix relates the joint velocities to the end-effector velocities:

\[ J = \begin{bmatrix} \frac{\partial x}{\partial \theta_1} & \frac{\partial x}{\partial \theta_2} \\ \frac{\partial y}{\partial \theta_1} & \frac{\partial y}{\partial \theta_2} \end{bmatrix} \]

### Calculating the Jacobian:

Let's compute the partial derivatives and form the Jacobian matrix for the 2-link planar arm.

1. **Partial Derivatives:**
   \[ \frac{\partial x}{\partial \theta_1} = -l_1 \sin(\theta_1) - l_2 \sin(\theta_1 + \theta_2) \]
   \[ \frac{\partial x}{\partial \theta_2} = -l_2 \sin(\theta_1 + \theta_2) \]

   \[ \frac{\partial y}{\partial \theta_1} = l_1 \cos(\theta_1) + l_2 \cos(\theta_1 + \theta_2) \]
   \[ \frac{\partial y}{\partial \theta_2} = l_2 \cos(\theta_1 + \theta_2) \]

2. **Jacobian Matrix \(J\):**
   \[ J = \begin{bmatrix} -l_1 \sin(\theta_1) - l_2 \sin(\theta_1 + \theta_2) & -l_2 \sin(\theta_1 + \theta_2) \\ l_1 \cos(\theta_1) + l_2 \cos(\theta_1 + \theta_2) & l_2 \cos(\theta_1 + \theta_2) \end{bmatrix} \]

### End-Effector Velocities:

The end-effector velocities can be expressed as a column vector:

\[ \begin{bmatrix} \dot{x} \\ \dot{y} \end{bmatrix} = J \begin{bmatrix} \dot{\theta}_1 \\ \dot{\theta}_2 \end{bmatrix} \]

The Jacobian allows us to relate the joint velocities to the velocities of the end effector in the Cartesian space. This is essential for control, trajectory planning, and understanding how changes in joint angles affect the motion of the end effector in a 2-link planar arm.