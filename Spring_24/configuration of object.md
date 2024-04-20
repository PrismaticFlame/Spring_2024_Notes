- Configuration of a moving object is the specification of all points on the moving object
- Specification of the degrees of freedom (DoF) of object
	- Point in 2D place = 2 DoF (x, y)
	- Rigid body in 2D plane
		- 3 DoF (x, y, $\theta$)
	- Rigid body in 3D space
		- 6 DoF (x,y,z, roll, pitch, yaw)
	- n-link robot arm with fixed base

# Some configurations
In robotics, the term "configuration" refers to the arrangement or set of parameters that fully defines the state of a robot or an object. The specific configurations depend on the type of robot or object in consideration. Here are some examples of different configurations in robotics:

1. **Joint Configuration:**
   - For robots with articulated limbs, the joint configuration specifies the angles of each joint. This is crucial for defining the position and orientation of the robot's end-effector.

2. **Pose Configuration:**
   - The pose configuration encompasses both the position (x, y, z) and orientation (roll, pitch, yaw) of an object or a robot's end-effector in a three-dimensional space.

3. **Articulated Robot Configuration:**
   - In the context of articulated robots, such as robot arms, the configuration involves the joint angles. For example, a 6-DOF (Degrees of Freedom) robot arm might have a configuration represented by a set of six joint angles.

4. **Wheeled Robot Configuration:**
   - For mobile robots with wheels, the configuration may involve parameters such as the position (x, y) of the robot's center, its orientation, and possibly the velocities of its wheels.

5. **Holonomic and Non-Holonomic Configurations:**
   - Holonomic robots have configurations that allow them to move freely in all directions without constraints. Non-holonomic robots, on the other hand, have configurations that limit their instantaneous motion in certain directions.

6. **Manipulator Configuration:**
   - In the context of robotic manipulators, the configuration defines the joint angles and lengths of the links, determining the position and orientation of the end-effector.

7. **Static Configuration:**
   - For objects at rest, the static configuration includes parameters like position, orientation, and dimensions. This is relevant for objects in a scene that a robot may need to interact with or avoid.

8. **Dynamic Configuration:**
   - In dynamic scenarios, the configuration may include information about the velocities, accelerations, and forces acting on the robot or object. This is particularly important for tasks involving motion planning and control.

9. **Sensor Configuration:**
   - Some robots are equipped with sensors, and their configuration may include parameters related to the orientation and alignment of these sensors.

10. **Multi-Robot Configuration:**
    - In scenarios involving multiple robots, the configuration space extends to the positions, orientations, and possibly velocities of each robot relative to others.

Understanding and appropriately representing these configurations are essential for tasks such as motion planning, control, and simulation in robotics. Different types of robots and objects have unique sets of parameters that define their configurations based on their mechanical structures and intended functionalities.