---
title: "Data Harness Final Design Report"
date: 2022-10-19
image: "/images/data-harness-fdr-23.png"
summary: "The data harness is one of the four wiring harnesses on the WUFR-23. It powers all of the non-engine sensors and transmits data via sensor boards to the AiM MXS, our dash/DAQ."
---

## Overview

The data harness is one of the four wiring harnesses on the WUFR-23. It powers all of the non-engine sensors and transmits data via sensor boards to the AiM MXS, our dash/DAQ. Listed below are all of the components in the harness and their inputs/outputs:
| Component                | Inputs                                                                   | Outputs |
| ------------------------ | ------------------------------------------------------------------------ | ------- |
| Rear Sensor Board        | CAN, rear shocks, rear brake temperatures, rear brake pressure           | CAN     |
| PDM                      | CAN                                                                      | CAN     |
| Front Left Sensor Board  | CAN, front shocks, front left brake temperature, front brake pressure    | CAN     |
| Front Right Sensor Board | CAN, radiator, front right brake temperature, pitot tube, steering angle | CAN     |
| PE3                      | Numerous engine sensors                                                  | CAN     |

## Goals
#### Reliability
- **Less wire/connector breakage:** To combat the issue of wires breaking due to wear, we are using thicker gauges of wire at every possible connection. We use 18 AWG wire everywhere possible, using 22 AWG wire only for connectors which will not accept larger gauges. Though this greater gauge will add more bulk to the bundles and increase the weight, the fact that our bundles will be significantly shorter negates this.
- **Easier wiring troubleshooting:** This year, we are not using MX23A connectors except for the connections to the PE3 itself. This is because in the WUFR-22, it was difficult to depin these connectors without either damaging the connector or the wires. By using primarily deutsch and other sensor connectors, we will be able to easily depin and repin wires in the (hopefully rare) case of incorrect wiring.
#### Consistency
- **Better wiring diagram readability:** For the WUFR-23 engine harness, we took special care to make sure the RapidHarness diagram was more organized and readable. Instead of giving connectors arbitrary names such as “X2”, we labeled them with a shortened version of their name (noted in the table above). We also included the correct color and gauge of the wire needed to ensure our wiring color scheme is followed across all harnesses. This reduces the need for EDA members to cross reference the wiring tables and diagrams in RapidHarness and should reduce errors when wiring. We also organized the diagram itself so that the components are in positions that are relatively similar to their proposed positions on the car, helping to better visualize bundle routing.
#### Control
- **Improved wire management:** The WUFR-22’s bunker, while a convenient place to have all of EDA’s major components, resulted in us having thick and messy bundles of wire spanning nearly the whole car. To minimize this, we designed a harness that would be almost entirely behind the firewall. This results in shorter bundle lengths and mitigates the need for bundles going from the front of the car to the engine. We will also be following a strict wire color scheme. Furthermore, we plan to be stricter with our labeling and heat-shrinking of bundles.

## Math & Modeling

**WUFR-23 Wiring Harness Color Scheme**
| Gauge | Color                 | Purpose             | Amount Ordered |
| ----- | --------------------- | ------------------- | -------------- |
| 12    | Red with white stripe | 12V                 | 500 ft         |
| 12    | Black                 | High GND            | 250 ft         |
| 14    | Black                 | CAN GND             | 500 ft         |
| 14    | Red                   | CAN PWR             | 500 ft         |
| 16    | Black                 | Misc. GND           | 500 ft         |
| 16    | Red with white stripe | Misc. PWR           | 500 ft         |
| 18    | Black                 | Low GND             | 500 ft         |
| 18    | Red                   | 5V PWR              | 500 ft         |
| 18    | Purple                | Sensor board signal | 500 ft         |
| 18    | Green                 | CAN High            | 500 ft         |
| 18    | White                 | CAN Low             | 500 ft         |

**WUFR-23 Wiring Harness Diagram**

![WUFR-23 Wiring Harness Diagram](/images/data-harness-fdr-23.png)

## Production Plan
1. Each sensor spliced if necessary and connected to a Deutsch DT connector (A power, B ground, C signal; male on sensor side)
2. Powers and grounds will be spliced according to the Rapid Harness
3. Sensor bundles will be heat shrunk, snake skinned, and labeled
4. CAN lines will be twisted and wrapped with aluminum foil
5. Continuity testing will be done continuously to verify connections
## Testing Plan
12V and 5V power will be continuously tested using a multimeter throughout the wiring process to ensure that all sensors are receiving the appropriate voltage. Regular continuity testing will also be done, both on the PCBs and across the harness. We will create a running spreadsheet of these continuity testing results to ensure consistency at different points in our engine harness build timeline. 