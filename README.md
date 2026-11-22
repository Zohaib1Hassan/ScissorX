# Mini Scissor Lift (3D-printable, screw-driven)

Parametric CAD (CadQuery) + a kinematics/statics calculation for a small hand-cranked scissor lift.

## Key numbers (calculated, not measured)
| | |
|---|---|
| Platform height | 64.0 mm collapsed -> 126.9 mm extended (stroke 62.9 mm, 1.98x) |
| Link length / section | 120 mm pin-to-pin, 12 x 4 mm, 4 mm pins, 2 link pairs |
| Lead screw | M3 x 0.5 mm pitch, 52.8 mm slider travel = 105.5 knob turns |
| Rated load (design) | 9.0 kg, evenly distributed |
| Max screw force | 242.6 N (collapsed, 20 deg) |
| Max raising torque | 68.6 N*mm |
| Minimum safety factor | 2.01 (link bending+axial 17.4 MPa; pin bearing 7.7 MPa; vs 35 MPa PLA) |

## Method
Planar statics of one X-stage; load split between two sides. Each link is solved as a free body
(6 unknown reactions, 6 equations). Check: screw force equals W / tan(theta) (max difference 0.0 N).
Link stress = N/A + M*c/I at the net section through the pin hole (hole = pin + 0.2 mm), at mid-span.
Bearing stress = pin shear force / (pin diameter x link thickness).
Screw torque: T = F*(d_m/2)*(l + pi*mu*d_m)/(pi*d_m - mu*l), d_m = 2.675 mm, mu = 0.15.

## Assumptions
PLA yield 35 MPa (conservative for FDM, layers oriented along links); friction in pins neglected;
platform rigid; rated load is the largest 0.5 kg step with SF >= 2 over the full stroke.
Slender-link buckling and print-orientation anisotropy are not modelled. No physical testing was done.

## Files
scissor_lift.py (CAD) - sim.py (calculation) - render.py (previews) - stl/ step/ - simulation_results.csv
Run: `pip install cadquery numpy matplotlib` then `python scissor_lift.py`, `python sim.py`.
