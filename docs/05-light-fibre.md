# Light Fibre System

> **Document Version:** Draft v0.5
>
> **Project:** Project Lumina
>
> **Status:** 🟡 Research in Progress

---

# Overview

The Volkswagen ID.7 illuminated front emblem is not an isolated lighting component.

Instead, it forms part of the vehicle's exterior contour lighting architecture together with the illuminated grille light fibres.

The purpose of this document is to reverse engineer the original Volkswagen implementation and document every confirmed engineering finding.

Unlike a traditional retrofit guide, this document separates confirmed facts from engineering theories and measured data.

---

# Research Status

| Category | Status |
|-----------|----------|
| Official Workshop Manual | ✅ |
| Current Flow Diagrams | ✅ |
| OEM Parts | 🟡 |
| Physical Measurements | 🟡 |
| Wiring Verification | 🔴 |
| BCM Coding | 🟡 |

---

# Engineering Method

Throughout Project Lumina every statement belongs to one of three categories.

---

## 🟢 Confirmed

Verified using one or more of:

- Official Volkswagen Current Flow Diagrams
- Official Workshop Manual
- OEM Parts Catalogue
- Physical Verification
- Measured Values

---

## 🟡 Working Theory

Supported by engineering evidence but still awaiting physical verification.

---

## 🔴 Unknown

No reliable engineering evidence currently exists.

Unknown sections remain documented to simplify future research.

---

# System Architecture

The illuminated front lighting system consists of multiple independent components.

```text
                   J519
                    │
                    │
                Vehicle Harness
                    │
                  T14j
                    │
        ┌───────────┴────────────┐
        │                        │
        │                        │
    Bumper Harness          Headlamp
        │                        │
        │                        │
      T4o                    MX2 / MX3
        │
      T4df
        │
      T4dh
        │
      L362 / L363
```

The illuminated emblem (MX16) is documented separately and does not appear to share the same connector architecture as the Light Fibre modules.

---

# Main Components

The following components have currently been identified.

| Component | Description | Status |
|------------|-------------|--------|
| MX16 | Illuminated Front Emblem | 🟢 Confirmed |
| L362 | Right Radiator Grille Contour Lighting | 🟢 Confirmed |
| L363 | Left Radiator Grille Contour Lighting | 🟢 Confirmed |
| L377 | Left DRL Module | 🟢 Confirmed |
| L378 | Right DRL Module | 🟢 Confirmed |
| T14j | Vehicle ↔ Front Bumper Connector | 🟢 Confirmed |
| T4o | Intermediate Connector | 🟢 Confirmed |
| T4df | Intermediate Connector | 🟢 Confirmed |
| T4dh | Light Fibre Connector | 🟢 Confirmed |

---

# MX16 — Illuminated Front Emblem

The Current Flow Diagrams identify the illuminated emblem as component **MX16**.

Unlike the Light Fibre modules, MX16 uses a simple two-pin connector.

Current documentation confirms the following pin assignment.

| Pin | Function | Wire |
|------|----------|------|
| 1 | Ground | br/sw |
| 2 | KL58 | gr/ge |

No LIN, CAN or dedicated communication bus is shown.

The emblem therefore appears electrically simple and behaves as a conventional illumination module.

Current theory suggests that internal LED electronics are integrated into the emblem assembly.

Further measurements are required.

---

# L362 — Right Radiator Grille Contour Lighting

L362 forms part of the illuminated grille assembly.

Unlike MX16 it uses a four-pin connector.

Current documentation identifies the following wire colours.

| Pin | Wire Colour |
|------|-------------|
| 1 | ws/bl |
| 2 | gn/bl |
| 3 | bl/rt |
| 4 | bl |

At the time of writing Volkswagen does not publish a dedicated connector pin assignment for these four conductors.

Instead the wiring must be reconstructed from the Current Flow Diagrams together with physical measurements.

This remains one of the primary goals of Project Lumina.

---

# L363 — Left Radiator Grille Contour Lighting

L363 is the left-hand counterpart to L362.

Volkswagen documents both modules as individual components despite them performing the same function.

Current evidence indicates that both Light Fibre modules share the same electrical architecture.

No differences in connector type have currently been identified.

Current status:

| Property | Status |
|----------|--------|
| Component identified | ✅ |
| Connector identified | 🟢 |
| Wiring verified | 🟡 |
| Physical measurements | 🔴 |

Future measurements will verify whether the left and right modules are electrically identical.

---

# L377 — Left DRL Module

L377 is documented as the left daytime running light module.

Unlike MX16, Volkswagen documents only two electrical connections.

| Pin | Function |
|------|----------|
| 1 | Ground |
| 2 | SIG |

The Current Flow Diagram labels the positive conductor as **SIG** rather than KL58.

The exact meaning of SIG has not yet been verified.

Current theories include:

- PWM controlled lighting output
- Driver output from headlamp electronics
- Diagnostic capable output

No evidence currently suggests LIN communication.

---

# L378 — Right DRL Module

L378 is electrically equivalent to L377.

Documented wiring:

| Pin | Function |
|------|----------|
| 1 | Ground |
| 2 | SIG |

The shared architecture between L377 and L378 strongly suggests that both DRL modules are controlled by the same electrical strategy.

---

# T14j — Vehicle to Front Bumper Connector

One of the most important discoveries during Project Lumina is connector **T14j**.

This connector forms the electrical transition between the vehicle wiring harness and the front bumper harness.

Current Flow Diagrams confirm that several lighting systems pass through T14j.

Current research focuses on determining whether vehicles without the illuminated emblem already contain populated terminals for MX16.

If confirmed, retrofitting may only require the missing bumper-side wiring rather than replacing the complete harness.

Current status:

| Investigation | Status |
|--------------|--------|
| Connector identified | ✅ |
| Physical location identified | ✅ |
| Pin population verified | 🔴 |
| Voltage measurements | 🔴 |

---

# T4dh

T4dh is the four-pin connector located directly at the Light Fibre module.

This connector represents the final connection before entering the illuminated grille light.

Known wire colours:

| Pin | Colour |
|------|---------|
| 1 | ws/bl |
| 2 | gn/bl |
| 3 | bl/rt |
| 4 | bl |

No official Volkswagen pin description has currently been located.

The connector therefore remains one of the highest priority measurement points.

---

# T4df

T4df is the mating connector to T4dh.

Evidence currently suggests that this connector belongs to the intermediate harness rather than the main vehicle harness.

Current theory:

Vehicle Harness

↓

T14j

↓

Front Bumper Harness

↓

T4o

↓

Intermediate Harness

↓

T4df

↓

T4dh

↓

L362 / L363

Further verification required.

---

# T4o

T4o appears further upstream in the Current Flow Diagrams.

Current evidence suggests that T4o is the interface between the front bumper wiring harness and the intermediate Light Fibre harness.

This architecture would explain why Volkswagen supplies multiple wiring harnesses for illuminated and non-illuminated vehicles.

---

# Shared Ground Topology

One of the most significant findings is the shared ground architecture.

Current Flow Diagrams confirm that the following components share the same ground network.

- MX16
- L377
- L378

Ground reference:

456

↓

457

↓

Ground

This strongly suggests that Volkswagen designed the contour lighting system around a common grounding strategy.

---

# KL58 versus SIG

A key discovery concerns the electrical difference between the illuminated emblem and the Light Fibre modules.

MX16 receives:

- KL58
- Ground

L377/L378 receive:

- SIG
- Ground

L362/L363 receive:

- Four-wire interface

This indicates that the illuminated emblem is not controlled using the same electrical architecture as the Light Fibre modules.

At the time of writing the exact electrical behaviour of SIG remains unknown.

Possible explanations include:

- PWM output
- Switched 12V output
- Intelligent LED driver signal

Physical measurements are required before any conclusion can be drawn.

---

# Engineering Observation

The illuminated emblem appears electrically simple.

The Light Fibre modules appear electrically intelligent.

This architectural difference may explain why Volkswagen chose separate wiring harnesses for illuminated and non-illuminated vehicles.

Project Lumina therefore focuses on determining whether these systems can be integrated without replacing the complete OEM bumper harness.

---

# Current Flow Diagram Analysis

Project Lumina is based on official Volkswagen Current Flow Diagrams rather than assumptions or aftermarket documentation.

During analysis the following major observations were made.

## Observation 1

MX16 is documented as an independent lighting module.

Unlike the Light Fibre system it receives:

- KL58
- Ground

No additional communication lines are shown.

---

## Observation 2

L362 and L363 are connected through a dedicated four-pin connector.

Volkswagen does not document these pins as:

- KL58
- Terminal 30
- Terminal 31

Instead the connector must be interpreted from the surrounding circuitry.

This strongly suggests the presence of internal electronics.

---

## Observation 3

L377 and L378 are supplied using Ground and SIG.

SIG is currently one of the most important unanswered questions within Project Lumina.

No official documentation describing the electrical characteristics of SIG has yet been located.

---

## Observation 4

The illuminated emblem is shown separately from the Light Fibre modules.

This indicates that Volkswagen considers MX16 an independent lighting component rather than an integrated part of the grille illumination.

---

# OEM Harness Investigation

Current research has identified multiple OEM wiring harnesses involved in the retrofit.

| Part Number | Description | Status |
|-------------|-------------|--------|
| 14A971095AQ | Front bumper wiring harness | 🟢 Confirmed |
| 14A971014 | Intermediate Light Fibre harness | 🟡 Under Investigation |

The exact electrical differences between illuminated and non-illuminated vehicles remain unknown.

Current evidence suggests that the illuminated harness may contain additional conductors for MX16.

This hypothesis has not yet been physically verified.

---

# Physical Measurements

The following measurements are planned.

## T14j

Objectives

- Verify populated terminals
- Identify KL58
- Verify Ground
- Compare illuminated and non-illuminated vehicles

---

## T4dh

Objectives

- Measure all four conductors
- Compare OFF vs ON
- Compare against chassis Ground
- Measure conductor-to-conductor voltage
- Identify possible PWM output

---

## MX16

Objectives

- Verify current consumption
- Verify operating voltage
- Confirm behaviour during parking lights
- Confirm behaviour during DRL

---

# Retrofit Strategies

Several retrofit strategies are currently under consideration.

## Strategy A

Replace the complete OEM bumper wiring harness.

Advantages

- Fully OEM

Disadvantages

- Highest cost
- Largest installation effort

Status

🟡 Investigation

---

## Strategy B

Replace only the intermediate Light Fibre harness.

Advantages

- Lower cost
- Minimal vehicle modification

Disadvantages

- Requires further verification

Status

🟡 Investigation

---

## Strategy C

Build an OEM-compatible adapter harness.

Advantages

- Lowest installation effort
- Fully reversible
- No permanent modification of the vehicle harness

Disadvantages

- Requires electrical verification

Status

🟡 Investigation

---

# Confirmed Facts

The following information has been confirmed through official documentation.

✅ MX16 exists as a dedicated Volkswagen component.

✅ MX16 uses a two-pin connector.

✅ MX16 receives KL58 and Ground.

✅ L362 uses a four-pin connector.

✅ L363 uses a four-pin connector.

✅ L377 uses Ground and SIG.

✅ L378 uses Ground and SIG.

✅ Ground points 456 and 457 are shared.

✅ T14j is the transition connector between the vehicle harness and bumper harness.

---

# Working Theory

The following engineering hypotheses remain under investigation.

🟡 SIG may represent a PWM controlled lighting output.

🟡 The Light Fibre modules likely contain internal LED driver electronics.

🟡 Vehicles without the illuminated emblem may already contain partially populated wiring.

🟡 The intermediate harness (14A971014) may be the only hardware difference between illuminated and non-illuminated vehicles.

🟡 BCM coding may be required after retrofit.

---

# Future Verification

The following tasks remain before Project Lumina reaches Version 1.0.

- Verify T14j pin population.
- Verify KL58 location.
- Verify Ground distribution.
- Verify SIG electrical behaviour.
- Compare illuminated and non-illuminated harnesses.
- Verify OEM retrofit without replacing the complete bumper harness.
- Investigate BCM coding.
- Build prototype adapter harness.
- Validate complete installation.

---

# Revision History

| Version | Description |
|----------|-------------|
| v0.1 | Initial documentation |
| v0.2 | Current Flow Diagram analysis |
| v0.3 | OEM wiring research |
| v0.4 | OEM harness investigation |
| v0.5 | Physical measurement planning |

---

# References

Official Volkswagen documentation forms the foundation of Project Lumina.

Primary sources include:

- Volkswagen Current Flow Diagrams
- Volkswagen Workshop Manual
- OEM Parts Catalogue
- ETKA
- Physical vehicle inspection
- Community research (VWIDTalk and other technical forums)

Community findings are never treated as confirmed until verified against official documentation or physical testing.

---

# Disclaimer

This document is part of Project Lumina.

Its purpose is to document the engineering process behind the OEM illuminated Volkswagen ID.7 front emblem retrofit.

Information may change as additional measurements and official documentation become available.

Every effort is made to distinguish verified engineering data from ongoing research.

---

**End of Document**