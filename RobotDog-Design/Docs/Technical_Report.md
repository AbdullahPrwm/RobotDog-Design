# Technical Report: Mechanical Design of a Robotic Dog

---

# 1. Introduction

This report presents the preliminary mechanical design for a simple quadruped robot (robotic dog). The design is based on the YouTube tutorial   [1DAY_1CAD] ROBOT DOG SPOT   and was implemented   without any modifications   to the original design.

The objective of this project is to understand the fundamental mechanical principles that enable a robot to stand and walk, including:
- Structural design
- Joint mechanisms
- Degrees of freedom
- Actuator selection
- Torque calculations
- Stability analysis
- Walking gaits

---

# 2. Robot Specifications and Dimensions

The following specifications are based on a scaled-down educational version of a quadruped robot:

| Specification | Value | Notes |

| Robot Type | Small Quadruped Robot | 4 legs |
| Body Length | ~300 mm | Scaled for educational project |
| Body Width | ~150 mm | Scaled for educational project |
| Standing Height | ~250 mm | Approximate height from ground to top of body |
| Total Estimated Weight | ~2.5 - 3.5 kg | Estimated for 3D-printed structure and servos |
|   Degrees of Freedom (DOF)   | 12 (3 per leg) | Hip: 2 DOF, Knee: 1 DOF |
|   Maximum Speed   | Not specified | Initial design for static walking |
|   Material   | PLA (3D printed) / Aluminum frame | For prototyping |

---

# 3. Mechanical Structure

## 3.1 Body Design
- The body is a rigid, box-like frame designed to house:
  - Battery pack
  - Control board (e.g., Arduino)
  - Power distribution system
- The design prioritizes a   low center of gravity   for stability
- Weight distribution is balanced to prevent tipping

## 3.2 Leg Design
- Four identical legs are used for simplicity
- Each leg consists of two main segments:
  -   Upper leg (Thigh):   Connects hip to knee
  -   Lower leg (Shin):   Connects knee to foot
- Legs are designed with lightweight structure to reduce load on actuators

## 3.3 Feet Design
- Rubber grips will be added to prevent slipping
- Flat base design to increase ground contact area

---

# 4. Joints and Degrees of Freedom

## 4.1 Joint Configuration
Each leg incorporates   3 active joints  :

| Joint | Type | Movement | Degrees of Freedom |

|   Hip Abduction/Adduction   | Rotational | Lateral movement (in/out) | 1 |
|   Hip Flexion/Extension   | Rotational | Forward/backward swing | 1 |
|   Knee Flexion/Extension   | Rotational | Bending the leg | 1 |

## 4.2 Total Degrees of Freedom
-   Total DOF:   12 (4 legs × 3 joints)
- This configuration provides sufficient movement for basic walking patterns

---

# 5. Actuator Selection

## 5.1 Motor Type
For the initial mechanical design,   standard high-torque hobby servo motors   are selected:
-   Model:   MG996R Servo Motor (or equivalent)
-   Torque Rating:   ~2.5 Nm (25 kg·cm) at 5V
-   Operating Voltage:   4.8V - 6.6V
-   Speed:   0.17 sec/60° at 6V

## 5.2 Selection Criteria
-   Availability:   Widely available in local markets
-   Cost:   Affordable for educational projects
-   Control:   Built-in control electronics
-   Torque:   Sufficient for the calculated requirements

## 5.3 Number of Actuators
-   Total servos required:   12 (one for each joint)

---

# 6. Torque Calculation (Hip Joint)

## 6.1 Problem Statement
The hip flexion/extension joint experiences the highest load during walking. The calculation determines the minimum torque required to support the robot's weight.

## 6.2 Assumptions
- Robot is standing on three legs (worst-case static load)
- Total robot weight:   3.0 kg  
- Each leg supports half the robot weight (1.5 kg) during lateral gait
- Leg length from hip to foot:   0.1 m  
- Leg is fully extended horizontally (max lever arm)
- Safety factor of 1.5 applied for dynamic forces

## 6.3 Static Torque Calculation

  Step 1: Calculate the weight supported by one leg  
Mass supported = 1.5 kg
F = m × g
F = 1.5 × 9.81
F = 14.71 N

  Step 2: Calculate torque at the hip joint  
τ = F × r
τ = 14.71 × 0.1
τ = 1.47 Nm


  Step 3: Account for leg's own weight  
Leg mass = 0.2 kg
τ_leg = 0.2 × 9.81 × (0.1 / 2)
τ_leg = 0.098 Nm


  Step 4: Total static torque  
τ_static = 1.47 + 0.098
τ_static = 1.57 Nm


## 6.4 Final Required Torque (with Safety Factor)
τ_required = τ_static × Safety Factor
τ_required = 1.57 × 1.5
τ_required = 2.36 Nm


## 6.5 Result Summary

| Parameter | Value |

| Static torque | 1.57 Nm |
| Required torque (with SF) |   2.36 Nm   |
| Selected servo torque |   2.5 Nm   |
| Status | ✅ Safe margin available |

---

# 7. Stability and Center of Gravity

## 7.1 Stability Principle
The robot maintains stability by ensuring the   Center of Gravity (CoG)   remains within the   Support Polygon   (the shape formed by the ground contact points).

## 7.2 Design Considerations for Stability
| Factor | Action Taken |
| :--- | :--- |
|   Low CoG   | Heavy components (battery, controller) placed at the bottom |
|   Wide Base   | Legs designed to create a wide support polygon |
|   Balanced Weight   | Symmetrical design to prevent tipping |
|   Stable Gait   | Static tripod gait ensures 3 legs always on ground |

## 7.3 Stability Analysis
- The robot will use a   static walk   (slow and deliberate)
- During walking, at least 3 legs remain on the ground
- CoG always projects within the support triangle

---

# 8. Proposed Walking Gait

## 8.1 Gait Selection
The   Static Tripod Gait   is proposed for the initial design:
- 3 legs on the ground form a stable support triangle
- 1 leg is lifted and moved forward
- This ensures stability and simplifies control

## 8.2 Movement Sequence

| Step | Action | Supporting Legs |

| 1 | Lift Leg 1 (Front Right) | Back Right, Front Left, Back Left |
| 2 | Swing Leg 1 forward | Back Right, Front Left, Back Left |
| 3 | Place Leg 1 down | All 4 legs |
| 4 | Repeat with Leg 2 (Back Left) | Front Left, Front Right, Back Right |
| 5 | Continue cycling through all legs | - |

## 8.3 Gait Parameters
-   Type:   Static Tripod Gait
-   Speed:   Slow (prioritizing stability)
-   Step length:   Small (to maintain balance)
-   Cycle time:   Determined by servo speed

## 8.4 Advantages of Static Tripod Gait
- ✅ Simple to implement
- ✅ Stable and reliable
- ✅ Easy to control with basic electronics
- ✅ Suitable for educational purposes

## 8.5 Limitations
- ❌ Slow movement
- ❌ Not suitable for dynamic walking or running
- ❌ Requires precise servo synchronization


# 9. Expected Mechanical Issues and Solutions

## 9.1 Issue List

| # | Problem | Cause | Solution |

| 1 |  Servo Overheating  | Continuous high load, inadequate cooling | Use stronger servos, reduce walking speed, add heat sinks |
| 2 |  Weak 3D-Printed Parts  | PLA may break under stress | Add support structures, use stronger materials (ABS, Nylon) |
| 3 |  Friction and Backlash  | Mechanical joints loosen over time | Use bearings, precise alignment, regular maintenance |
| 4 |  Battery Drain  | High current draw from servos | Use high-capacity battery (3000mAh+), optimize power management |
| 5 |  Slipping Feet  | Lack of grip on smooth surfaces | Add rubber grips to feet, design with better ground contact |
| 6 |  Leg Collision  | Legs hitting each other | Adjust leg length, modify gait sequence, add offsets |
| 7 |  Vibration  | Loose connections or unbalanced parts | Tighten connections, balance moving parts |

## 9.2 Mitigation Strategies
-  Design improvements:  Add fillets and supports to 3D models
-  Material selection:  Use stronger materials for high-stress parts
-  Regular maintenance:  Check and tighten connections frequently
-  Redundancy:  Have spare parts available for critical components


# 10. Tools and Software Used

| Tool | Purpose |
| :--- | :--- |
|  Tinkercad  | 3D modeling and design |
|  Fusion 360  | Advanced 3D modeling (optional) |
|  SolidWorks  | Alternative CAD software |
|  Arduino  | Control and programming (future work) |
|  Manual Calculations  | Torque and stress analysis |



# 11. References

1. **[1DAY_1CAD] ROBOT DOG SPOT** - YouTube Tutorial
   - Link: https://youtu.be/kjLXoR1G3cY?si=U-GRUs5Zdmpvn1vu
   - Date: January 24, 2021

