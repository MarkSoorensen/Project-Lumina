# Project Lumina

> **OEM Illuminated Volkswagen Emblem – Electrical Integration Guide for the Volkswagen ID.7**

![Status](https://img.shields.io/badge/Status-Active-success)
![Vehicle](https://img.shields.io/badge/Vehicle-VW%20ID.7-blue)
![Platform](https://img.shields.io/badge/Platform-MEB-informational)
![License](https://img.shields.io/badge/License-MIT-green)

---

## Overview

Project Lumina documents the electrical integration of the OEM illuminated Volkswagen front emblem on the Volkswagen ID.7.

The original goal of this project was to create a complete OEM retrofit.

During development it became clear that the illuminated emblem used for testing is **not a direct mechanical replacement** for the factory emblem on my 2024 Volkswagen ID.7. Significant modifications to both the bumper and the emblem housing were required.

Because of this, the focus of this repository has changed.

Instead of documenting the mechanical retrofit, this repository documents the **electrical solution**, allowing others to understand how the OEM emblem can be powered correctly while using the factory light bar as the trigger source.

---

# Project Goals

✔ Identify the factory PWM signal

✔ Verify the PWM signal using measurements

✔ Develop a safe electrical solution

✔ Keep the factory wiring unmodified whenever possible

✔ Document all findings

✔ Make the project open source

---

# Current Status

| Feature | Status |
|----------|--------|
| PWM trigger identified | ✅ |
| HW-517 tested | ✅ |
| Dedicated 12V supply | ✅ |
| Bench testing completed | ✅ |
| OEM connector documented | ✅ |
| Mechanical retrofit | ⚠ Not plug-and-play |

---

# Important Notice

## This is NOT a complete retrofit guide.

The electrical solution documented here has been tested successfully.

However, the illuminated OEM emblem tested during this project **does not directly fit** the front bumper on my 2024 Volkswagen ID.7 without significant modifications.

This repository therefore focuses entirely on the electrical integration.

---

# Tested Vehicle

Vehicle:

Volkswagen ID.7

Model Year:

2024

Platform:

MEB

---

# Tested Hardware

| Component | Status |
|-----------|--------|
| OEM Illuminated Emblem (14A 853 600) | ✅ |
| Factory Emblem (14A 853 601 B) | ✅ |
| HW-517 MOSFET Module | ✅ |
| Dedicated 12V Supply | ✅ |
| Inline Fuse | ✅ |

---

# Electrical Design

The factory LED light bar is **not** used to power the emblem.

Instead, it is only used as a PWM trigger.

The emblem receives its power directly from a dedicated fused 12V supply through a HW-517 MOSFET relay.

This ensures that the factory light bar is never loaded by the additional current required by the illuminated emblem.

---

# Wiring Concept

```text
                  Factory LED Light Bar
                          │
                          │ PWM Signal
                          ▼
                +-------------------+
                |     HW-517        |
                |  PWM MOSFET Relay |
                +-------------------+
                          │
                          │
                          ▼
               Dedicated 12V Supply
                   (1A Inline Fuse)
                          │
                          ▼
              OEM Illuminated Emblem
```

---

# Bench Testing

The illuminated emblem was successfully tested before installation.

Bench test observations:

- Rated Voltage: 13.5V

- Rated Power: 12W

- Two separate 2-pin connectors

- Both connectors must receive power simultaneously

If only one connector is powered the emblem will not illuminate correctly.

---

# Mechanical Findings

Originally this project was intended as a full OEM retrofit.

Unfortunately the illuminated emblem tested in this project required significant modifications before it could physically fit the bumper.

Modifications included:

- Bumper trimming

- Emblem housing trimming

Because of this the mechanical installation is **not documented** in this repository.

If another emblem revision or bumper configuration is found to fit without modification this repository will be updated.

---

# Parts Used

| Part | Description |
|------|-------------|
| 14A 853 600 | Illuminated VW emblem |
| 14A 853 601 B | Standard VW emblem |
| HW-517 | PWM MOSFET relay |
| Inline fuse holder | 1A recommended |
| Automotive wire | 0.75mm² |
| Waterproof junction box | Optional |

---

# Repository Structure

```
Project-Lumina
│
├── README.md
│
├── docs
│   ├── Introduction.md
│   ├── Wiring.md
│   ├── Parts-List.md
│   ├── Bench-Test.md
│   ├── Installation.md
│   ├── Mechanical-Notes.md
│   └── Troubleshooting.md
│
└── images
```

---

# Disclaimer

This project is provided for educational purposes only.

Vehicle wiring modifications are performed entirely at your own risk.

Always disconnect the 12V battery before performing electrical work.

Double-check all wiring before applying power.

---

# Contributing

Pull requests are welcome.

If you have:

- another emblem revision

- another model year

- additional measurements

- improved wiring solutions

please consider contributing to this project.

---

# Future Work

- Rear illuminated emblem

- OEM connector adapter

- Additional model year compatibility

- Wiring diagrams

- Installation photos

---

# Acknowledgements

Thanks to everyone in the Volkswagen community who has shared information, measurements and experiences.

Hopefully this repository makes the electrical side of the illuminated emblem retrofit easier for the next person.

---

## License

MIT License

---

**Project Lumina**

*OEM Illuminated Volkswagen Emblem Electrical Integration*
