# RG830 Robot Manual

## Emergency Stop
When the robot is energized, the emergency buttons on the robot and any other external emergency conditions must be cleared, and then the Motor On button must be pressed.

![Emergency Stop Button](_media/AcilDurdurma.png)

## Operating Modes
- **Automatic Mode:** Production Mode
- **Manual Mode:** Movement and controls can be performed in jog mode.

![Operating Mode Selection](_media/ModSecim.png)

## Robot Axis Control with Jog Movement
- While the robot is in manual mode, the **Motor On** button located on the right side of the FlexPendant must be pressed to activate the motion units.

![Motor On Button](_media/MotorOnButon.png)

- You can access the Jogging page from the upper-left menu bar to see axis-related statuses.
- Axes 1–6 can be moved one by one. On the first press, the direction controls for axes 1–3 are shown; on the second press, axes 4–6 are shown below the corresponding axis numbers.

![Axis 1-6 Selection](_media/1_6EksenSecim.png)

- The robot can be moved linearly along the X, Y, and Z axes. These movements are performed relative to the Work Object (Wobj) selected in the interface, and the direction of movement is determined by the orientation of the relevant Wobj.

![Linear Movement Selection](_media/LineerHareketSecim.png)

- Orientation movement based on tool selection.

![Orientation Movement Selection](_media/OrientationHareketSecim.png)

## Robot Axis Calibration
- During the initial setup of the robot, calibration must be performed separately for each axis. During calibration, the zero-point marks (notches) of each axis must be aligned with high precision so that they face each other exactly.

![Axis Calibration Notches](_media/EksenCentikleri.png)

- After all axes on the robot are physically aligned with the calibration notches, you can follow the visual steps below to save the relevant values via the FlexPendant. This process should be applied during the initial installation of the robot or whenever a **"Robot calibration lost"** warning is received from the system.

![Robot Axis Calibration Steps](_media/RobotEksenKalibrasyonu.png)

## TCP (Tool Center Point) Definition

TCP is the exact center point where the robot's end effector (gripper, screw-driver, drill, etc.) performs its work. By default, the robot control unit only knows the robot's wrist center (6th axis flange center). However, in real operations it is the **Tool** attached to the wrist — not the wrist itself — that does the work, so the tip point of this tool must be mathematically defined for the robot.

**What is the Purpose of TCP Definition?**

**Precise Movement:** When the TCP is correctly defined, the robot performs all orientation movements around this point. Even when the robot's wrist moves, the tool tip (TCP) remains fixed.

**Linear Accuracy:** When the robot is required to move linearly along the X, Y, or Z axes, this movement is calculated based on the defined TCP point rather than the wrist center.

**Path Tracking:** For drilling, screw-driving, and gripping operations, the TCP must be accurate to the millimeter for the robot to perfectly follow the path on the workpiece.

- During TCP definition, the process is carried out by approaching a fixed, preferably sharp object from different angles.

## Wobj (Work Object) Definition

**Wobj (Work Object):** A user-defined coordinate system used to describe parts or fixtures within the robot's working area. In ABB robot systems, the Wobj definition is performed using the **3-Point Method** on the relevant surface.

- **Definition with the 3-Point Method**

To create the coordinate system, the operator teaches the following three reference points in order:

**X1 (Origin Point):** The starting (zero) point of the surface to be defined. The center of the coordinate system is set at this point.

**X2 (X-Axis Direction):** The second point that determines the direction of the X-axis. The line between X1 and X2 forms the positive X direction of the system.

**Y1 (Y-Axis Direction):** The third point that determines the direction of the Y-axis. This point describes the positive Y direction perpendicular to the X-axis.

By moving the robot to each definition point (X1, X2, Y1) separately and clicking **Modify Position** as shown in image 4, you can teach the coordinates of that point. After all teaching steps are completed, click **OK** as shown in image 5 to finalize the process.

**Automatic Z-Axis and Planarity**

The plane formed by these three taught points is mathematically calculated by the system, which automatically determines the Z-axis.

**Movement on Inclined Surfaces:** Even if the defined surface is inclined, when the robot moves using the Wobj reference of that surface, it performs perfectly linear movement based on the surface inclination.

**Precision:** The farther apart X and Y points are and the more precisely they are selected, the higher the accuracy of the created Wobj.

**NOTE:** The accuracy of the TCP values of the Tool used during the Wobj definition process directly affects the precision of the created work object.

- You can follow the steps for the Wobj definition process in the images below.

![Wobj Definition Steps](_media/WobjTanıtım.png)
