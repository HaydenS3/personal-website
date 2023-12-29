---
title: "Dash/DAQ Final Design Report"
date: 2023-01-17
image: "/images/racing.png"
---
## Overview
The dash/DAQ will be responsible for collecting data from the ECU and other sensors around the car, logging that data, and displaying real-time information to the driver.

We have chosen to buy an off-the-shelf dash/DAQ this year. (Custom dash/DAQ will be pursued in the future.) The dash/DAQ we chose is the AiM MXS 1.3. This make and model was chosen for its dual CAN buses, large amount of memory, and extensive documentation.

## Goals
#### Reliability
- **Designed and manufactured by professionals:** The MXS is designed and manufactured by AiM. It’s safe to say they have a little experience doing this sort of thing. We expect the module to be extremely reliable and well tested.
- **It just works (mostly):** The MXS is readily compatible with the PE3, so getting data from the ECU is plug and play. Getting data from our custom data system is a little more complex, however, the 2nd CAN channel and software on the MXS  is built for this application.
#### Consistency
- **Designed and manufactured by professionals:** Once again, the MXS is designed and manufactured by AiM. We expect it to be well tested and consistent in operation.
- **Configure it once, works the same forever:** The MXS is configured through custom software. We can be confident that once the MXS has been configured and is proven working, it will continue to operate in the same manner.
#### Control
- **Highly customizable dashboard and data logging:** The MXS software makes the dashboard and data logging highly customizable. We will be able to create and change dashboard layouts on the fly. Similarly, new sources of data on the CAN network can be easily added to MXS data collection.

## Rules

| Category                        | ID Number | Definition                                                                                                                           | Notes                                      |
| ------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------ |
| Cockpit, Cockpit Opening        | T.1.1.4.d | Cables, wires, hoses, tubes, etc. must not impede the template                                                                       | Wires will be cleanly tucked away          |
| Cockpit, Internal Cross Section | T.1.2.3.e | Cables, wires, hoses, tubes, etc. must not impede the template                                                                       | Wires will be cleanly tucked away          |
| Cockpit, Controls Accessibility | T.1.4.1   | All Vehicle Controls (steering, gear change, Cockpit Mains Switch / Cockpit Shitdown Button) must be operated from inside the cokpit | Dash will be mounted within the cockpit    |
| Cockpit, Controls Accessibility | T.1.4.2   | All Vehicle Controls must stay below the top-most point of the Front Hoop in any operational position                                | Dash will be mounted under the Front Hoop  |
| Cockpit, Firewall(s)            | T.1.8.4   | Grommets must be used to seal any pass through for wiring, cables, etc                                                               | Grommets will be used for any pass through |

## Math & Modeling

#### Details

The MXS will receive data via two CAN networks. One CAN network will relay ECU data, the other will relay data from the sensor board network. The MXS will additionally pull data from an AiM gps and allow USB connectivity via a mounting point in the cockpit. Data will be viewed using AiM’s RaceStudio 3 software.

The MXS also provides multiple built-in math functions. These functions will be used for all linearizations, keeping all linearizations contained within MXS software for easy access and modification.

We have also run calculations on CAN data throughput and storage. Maximum throughput for a standard CAN bus is 1 Mbit/s or 125,000 bytes per second. Since we have roughly 30 sensors on the car plus 8 bytes of data from each of our 4 sensor boards. The sum of these sensors comes out to 54 bytes per data point. We assume each byte will have a maximum sample rate of 100Hz. This leaves us with a maximum of 5,400 bytes per second; well under our cap of 125,000 bytes per second. At this rate of transfer, we can expect to store 18 MB of data per hour.
This is subject to increase if sensors return larger, higher resolution data.

Weight: 1.17 lbs

#### Mounting

![MXS Mounting 1](/images/dash-daq-fdr-23/mxs-mounting-1.png)
![MXS Mounting 2](/images/dash-daq-fdr-23/mxs-mounting-2.png)
![MXS Mounting 3](/images/dash-daq-fdr-23/mxs-mounting-3.png)

#### Wiring

Wiring to the dashboard should be very simple. Here is a list of the wires necessary:

| MXS Pin    | To/From       |
| ---------- | ------------- |
| 12V In     | Power harness |
| GND        | Power harness |
| CAN 1 High | Sensor  board |
| CAN 1 Low  | Sensor board  |
| CAN 2 High | PE3           |
| CAN 2 Low  | PE3           |
| 5 pin GPS  | GPS module    |
| USB Data + | USB port      |
| USB Data - | USB port      |
| USB GND    | USB port      |

## Verification & Testing

We’ve had success transferring data from the custom sensor boards to the MXS. We’ve also experimented with different driver layouts on the dashboard.

## Production Plan
There are very few wires to run for the dash, and we will follow this year’s wiring standard. This means each wire will be measured, cut, and pinned. Heatshrink and snakeskin will be added as needed, and each bundle will be labeled.