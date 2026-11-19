# Beam Designer

## Purpose

Create a clean, professional, single-page beam-analysis app. The app will analyze
a simply supported or cantilever beam, draw shear, moment, and deflection
diagrams, and check whether the selected member is strong and stiff enough.

The app is for learning and preliminary analysis. It must not be presented as
approval for final structural design.

## Scope and assumptions

- Supports: simply supported and cantilever.
- Member behavior: prismatic, linearly elastic, and homogeneous along the span.
- Span is measured in feet horizontally from the left end of the beam.
- Loading is vertical and downward.
- Shear deformation is ignored.
- The member self-weight is ignored.
- One load may be present at a time:
  - A point load, or
  - A full-span uniformly distributed load.
- Point loads are entered as magnitude and as distance from the left support.
- Uniform loads are entered as magnitude and apply across the full span.
- Buckling, torsion, combined stresses, connection design, and continuous beams
  are outside scope.

## Units

- Span: ft
- Point load: kip
- Uniform load: kip/ft
- Bending moment: kip-ft
- Stress: ksi
- Modulus of elasticity: ksi
- Section modulus: in³
- Moment of inertia: in⁴
- Deflection: in

## Inputs

### Beam

- Support condition: simply supported or cantilever
- Span length in feet

### Load

- Load type: point load or full-span uniform load
- Point-load magnitude in kip and location in ft from the left support
- Uniform-load magnitude in kip/ft

### Member

- Member type: steel W-shape or lumber

For steel members:

- Section selected from a built-in teaching list of about ten common W-shapes
- Built-in properties include moment of inertia `I`, section modulus `S`,
  modulus of elasticity `E`, and allowable bending stress

For lumber:

- Common nominal 2-inch and 4-inch sizes
- Species and grade selected by dropdown
- Built-in dimensions, moment of inertia, section modulus, modulus of
  elasticity, and allowable bending stress

The app will use one built-in combination of member properties and allowable
stress at a time. It will not accept separate user-entered member properties.

## Engineering calculations

The app will calculate:

- Support reactions
- Maximum positive and negative shear
- Maximum positive and negative bending moment
- Deflection along the beam

It will assume the following sign convention:

- Positive shear is upward force on the left face of a cut
- Positive moment produces sagging
- Positive deflection is downward
- Point and distributed loads act downward

The bending stress is calculated as:

`fb = Mmax / S`

where `Mmax` is the controlling maximum absolute bending moment. The bending
check is:

`fb <= allowable bending stress`

The deflection limit is `L / 360`, using span `L` in inches. The deflection
check location is:

- Midspan for simply supported beams
- The free end for cantilever beams

The bending and deflection percentages will be based on the controlling
allowable stress and `L / 360`, respectively.

## Outputs

The app will display:

- Beam geometry and the selected load
- Support locations
- Reactions
- Maximum shear
- Maximum bending moment
- Shear, moment, and deflection diagrams
- Controlling bending stress
- Maximum checked deflection
- Deflection limit
- Separate pass/fail results for bending and deflection

Each diagram will include:

- Labeled axes and units
- Labeled maximum and minimum values
- Support and load labels on the beam sketch
- Pass/fail markers where applicable

## Interface behavior

- The app recalculates automatically as valid inputs change.
- The opening state will load the W12×26 uniform-load example.
- Invalid, missing, or unsupported inputs will produce an inline warning.
- When an edit is invalid, the app will retain the previous valid results and
  visibly mark them as the last valid result set.
- The app will not overwrite or clear diagram areas while waiting for valid
  input.
- It will be usable on desktop and mobile browsers.
- The interface will be clean and professional.

## Opening example

The app opens with:

- Simply supported beam
- 20 ft span
- Full-span uniform load of 1 kip/ft
- W12×26 steel section

The expected result for this validation case is:

- Maximum moment: 50.0 kip-ft
- Midspan deflection: 0.609 in

## Validation

### W12×26 simply supported beam

- Span: 20 ft
- Support: simply supported
- Load: 1 kip/ft full-span uniform load
- Member: W12×26
- Expected maximum moment: 50.0 kip-ft
- Expected midspan deflection: 0.609 in

### Simply supported off-center point load

Include an off-center point load with a known hand-calculation result in
`02_validation/`. Add the reaction, maximum moment, and deflection expected
values after hand calculations are complete.

### Cantilever point load

Include a cantilever point load with a known hand-calculation result in
`02_validation/`. Add the reaction, maximum moment, and free-end deflection
expected values after hand calculations are complete.

## Out of scope

- Continuous beams
- Fixed-end beams other than the cantilever boundary condition
- Partial uniform loads
- Multiple loads acting simultaneously
- Buckling
- Shear deformation
- Combined steel and lumber selection
- User-entered member properties
