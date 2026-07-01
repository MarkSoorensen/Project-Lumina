# 05 – Light Fibre System

> **Status:** 🟡 Research in Progress

## Purpose

This document contains the reverse engineering work for the Volkswagen ID.7 front light fibre system and illuminated front emblem retrofit.

---

# Components

| ID | Description |
|----|-------------|
| MX16 | Illuminated Front Emblem |
| L362 | Right radiator grille contour light |
| L363 | Left radiator grille contour light |
| L377 | Left DRL LED module |
| L378 | Right DRL LED module |
| T14j | Vehicle ↔ Front bumper transition connector |
| T4dh | Connector at light fibre |
| T4df | Intermediate connector |
| T4o | Harness connector |

---

# Confirmed Findings

## MX16

Confirmed from Volkswagen Current Flow Diagrams:

| Pin | Function | Wire colour |
|-----|----------|-------------|
| 1 | Ground | br/sw |
| 2 | KL58 | gr/ge |

MX16 is a simple 2-pin module.

---

## L362

Current observations:

- Uses a 4-pin connector.
- Contains internal electronics.
- Does **not** share the same wiring architecture as MX16.

Current wire colours:

| Pin | Colour |
|-----|--------|
|1|ws/bl|
|2|gn/bl|
|3|bl/rt|
|4|bl|

---

## Shared Ground

Confirmed:

- Ground point 456
- Ground point 457

are shared by:

- MX16
- L377
- L378

---

# OEM Parts

Known part numbers:

| Part | Description |
|------|-------------|
|14A971095AQ|Front bumper wiring harness|
|14A971014|Intermediate light fibre harness|

The exact electrical difference between illuminated and non-illuminated vehicles is still under investigation.

---

# Current Working Theory

🟡 The front emblem requires only:

- KL58
- Ground

The grille light fibre appears to be controlled through dedicated signal lines and an internal driver.

Further measurements are required before recommending any wiring modification.

---

# Planned Measurements

- Measure T4dh with connector connected.
- Measure each pin against chassis ground.
- Measure between all four conductors.
- Verify behaviour with parking lights OFF / ON.

---

# Future Work

- Verify populated terminals at T14j.
- Compare illuminated vs non-illuminated bumper harness.
- Investigate BCM coding.
- Verify retrofit without replacing the complete harness.

---

_Last updated during Project Lumina reverse engineering._
