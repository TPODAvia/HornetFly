# HornetFly

**HornetFly** is an open engineering project for a **VTOL aircraft** designed to be **agile, fast, long-range, and autopilot-capable**, while keeping the main fuselage/body near a commanded attitude during flight.

The project covers the complete aircraft stack: **mechanical design, electronics, embedded firmware, flight control, autonomy, simulation, testing, and manufacturing**.

## Core goals

- **VTOL** — vertical takeoff, hover, transition, forward flight, and vertical landing.
- **Agile** — fast attitude and trajectory response with vectored/tilting propulsion where appropriate.
- **Fast** — efficient forward-flight configuration with low drag and high cruise speed.
- **Long range** — optimize propulsion, aerodynamics, energy storage, and mission planning for endurance.
- **Autopilot** — autonomous navigation, mission execution, stabilization, failsafes, and return-to-home.
- **Stable body attitude** — minimize unnecessary fuselage pitch/roll during translation and support commanded body-angle flight.
- **Sensor-ready** — rigid mounting for RGB, thermal, depth, LiDAR, GNSS, IMU, airspeed, and other payloads.

## Repository layout

```text
HornetFly/
├── mechanical/       CAD, airframe, mechanisms, drawings, printable parts
├── electronics/      Schematics, PCB, BOM, power system, avionics interfaces
├── firmware/         MCU, actuator, sensor, and low-level embedded firmware
├── software/         Flight control, autonomy, ROS 2, perception, drivers, tools
├── simulation/       Aerodynamics, SITL/SIL/HIL, Gazebo/Isaac/models
├── config/           Airframe, controller, sensor, network, mission configs
├── docs/             Architecture, design decisions, subsystem documentation
├── tests/            Bench, SIL, HIL, ground, transition, and flight tests
├── data/             Calibration, datasets, telemetry, and flight logs
├── manufacturing/    Gerbers, CNC, 3D-print, assembly, release outputs
├── scripts/          Build, flashing, deployment, logging, analysis utilities
└── .github/          GitHub workflows and issue templates
```

## High-level architecture

```text
Mission / Autonomy
        |
        v
Trajectory + Flight Mode Manager
        |
        v
State Estimation
(IMU/GNSS/airspeed/vision/etc.)
        |
        v
Guidance + Attitude Controller
        |
        v
Control Allocator
   |               |
   v               v
Motor thrust   Tilt/vector actuators
        |
        v
     HornetFly
```

The controller should treat **vehicle translation** and **body attitude** as separate objectives whenever the propulsion geometry allows it. This lets HornetFly remain close to level for sensing or payload missions, while still accelerating and maneuvering aggressively.

## Suggested development stages

1. **Concept / requirements** — mass, speed, range, hover time, payload, propulsion topology.
2. **Airframe CAD** — fuselage, wing, motor mounts, tilt/vector mechanisms, service access.
3. **Power & avionics** — battery, ESCs, flight controller, companion computer, sensors, telemetry.
4. **Simulation** — vehicle dynamics, actuator limits, transitions, controller development.
5. **Autopilot integration** — stabilization, navigation, mission modes, failsafes, RTH.
6. **Prototype testing** — actuator bench tests, restrained hover, transition testing, endurance tests.
7. **Production outputs** — drawings, BOM, Gerbers, manufacturing files, assembly documentation.

## Recommended flight modes

- DISARMED
- MANUAL / ACRO
- STABILIZED
- HOVER
- POSITION HOLD
- LEVEL-BODY TRANSLATION
- VTOL TRANSITION
- CRUISE
- AUTO MISSION
- RETURN-TO-HOME
- LAND
- FAILSAFE

## Autopilot direction

HornetFly is intentionally autopilot-agnostic at this stage. The repository can support integration with platforms such as **PX4 or ArduPilot**, plus an optional companion computer for perception, high-level autonomy, mission logic, and sensor fusion.

## Development rules

- Keep source files separate from generated/exported files.
- Store reusable CAD and electronics source projects in Git.
- Keep large raw telemetry/log datasets outside normal Git history where possible.
- Document electrical interfaces, actuator limits, coordinate frames, and control assumptions.
- Add test evidence for changes affecting propulsion, flight control, power, or safety.

## Status

**Early development.** Airframe geometry, propulsion topology, actuator layout, avionics, aerodynamic targets, and final autonomy stack are still open for iteration.
