# E30 Teardown

A scroll-driven 3D teardown of the BMW E30 3 Series in one HTML file.

**Live:** https://lincolnchoi9.github.io/motiondesigntest/

Scrolling moves the teardown along. Each section of the page is one stage:

| # | Stage | What happens |
|---|-------|--------------|
| 00 | Intro | The assembled car, built from code |
| 01 | Shell | The unibody lifts off the subframes in one piece and turns into an x-ray ghost |
| 02 | Engine | The M20 straight-six comes out and explodes: block, head, belt-driven cam, 12 valves, crank, pistons |
| 03 | Drivetrain | Clutch, Getrag gearbox, two-piece driveshaft and differential laid out in a line, with gear sizes taken from the ratios |
| 04 | Suspension | Front struts and rear semi-trailing arms move through bump and droop, with camber and toe solved from the pivot geometry |
| 05 | Power flow | Fuel and spark, then crank, gearbox and rear wheels, with live rpm, gear, speed and torque. The flow reverses under engine braking |
| 06 | Model years | Pick a year from 1982 to 1991 and the car rebuilds: chrome or polyurethane bumpers, trim, tail lamps, engine, gearing and optional M3 box flares |
| 07 | Spec sheet | Every figure, generated from the same spec model |

## One spec model

Everything comes from the `SPEC` object near the top of the script, through `resolve(cfg)`:

- **Geometry:** body dimensions, wheelbase and track, arch size from the tyre, bore, stroke, rod length, clutch diameter, and gear radii from the ratios.
- **Motion:** the slider-crank kinematics, cam phasing from the firing order, and valve timing.
- **Numbers:** displacement from bore and stroke, road speed from gearing and tyre size, wheel torque from the torque curve and the ratios, and camber change from the suspension pivots.
- **Text:** labels, copy, HUD readouts and the spec sheet all read from the resolved model.

Change a value in `SPEC` and the car, the readouts and the page text all follow.

## Run it locally

ES modules need an HTTP server, so opening the file directly won't work:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000. Add `?debug` to the URL to expose `window.__e30` for frame timing and stepping.

## Tech

- [Three.js](https://threejs.org) r160, loaded from jsDelivr through an import map. There's no build step.
- All geometry is procedural, with no model files: extruded profiles, lathes, tubes and swept surfaces.
- HTML callouts are projected from 3D anchors and laid out in columns so they don't overlap.

## Accuracy

Figures are period manufacturer data where available. Kerb weights are approximate and marked ≈. The torque curve is a smooth model fitted through the published peak torque and peak power points. The 3D motion runs in slow motion; the readouts use real values.

This is an unofficial fan project, not affiliated with or endorsed by BMW AG.
