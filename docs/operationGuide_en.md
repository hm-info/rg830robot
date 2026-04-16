# Machine Initial Startup Robot Gripper Mold Status

- When the system is first turned on, after reset, it asks for confirmation if there is a mold in the gripper.

![RG830](_media/o_GripperFree.png)

**YES:** It places the mold it has in its designated spot, returns to the home position, and waits for communication with the job file.

**NO:** It waits for communication with the job file in the home position.

- The exe file must be opened to read the job file.
- The prepared job file should be placed in the Robot File folder.
- When the Start button is pressed, the job file in the Robot File folder is read, data transfer from PLC to robot occurs, and after the information transfer is complete, the robot starts running the job file.

## Robot Passive Positioning Error Handling

## Door Opening Permission Procedure

- When the safety permission button in the entrance section is pressed, the system completes the current work cycle at a safe point. After the cycle ends, the system automatically gives approval to open the doors.

## Emergency Stop - Stop Scenarios.

**Emergency Stop Condition:**

When the Emergency Stop button is pressed, the active work cycle is canceled due to safety protocols, and the system enters safe standby mode. After this process, since the system data is reset, restarting the job file from the beginning is mandatory.

**Steps to Reactivate the System:**

![RG830](_media/o_AlarmRstButon.png)

- The pressed Emergency Stop button is released.
- **A:** Alarms (Reset) are cleared from the operator panel.
- **B:** Press Reset. The robot does "Po to Main", then **C** question panel opens.
- **C:** Inquiry is made whether there is a mold on the gripper or not. Subsequently, **D** question panel opens.
- **D:** Question panel opens regarding whether to continue with the same job file or a different job file after the emergency.

  **YES:** Continues with the job file in memory.

  **NO:** Waits for a different job file to be loaded. If it cannot read the job file for a certain period, it gives an error message that it could not read the file.

  **Stop Condition:**

When **E (Stop Button)** is pressed in the system, PLC and robot enter a coordinated "waiting mode". The technical operation of this process is as follows:

 - **PLC**, when the stop signal is received, freezes the current work step (state) and puts the system into "Stop State" mode.

 - **Robot**, instead of stopping movement immediately when the stop signal comes, continues to work until the next waiting signal step (checkpoint) to maintain process integrity. When the robot reaches that step, it stops and waits for the "status bit" from the PLC.

 - **Restarting the System:** When the operator presses **F (Start Button)**, the PLC activates the relevant status bit and directs the system back to the normal work cycle from the step it left off.

## When working with the line, when will the frame come from the line, is the frame coming from the line the same as the frame?

## Alarm conditions during frame clamping

- Frame Handling Axis Error
- Frame Handling Axis could not calibrate !
- Frame Handling Axis Speed Error !
- Frame Handling Axis Minimum Limit Error !
- Frame Handling Axis Maximum Limit Error !
- Frame Handling Axis Lag Error !


## Drilling Tool Not Ok Alarm Condition

**The system performs automatic tool control once at the beginning of each job to ensure operational safety. The process and what to do in case of error are specified below:**

- The robot touches the tool tip to a predefined control switch to verify the physical integrity of the drilling tool.

- If the verification signal is not received from the switch despite reaching the tool control point, the robot automatically stops movement. It moves to a safe waiting position (above the control point) and activates the status alarm on the operator panel.

**Intervention and Troubleshooting:**

- **Tool Damage:** If the drill bit is physically damaged or broken, it should be replaced with a new tool tip.

- **Sensor Check:** If no problem is observed on the tool tip, the functionality and cable connections of the relevant control sensor (switch) should be checked.

- **Reactivating the System:** After necessary physical corrections are made and the fault source is eliminated, press the **Start Button (F)** on the panel to continue the process from where it left off.

## Accessory Not Ok Alarm Condition

For the accessory mounting process to proceed healthily, it is critical that the part is successfully taken from the magazine and positioned precisely within the mold. Therefore, the presence and position of the part are checked via sensors before proceeding to the mounting stage.

If the accessory brought to the control point by the robot is not detected by the sensor, the system generates an "AccessoryNotOk" alarm; the robot moves to waiting mode by rising slightly from the control point to allow operator intervention. The solution paths to be followed in this case are specified below:

**Continuing with Manual Intervention**

- If the accessory has come out of the magazine but remained on the magazine because it was not fully taken by the mold:

The operator opens the safety door (the system will go into Emergency Stop mode) and enters the line. Takes the accessory from the magazine and manually places it into the mold, paying attention to the direction of arrival. After exiting the line and closing the safety door, reset the system and press *F (Start Button)* on the panel to continue the process from where it left off.

**Retrying the Picking Operation (If Accessory is in Magazine)**

- If the accessory has remained in the magazine and the operator wants the robot to pick the same accessory again:

After exiting the line and activating the safety lock, press *B (Reset Button)* on the panel. With this operation, the robot will repeat the accessory picking cycle from the beginning.

**Condition Where No Accessory Comes Out of Magazine**

- If the robot has returned empty because no accessory came out of the magazine and has come to the waiting point:

After the error is fixed, press *B (Reset Button)* on the panel to restart the accessory picking operation.

## Condition Where Screw Cannot Be Pulled to Jaw

The robot requests screw feeding from the system before the screwing operation. If the screw feeding fails, the operator should follow the steps below:

**Preliminary Check:**

- The operator should first visually check the screwing tip to confirm whether the screw has been sent or not.

**If Screw Feeding is Successful (Visual Confirmation):**

- If the screw has reached the tip and no problem is observed:

Since the line has been entered, the system safety circuits must be reset first. Then press *F (Start Button)* on the panel to continue the process from where it left off.

**If Screw Feeding Failed (Error Confirmation):**

- If it is confirmed in the visual check that the screw has not reached the tip:

Since the line has been entered, the system safety circuits must be reset first. Then press *B (Reset Button)* on the panel to retrigger the screw pulling operation.

## PassNextAccessory to Skip Current Accessory Mounting

![RG830](_media/o_PassNextAccessory.png)

If any problem is encountered during the robot's drilling, screwing, or other operations, the following steps should be followed to intervene in the process without disrupting the current workflow:

**Stopping the Operation:**
- Press E (Stop Button) on the panel. This puts the robot into waiting mode.

**Caution:** If B (Reset Button) is pressed at this stage, the entire process state is reset and the process returns to the beginning.

**Restarting the Operation and Options:**

- After stopping, when F (Start Button) is pressed, a decision page opens on the screen. The operator should choose one of the following two options at this stage:

**G:** Allows the robot to continue its operations from where it left off.

**H:** Allows the robot to cancel its current operation and proceed to the next accessory cycle.

*Critical Warning:* When option **H** is chosen, after the robot safely rescues itself, if there is a mold in the gripper, it will go to the drop point. Make sure that there is no accessory in the mold during the drop operation.

## Accessory Mounting Alarm Definitions and Solution Steps

The alarms listed below are alarm messages that may occur during mounting.

- Left/Right Magazine Accessory 1 could not go backward ! / Left/Right Magazine Accessory 1 could not go forward !
- Vertical Clamp could not go backward ! / Vertical Clamp could not go forward !
- Horizontal Clamp could not go backward ! / Horizontal Clamp could not go forward !
- Gripper Move could not go backward !
- Screw Type Valve could not go backward ! / Screw Type Valve could not go forward !
- Left/Right Screw Drop could not go backward! / Left/Right Screw Drop could not go forward!
- Screwing Axis Error !
- Screwing Axis Speed Error !
- Screwing Axis Minimum Limit Error ! / Screwing Axis Maximum Limit Error !
- Screwing Axis Lag Error !
- Axis Screw Group Minimum Limit Error ! / Axis Screw Group Maximum Limit Error !
- Axis Screw Group Lag Error !
- Screw Drop failed !
- Screw did not move to jaw or Screw detector broken !
- Right Magazine Hinge1 Left Bottom Clamp could not go backward ! / Right Magazine Hinge1 Left Bottom Clamp could not go forward !
- Right Magazine Hinge1 Left Top Clamp could not go backward ! / Right Magazine Hinge1 Left Top Clamp could not go forward !
- Right Magazine Hinge1 Right Bottom Clamp could not go backward ! / Right Magazine Hinge1 Right Bottom Clamp could not go forward !
- Right Magazine Hinge1 Right Top Clamp could not go backward ! / Right Magazine Hinge1 Right Top Clamp could not go forward !

## Condition Where Axis Gets Stuck During Movement

Sometimes the robot cannot reach the point it wants to go mathematically or gets stuck in joint limits, even if it does not hit a physical obstacle. In these cases, the steps the operator should follow to rescue are as follows:

**1. Diagnosing the Problem (Reading Error Message)**

- If you see one of the following messages on the screen, the robot has entered a "geometric" deadlock:

**"Axis Limit":** The robot has reached the last point one of its joints can rotate.

**"Singularity"** (Singularity): The robot's wrist axes (4 and 6) have aligned, the robot has lost its direction.

**"Out of Reach":** The robot's arm cannot reach that point or follow that path.

**2. Rescuing the Robot in Manual Mode (Jogging)**

![RG830](_media/ModSecim.png)

Turn the key to the right from the control unit to put it in *B (Manual Mode)*

![RG830](_media/1_6EksenSecim.png)

- When the robot gives these errors, it usually refuses to move in "Linear" (Linear) mode. To relieve the robot:

**Change Movement Mode:** Change the movement mode to "Axis" (Axis) mode via FlexPendant. When **A** is pressed, you will see that **B** part changes between axes 1-3 and 4-6.

**Manually Rotate Axes:** If there is a limit error: Rotate the axis hitting the limit in the opposite direction with the joystick. The area where the axis to be worked on should be kept in **B**, and moved by looking at the image showing how the joystick directions work on the Jogging page.

**If there is Singularity:** Slightly move the 5th axis (wrist bending) up or down to make the axes come out of alignment.

**Pull to a Safe Point:** Move the robot away from the problematic point by about 5-10 cm and take it to empty space (safe area).

**3. "Bypassing" the Operation and Continuing (Moving Program Pointer)**

![RG830](_media/o_PointerTaşıma.png)

- What the operator should actually do is to rescue the robot from that "faulty point" and manually direct it to the next safe operation step. Follow these steps:

**Open Program Editor Page:** Enter the section on FlexPendant, press **A** from the menu bar and **B** to open the Program Editor page.

**Select the Next Step:** Touch and select the line below the line where the robot got stuck or the next operation start (e.g.: MoveL or MoveJ) in the code. Visual **C**. Do not skip command lines if there are command lines in between. To avoid getting stuck in states on the PLC side.

**Move the Cursor (PP to Cursor):** Press **D** "Debug" menu **E** "PP to Cursor" (Move Program Pointer to Selected Line) option.

After these operations, it would be healthy to first run manually to observe that the operation can continue. To proceed step by step manually, hold down the **F** Motor On button on the FlexPendant as shown in the visual. As shown in Visual **H**, while you hold it down, you see the Motor On text, you can proceed with operations manually in this way. Then, Visual **G** is used to execute each line step by step, advancing one line at a time with each press. If you do not want to go step by step in Visual **G**, when you press Visual **I**, it starts scanning all lines step by step. When you want to stop while the robot is running, you can press the Visual **J** Stop button or release your hand from the Visual **F** Motor On button. After running the robot, if the robot can go to the next step by itself, after this stage, you can switch the Robot to Automatic Mode and run it again.

**Automatic Mode and Start:** Turn the key to the **K** direction shown in the visual, confirm the questions coming to the FlexPendant screen, put the system in "Auto" mode, activate the motors by pressing the **L** part shown in the visual, and after clearing the alarms in the system, give Start to continue your operations.

**Speed Control:** Keep the speed at 10%-25% level while the robot makes its first movement and monitor its path. If no problem is observed, you can set the speed back to 100%. For the speed setting page, click on the **M-N** parts shown in the visual in sequence to open the **O** speed page.

## Detailed information about parameters on the screen, screwing axis speeds

## General working principle with the line
