# RG830 Robot Manual

## Emergency Stop
When the robot is energized, the emergency buttons on the robot and any other external emergency conditions must be cleared, and then the Motor On button must be pressed.

![KT803](_media/AcilDurdurma.png)

**A:** Emergency Stop Button

**B:** Motor On Button

## Operating Modes

![RG830](_media/ModSecim.png)

- **A - Automatic Mode:** Production Mode
- **B - Manual Mode:** Movement and controls can be performed in jog mode.

## Robot Axis Control with Jog Movement

- While the robot is in manual mode, the **Motor On** button located on the right side of the FlexPendant must be pressed to activate the motion units.

![RG830](_media/MotorOnButon.png)

**A:** Motor On Button

- You can access the Jogging page from the upper-left menu bar to see axis-related statuses.
- Axes 1–6 can be moved one by one. On the first press, the direction controls for axes 1–3 are shown; on the second press, axes 4–6 are shown below the corresponding axis numbers.

![RG830](_media/1_6EksenSecim.png)

**A:** Axis 1–6 selection control

**B:** Currently selected axis range

- The robot can be moved linearly along the X, Y, and Z axes. These movements are performed relative to the Work Object (Wobj) selected in the interface, and the direction of movement is determined by the orientation of the relevant Wobj.

![RG830](_media/LineerHareketSecim.png)

**A:** Linear and Orientation Movement Selection Button

**B:** Linear Movement Display Icon

- Orientation movement based on tool selection.

![RG830](_media/OrientationHareketSecim.png)

**A:** Linear and Orientation Movement Selection Button

**B:** Orientation Movement Display Icon

## Robot Axis Calibration

- During the initial setup of the robot, calibration must be performed separately for each axis. During calibration, the zero-point marks (notches) of each axis must be aligned with high precision so that they face each other exactly. Each axis has its own dedicated notch.

![RG830](_media/EksenCentikleri.png)

- After all axes on the robot are physically aligned with the calibration notches, you can follow the visual steps below to save the relevant values via the FlexPendant. This process should be applied during the initial installation of the robot or whenever a **"Robot calibration lost"** warning is received from the system.

![RG830](_media/RobotEksenKalibrasyonu.png)

## TCP (Tool Center Point) Definition

The TCP (Tool Center Point) definition is performed by approaching a fixed, sharp-tipped reference point from different angles. The following steps must be followed to correctly define both the center point and the Z-axis direction:

- TCP&Z Approach Method

For this process, a total of 5 approach points must be defined to ensure high precision:

Approach 1, 2, and 3 (TCP Determination): The reference point is contacted from three different directions with approximately 120° angles between them.

Approach 4 (Perpendicular View): The tool is contacted with the reference point while positioned exactly perpendicular (90°). This is the primary reference point for orientation calculation.

Approach 5 (Z-Direction Definition): The tool is raised upward from the reference point along the Z-axis direction. This final point ensures the robot correctly identifies the positive Z direction in the tool coordinate system.

- Critical Application Notes

Precision: All approaches must contact the tip of the fixed reference point with the same millimeter-level accuracy. Deviations at contact points directly reduce the robot's operational precision.

Verification: After the definition is complete, move the robot in manual mode (Orientation) to verify that the tool tip remains stationary at the reference point.

- Approach Visuals

![RG830](_media/TCPyaklasim.png)

- Tool Definition Calibration Steps

Follow the visual sequence above to approach each reference point with precision. Once access to each point is complete, press the **Modify Position** button indicated in step 5 of the image below to save the relevant coordinate to the system. After all required points have been taught in this manner, press **OK** to finalize the calibration process.

**NOTE:** The robot must be in Manual Mode for this operation.

![RG830](_media/TCP_TanıtmaAdimları.png)

## Wobj (Work Object) Definition

**Wobj (Work Object):** A user-defined coordinate system used to describe parts or fixtures within the robot's working area. In ABB robot systems, the Wobj definition is performed using the **3-Point Method** on the relevant surface.

- **Definition with the 3-Point Method**

To create the coordinate system, the operator teaches the following three reference points in order:

**X1 (Origin Point):** The starting (zero) point of the surface to be defined. The center of the coordinate system is set at this point.

**X2 (X-Axis Direction):** The second point that determines the direction of the X-axis. The line between X1 and X2 forms the positive X direction of the system.

**Y1 (Y-Axis Direction):** The third point that determines the direction of the Y-axis. This point describes the positive Y direction perpendicular to the X-axis.

By moving the robot to each definition point (X1, X2, Y1) separately and clicking **Modify Position** as shown in image 5, you can teach the coordinates of that point. After all teaching steps are completed, click **OK** as shown in image 5 to finalize the process.

**Automatic Z-Axis and Planarity**

The plane formed by these three taught points is mathematically calculated by the system, which automatically determines the Z-axis.

**Movement on Inclined Surfaces:** Even if the defined surface is inclined, when the robot moves using the Wobj reference of that surface, it performs perfectly linear movement based on the surface inclination.

**Precision:** The farther apart X and Y points are and the more precisely they are selected, the higher the accuracy of the created Wobj.

**NOTE-1:** The accuracy of the TCP values of the Tool used during the Wobj definition process directly affects the precision of the created work object.

**NOTE-2:** The robot must be in Manual Mode for this operation.

- You can follow the steps for the Wobj definition process in the images below.

![RG830](_media/WobjTanıtım.png)

## Teaching Mold Pick and Place Points

In the system, mold picking and placing operations are performed on the same coordinate plane. Therefore, the definition made for the pick point will automatically apply to the place operation as well.

- Magazine Layout and Software Structure:

The current system includes Left and Right Magazine layouts, each consisting of 3 levels. These layouts are categorized in the system as F1, F2, and F3, and the cell arrangement of each level is defined in software using Array structures. This array structure enables the robot to navigate automatically and precisely to each sub-compartment within every level.

**IMPORTANT NOTE:** All point definition and update operations must be performed while preserving the orientation values used in the robot's standard operating cycle. Point updates must not be made with randomly selected joint angles or orientations; it must be confirmed that the robot is at the correct approach angle for the target point. Records made at random positions may cause trajectory errors and mechanical collisions in automatic mode.

- The following steps must be followed when teaching mold pick points:

**Alignment:** The robot must be precisely positioned at the relevant pick point in manual mode.

**Mechanical Check:** With the gripper in the open position, confirm that the centering pins are fully aligned with the slots on the mold.

**Lock Test:** Close the gripper to check mechanical fit and gripping security.

**Recording:** Once the physical placement is verified as correct, complete the recording of the reference point for the relevant Array element by following the visual instructions below.

**NOTE:** The robot must be in Manual Mode for this operation.

![RG830](_media/AlmaBirakmaNokta.png)  ![RG830](_media/AlmaBirakmaNoktaR.png)

## Teaching Accessory Control Points

Each accessory in the system has its own control sensor for presence/absence detection. The following procedure must be followed to correctly define the accessory control point:

- Alignment and Positioning:

After the robot picks the mold from the relevant station, it must exit in a linear path without disturbing the gripping plane and orientation. The accessory must be positioned directly in front of the sensor and within the detection range. The robot's position at this control point should be determined and recorded as the position where the sensor most reliably detects the accessory.

- Software Structure:

As with pick-and-place points, accessory control points are defined within Array structures named specifically for each accessory group. This allows separate and independent control coordinates to be created for each accessory type.

- Recording:

Once precise positioning is complete, the point recording steps must be performed by following the visual instructions below.

**NOTE:** The robot must be in Manual Mode for this operation.

![RG830](_media/AksesuarKontrolL.png)  ![RG830](_media/AksesuarKontrolR.png)

## Teaching the Drill Tool Tip Control Point

Before starting a drilling operation, the robot checks the integrity of the drill bit (broken bit detection) via the DrillingToolControlProg routine. It is critical that the reference control point is correctly taught for the system to perform this check reliably.

- Points to Consider:

Just as with pick and place operations, the control point must also be taught in the same orientation consistent with the robot's own operating cycle. The robot approaching this point at its standard working angle both improves detection accuracy and prevents trajectory errors.

The definition and recording steps for this point are detailed in the visuals below.

![RG830](_media/DrillToolKontrol.png)
