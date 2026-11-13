# MacPherson Strut Suspension — Engineering Diagram & Physics Simulator

A single-file, zero-dependency interactive automotive engineering cutaway diagram and real-time half-car physics simulator (`macpherson_suspension_sim.html`). Designed for students, mechanics, and vehicle dynamics enthusiasts, it visualizes how front MacPherson strut suspension components articulate, deform, and transfer loads across bumps, potholes, cornering maneuvers, and component failures.

---

## Key Features

### 1. Interactive High-DPI Cutaway CAD Diagram
- **MacPherson Struts & Helical Coil Springs**: Cutaway hydraulic damper tubes showing internal fluid levels, moving piston valves, chrome piston rods, progressive urethane bump stops, and dynamic helical coil springs that change color under high compression.
- **Upper Strut Mounts & Bearing Plates**: Rubber-isolated upper strut tower mounts that flex under vertical shock loads and allow steering axis rotation.
- **Lower Control Arms (LCA) & Ball Joints**: Pivoting lateral control arms swinging through true circular arcs, dynamically altering wheel camber and track geometry.
- **Anti-Roll (Sway) Bar & End Links**: U-shaped spring-steel torsion bar coupled to the strut housings via ball-joint end links, glowing dynamically from cyan to amber to rose as torsional stress increases.
- **Elastomeric Bushings**: Deformable subframe pivot and D-bracket bushings supporting **OEM Rubber** ($1.0\times$), **Stiff Polyurethane** ($2.4\times$), and **Worn / Loose** ($0.45\times$ stiffness with radial free play) compounds.
- **Interactive Inspection & Overlays**: Hover or click any part on the diagram (or use the toolbar pills) to highlight the assembly, inspect live telemetry, and toggle callout labels or real-time tire/sway-bar force vectors.

### 2. Real-Time Half-Car Physics Engine
- **4-DOF Equilibrium-Centered Dynamics**: Integrates sprung chassis heave ($z_{\text{chassis}}$), chassis roll angle ($\phi$), and independent left/right unsprung wheel vertical positions ($z_{\text{wheel},L}$, $z_{\text{wheel},R}$) around static ride-height equilibrium using velocity-first Symplectic Euler integration across $8$ sub-steps per frame ($\Delta t \le 0.033\text{ s}$).
- **Asymmetric Hydraulic Damping**: Models realistic twin-tube/monotube damper valving where rebound damping ($1.48\times$) is stiffer than compression damping ($0.72\times$).
- **Blown Shock Failure Simulation**: Simulates blown Left, Right, or Both shocks by dropping damping efficiency to $3\%$, aerating internal hydraulic fluid with visible foam bubbles, leaking oil droplets down the strut housing, and triggering prolonged resonant bounce and bump-stop bottoming.
- **Unilateral Tire Contact & Travel Stops**: Tires support static vehicle preload ($W_T$) and can lift airborne over sharp crests before landing back onto the road surface, while progressive bump stops ($> +65\text{ mm}$) and droop stops ($< -75\text{ mm}$) prevent mechanical over-travel.

### 3. Live Telemetry & 4-Channel Oscilloscope
- **Heads-Up Display (HUD)**: Live readouts for Chassis Heave ($\text{mm}$), Body Roll ($^\circ$), Lateral Acceleration ($\text{G}$), Longitudinal Acceleration ($\text{G}$), Sway Bar Torque ($\text{N}\cdot\text{m}$), Strut Health, and Bushing Compound.
- **Component Inspector**: Context-sensitive engineering panel displaying real-time travel, damper forces, piston velocities, dynamic camber, control arm angles, and elastomer strain for whichever component is selected.
- **4-Channel Scrolling Oscilloscope**: Plots real-time waveforms for **Chassis Heave** ($\text{mm}$), **Left & Right Wheel Travel** ($\text{mm}$), **Body Roll Angle** ($^\circ$), and **Peak Damper Force** ($\text{kN}$), alongside effective damping ratio ($\zeta$) diagnostics and bump-stop bottoming warnings.

---

## Quick Start & Usage

1. Download or save `macpherson_suspension_sim.html` locally.
2. Open `macpherson_suspension_sim.html` directly in any modern desktop or mobile web browser (Chrome, Edge, Firefox, or Safari).
3. **No installation, build step, server, or internet connection is required**—all styling, physics, and High-DPI canvas rendering are self-contained inside the single HTML file.

---

## Controls & Simulation Modes

| Control Group | Options & Parameters | Engineering Effect |
| :--- | :--- | :--- |
| **Quick Presets** | `Healthy OEM`, `Blown Left Shock`, `Track Stiff`, `No Sway Bar`, `Worn Bushings` | One-click configurations demonstrating common suspension setups and mechanical faults. |
| **Playback Controls** | `Pause / Resume`, `0.5x Slow-Mo`, `Reset` | Freeze motion mid-impact, inspect fast wheel-hop oscillations in slow motion, or return to static equilibrium. |
| **1. Shock Tuning & Faults** | Shock Stiffness ($0\%\text{--}100\%$), Blown Shock (`None`, `Left`, `Right`, `Both`), Coil Spring Rate ($50\%\text{--}150\%$), Sway Bar Stiffness ($0\%\text{--}150\%$), Bushing Compound (`OEM Rubber`, `Polyurethane`, `Worn / Loose`) | Tunes natural ride frequency, damping ratio ($\zeta$), roll stiffness, and bushing compliance/slop. |
| **2. Road & Impulses** | Continuous Roads (`Smooth`, `Speed Bumps`, `Potholes`, `Washboard`, `Curb Drop`), One-Shot Triggers (`Left Bump`, `Right Bump`, `Both Bumps`, `Left Pothole`, `Bounce Test`), Vehicle Speed ($0\text{--}80\text{ mph}$) | Generates continuous terrain profiles or isolated single-wheel/dual-wheel road disturbances and chassis drop tests. |
| **3. Driving Maneuvers** | Steering (`Straight`, `Left Turn`, `Right Turn`, `Auto Slalom`, manual slider), Longitudinal Load (`Cruise`, `Hard Braking`, `Hard Accel`) | Applies lateral cornering roll torque ($\text{G}$-load weight transfer) and longitudinal brake dive / throttle lift. |

---

## Reference Vehicle & Physics Parameters

The simulation uses representative front-axle parameters for a mid-size passenger sedan:

$$\begin{aligned}
M_S &= 720\text{ kg} && \text{(Front sprung mass)} \\
M_U &= 42\text{ kg} && \text{(Unsprung mass per corner)} \\
I_{\text{roll}} &= 255\text{ kg}\cdot\text{m}^2 && \text{(Front half-car roll inertia)} \\
t_{1/2} &= 0.76\text{ m} && \text{(Half-track width)} \\
h_{\text{CG}} &= 0.52\text{ m} && \text{(Center of gravity height above roll axis)} \\
K_{\text{spring,nom}} &= 45,000\text{ N/m} && \text{(Nominal coil spring rate, } 45\text{ N/mm)} \\
K_{\text{sway,nom}} &= 22,000\text{ N/m} && \text{(Nominal anti-roll bar rate at wheel)} \\
C_{\text{damper,nom}} &= 5,600\text{ N}\cdot\text{s/m} && \text{(Nominal hydraulic damping coefficient)} \\
K_{\text{tire}} &= 215,000\text{ N/m} && \text{(Vertical tire carcass stiffness)}
\end{aligned}$$

---

## Project Structure

```text
├── macpherson_suspension_sim.html   # Complete self-contained application (HTML + CSS + Canvas Physics Engine)
└── README.md                        # Project overview, physics specification, and user guide
```
