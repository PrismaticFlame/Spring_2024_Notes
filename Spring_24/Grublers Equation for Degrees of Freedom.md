Gruebler's equation, named after its creator Franz Gruebler, is used in mechanical engineering and robotics to calculate the degrees of freedom of a mechanical system. The equation is particularly useful for systems with rigid bodies and joints, such as robotic manipulators. Gruebler's equation relates the number of degrees of freedom (\(DOF\)) to the number of links (\(L\)), joints (\(J\)), and constraints (\(C\)) in the system.

The formula for Gruebler's equation is given by:

\[ DOF = 3(L - 1) - 2J - C \]

where:
- \( DOF \) is the total number of degrees of freedom.
- \( L \) is the number of links in the system.
- \( J \) is the number of joints in the system.
- \( C \) is the number of constraints in the system.

The equation accounts for the fact that each rigid link reduces the system's degrees of freedom by 6 (3 translational and 3 rotational). The term \(3(L - 1)\) represents the degrees of freedom associated with the free movement of the system. The term \(2J\) accounts for the constraints introduced by the joints, each of which typically constrains two degrees of freedom. The \(C\) term represents additional constraints that might be present in the system.

It's important to note that this equation assumes a planar mechanism or a spatial mechanism where each joint provides one translational and one rotational degree of freedom. For more complex systems or those with special joint configurations, modifications to the formula may be necessary.

Gruebler's equation is a valuable tool for analyzing the mobility of mechanical systems and is often used in the design and analysis of robotic manipulators to ensure they have the required degrees of freedom for their intended tasks.