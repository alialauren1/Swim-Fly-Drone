# Swim Fly Drone Project

Our project entails constructing a submersible chamber capable of reaching
specified depths. The system will operate in a closed loop, maintaining control until it 
reaches a desired pressure depth.

This project was intended for our senior project where. Dr. Ghalamchi wants to improve previous tests on waterproof drones that can take off from underwater to allow for a drone that can float on top of the water surface as well as have added support to be pushed up from underwater. The new design needs to be detachable from the built waterproof drone to compare its new features in tests. The propellers must also be above the water surface when the drone is idling on the water so that the efficiency of takeoff can be compared to the drone without the chamber in which the whole drone is submerged underwater upon takeoff.

Our project for ME 405 will be the system attached to this drone, enabling the drone to submerge underwater with a minimum depth of 5ft. While allowing for the system to resurface and position the propellers above the water's surface. 

Pressure can be directly correlated to depth, given a liquid's density.
   In order to simulate this system for our ME 405 Term Project, this system takes a desired pressure setpoint and controls a motor-driven syringe system to
   pressurize a chamber to the setpoint. It waits a period of time, as if it were underwater collecting data,
   and then returns to the initial pressure, as if it were returning to the water surface. 

## Hardware design
In Figure 1, we can see the internal system of the system. We have integrated Ametck Pittman's PG6712A077-R3 motor to a 50 CC syringe. Utilizing this motor, we've have attached a worm gear and gears to ensure sufficient torque to be generated. These gears are attached to a pinion
and aligned with a rack that allows for the syringe to be moved back and forth. This allows
for the system to achieve the desired weight to submerge the whole system.

The gears were selected from McMaster. This is so in the future, they can be ordered parts. For now, we used the CAD files to 3D print them for budget reasons. While sizing and choosing the number of teeth we would need for our system, we calculated to torque that the motor needed to have to overcome the friction force between the piston and syringe. This calculation is shown below. In the future, we can order a motor that is more selectively chosen using this information. However for now, we used the motor provided to us in lab. 

$F_r = T_A / R_A$

$T_A = F_R * R_A$

$T_B = T_A$

$T_C = (N_C / N_B ) * T_B$

$T_C = (N_C / N_B ) * (F_R * R_A)$

$T_C = (1/15) * (6 N) * (.0152 m)$

$T_C = (0.006 Nm) = (6 mNm)$ 

Doing these calculations led us to select appropriate gears for our system, ensuring that they can withstand the pressure encountered during operation while maintaining an ideal speed. Below shows a table of the parameters.  

|           **Parameters**           |   Variable   |   Value   |   Units   |
|:----------------------------------:|:------------:|:---------:|:---------:|
|    **----Rack+Piston+Syringe--**   |  **-------** |  **----** |  **----** |
| Force to overcome friction in tube |      F_R     |     6     |     N     |
|           **----Gears--**          |  **-------** | **-----** | **-----** |
|            Radius Gear A           |      R_A     |   0.0152  |     m     |
|            Teeth Gear A            |      N_A     |     17    |           |
|     Outer Diameter Worm Gear B     |     OD_B     |     16    |     mm    |
|          Teeth Worm Gear B         |      N_B     |     15    |           |
|     Pressure Angle Worm Gear B     |     Phi_C    |     20    |  degrees  |
|        Outer Diameter Worm C       |     OD_C     |     12    |     mm    |
|        Pressure Angle Worm C       |     Phi_C    |     20    |  degrees  |
|            Teeth Worm C            |      N_C     |     1     |           |
|   **-----Motor Parameters------**  | **--------** | **-----** |  **----** |
|        Radius of Motor Gear        |      rm      |  0.00662  |     m     |
|        Motor Nominal Voltage       |     V_DC     |     12    |     V     |


![pic 3](https://github.com/alialauren1/ME405-Term-Project/assets/157066050/dabea663-33ab-48a3-91b7-2d57c6a7cb01)

Figure 1. CAD: Internal system of our terms project with labels indicating parts of the system.

![PIC 4](https://github.com/alialauren1/ME405-Term-Project/assets/157066050/eb48edbe-51e1-428f-be92-7078a6765a94)

Figure 2. CAD: Secondary view of the internal system of our terms project with labels indicating parts of the system.

![Screenshot 2024-03-19 at 6 15 07 PM](https://github.com/alialauren1/ME405-Term-Project/assets/157066441/7a1a9980-e30d-4ffa-95b8-1a75b6fceadd)

Figure 3. Gears, motor, and frame for the internal system.

The pressure sensor we selected is the SSCMANV030PA2A3 Honeywell Pressure Sensor. It measures absolute pressure, with a range from 0-30 psi. Is allows liquid media on the port, which will come of use in future quarters when we test our system underwater. 

<img width="182" alt="Screenshot 2024-03-19 at 8 53 00 PM" src="https://github.com/alialauren1/ME405-Term-Project/assets/157066441/83f965b6-e449-474c-9980-f4381207573f">


Figure 4. SSCMANV030PA2A3 Honeywell Pressure Sensor

![IMG_6037](https://github.com/alialauren1/ME405-Term-Project/assets/157066441/d11b0a8d-c261-4473-9286-de9a2c53cbf4)

Figure 5. Hardware all connected

![IMG_5986](https://github.com/alialauren1/ME405-Term-Project/assets/157066441/2dcb67c6-f8fc-4aed-8ba3-724c25d5ca32)

Figure 6A. System Connected to Bottom of Drone Body - View 1

![IMG_5952](https://github.com/alialauren1/ME405-Term-Project/assets/157066441/372ee37b-0d7c-4a9a-8496-3acea0664945)

Figure 6B. System Connected to Bottom of Drone Body - View 2

<img width="561" alt="Screenshot 2024-03-19 at 8 43 37 PM" src="https://github.com/alialauren1/ME405-Term-Project/assets/157066441/63960632-6290-4ac7-8c0b-4ce70331d5dc">

Figure 7. Overall View of Drone Body with Chamber 

### Schematic

The schematic below shows a very general diagram of how components are being powered and communicating with one another. 
The power supply provides power to the motor. The power supply was set to 12V with a 0.5 A current limit. 

<img width="355" alt="Schematic" src="https://github.com/alialauren1/ME405-Term-Project/assets/157066441/69f9537e-9c2f-4ec5-904a-f615c2763568">

Figure 8. Schematic of components

## Software design
The main program uses three classes inside two tasks that multitask with one another. A detailed description of the software design can be found on our doxygen main page linked here: 
https://alialauren1.github.io/ME405-Term-Project/index.html#soft_org_sec

To measure pressure, we used a Honeywell Board Mount Pressure Sensor, which uses I^2C communication. A class was made to use this sensor. Details on how the data was collected and process is linked below. Pressure Sensor: SSCMANV030PA2A3
https://alialauren1.github.io/ME405-Term-Project/index.html#autotoc_md1

Attaching the sensor and the Ametek motor to our Nucleo, we were able to program both components to get a functioning product.

### Tasks and States
The Tasks and States used in the main program are shown in diagrams linked on the page below.
https://alialauren1.github.io/ME405-Term-Project/index.html#T_S_sec

## Testing and Results

### Preliminary
Our senior project requires our chamber to be able to acheive at minimum, 5 ft depth. Calculations were run, shown below, to determine the pressure that coincides with a depth of 5 ft in water. Being a little under 16.5 psi, we decided to run initial tests at 16.5 psi.

<img width="558" alt="Screenshot 2024-03-19 at 9 05 30 PM" src="https://github.com/alialauren1/ME405-Term-Project/assets/157066441/ff3288be-28b8-42c2-b472-b3d4093e939d">

In order to test our project sensors and motor control, we ran multiple tests in order to find our optimal Kp value. The results are presented in the plot down below. This was preliminary testing. 

<img width="605" alt="Screenshot 2024-03-17 at 10 32 32 PM" src="https://github.com/alialauren1/ME405-Term-Project/assets/157066441/ac451cf5-9cc9-4dc5-884a-5c23263242ac">

Figure 9. Plot of Pressure vs Time inside the syringe. Each line represents a different run of data collected while altering the Kp value.

During our testing, we initially set Kp to 5 (shown in blue) and then increased it to 10 (shown in orange). Observing the graph, it's evident that increasing the Kp value led to faster attainment of the target pressure of 16.5 [psi].

While testing to achieve for efficiency in reaching the desired pressure, it's essential to consider what our system will be attached to. Our system with the syringe and pressure sensor will be attached to a drone. Rapid pressure and volume changes may introduce a moment within the drone body, causing the drone to loose control. Therefore, we must weigh the trade-offs between achieving rapid pressure targets and maintaining system stability.

As we continue to test our project, further tests will be necessary to determine the optimal balance between speed, the system stability and accuracy. This process may involve fine-tuning parameters beyond just changing the Kp. This may incude making the chamber of the system bigger and other factors.

### Lab Demo Results and Functionality of Product
The below plot shows the pressure inside the syringe. The autonomous journey is one in which the system reaches the desired setpoint, waits for a duration, and then returns to the initial pressure. 

<img width="360" alt="image" src="https://github.com/alialauren1/ME405-Term-Project/assets/157066441/75d0b395-c743-4855-a188-f06f3c17799e">

Figure 10. Plot of Pressure vs Time inside the syringe with a setpoint of 17 [psi].  

This journey mimics future developement of our larger senior project in which this pressure chamber will be attached to a drone. We anticipate it will be beneficial for some remote or signal to send a desired depth as the setpoint to the system, in which the chamber will submerge with the drone, going to that depth. It will remain there, possible to collect data, and then autonomously return to the surface. 
We are satisfied with the final results. The chamber is able to reach pressures higher than a pressure corresponding to 5ft, which was what we wanted to achieve.
It is also able to maintain the increase in pressure while the motor is turned off, which is a satisfying result. 

The system also works at lower than atmosphere pressures. In the plot below, the setpoint was chosen as 13 psi. However, in another test, we were able run the system with an even lower setpoint of 10 psi. Although this is less necessary to have, it is satisfying to see that ability. 

<img width="349" alt="Screenshot 2024-03-19 at 8 38 33 PM" src="https://github.com/alialauren1/ME405-Term-Project/assets/157066441/a8d9b7e9-7423-4f52-975f-87fc786d1f34">

Figure 11. Plot of Pressure vs Time inside the syringe with a setpoint of 13 [psi].  

## What we have learned
Designing this system taught us how important it is to design and test early. 
Although most of the system was done with a reasonable amount of time, we were faced with issues causing the system to take longer to complete than anticipated.

### 3D Printing
While 3D printing gears and housing system for our project we learned that tolerances while creating parts is harder to achieve. When 3D printing the gears it was harder to align the gears causing the small gears to slip and not allowing for our system to be as efficient as it can be.

Note: We are saving our used PLA parts to find a place to recycle them. 

![Screenshot 2024-03-19 at 6 14 47 PM](https://github.com/alialauren1/ME405-Term-Project/assets/157066441/54fc154a-4143-4713-95bc-231fa4f20410)

Figure 12. Collection of gears tested

### Software and Sensors
We learned that the data being output from our pressure sensor was in counts. This led to the creation of a definition in our PressureSensor class to interpret the counts into a unit of measurement that could be easily interpretted, that being [psi]. Since our Closed-Loop Controller class uses the pressure sensor output in counts to correct for a desired pressure, an additional definition was made to interpret user desired setpoint input from [psi] to counts. 

## Safety
Our project prioritizes user safety through thoughtful design considerations. By utilizing small gears, we have effectively reduced the risk of injuries to the user. Once the system has been fully assembled, all moving components and electrical elements will be enclosed and inaccessible to the user. This design ensures that users are protected from potential hazards during the system's operation.

## Bugs and Future Work

We would also like to fix our code in Task2 State 3 where there is a break in data collection between the chamber resting at a higher pressure and then returning to its original pressure. As shown on the plot in the "Lab Demo Results" section, there is a small duration of time in which no data is collected. That is state 3, whilst counter_s3 is between 1 and 3. We tried removing this portion and only having state 3 reset the setpoint to initial pressure in one count but it did not initially work and we have run out of time to work on the code. So, for now, there is that small time duration blip in the data.  

In the future we would like to implement a third task into our main program that is a user interface for the pressure setpoint. 
The user could select from a range of setpoint options and the system would adjust the pressure in the chamber accordingly. 
This task would multitask with the other two tasks and allow for the user to input a setpoint whenever they want whilst the program runs. 

We plan to build a larger waterproof chamber to encompass components similar to those used in project. This will allows us to test the systems depth control abilities in actual water. We look forward to the continuation of this project and appreciate all that it has taught us so far. 

## Additional files

Pressure sensor datasheet:
[SSCMANV030PA2A3 Honeywell.pdf](https://github.com/alialauren1/ME405-Term-Project/files/14630972/SSCMANV030PA2A3.Honeywell.pdf)

I2C Communications with Honeywell Pressure Sensors:
[sps-siot-i2c-comms-digital-output-pressure-sensors-tn-008201-3-en-ciid-45841.pdf](https://github.com/alialauren1/ME405-Term-Project/files/14630975/sps-siot-i2c-comms-digital-output-pressure-sensors-tn-008201-3-en-ciid-45841.pdf)
 
