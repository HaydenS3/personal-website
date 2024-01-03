---
title: "Control Board Code"
date: 2023-12-29
---

## Overview

This code takes in a number of driver inputs to control DRS, shifting, and the clutch. It also sends data over CAN to be logged.

## Input / Signal Processing

Digital inputs are stored in global variables of the type unsigned long. Bit masking is used to track the input over samples, where each bit represents a single sample of the input. An input with a value of ULONG_MAX is considered `true`, all other values are considered `false`.

This approach was chosen for its space efficiency and ability to debounce digital inputs.

Analog inputs use a rolling average filter and are sampled at a 12 bit resolution.

The sample rate of the system is unknown.

## DRS Control

DRS is controlled via servo. Position is changed using the servo Arduino library. A global boolean `drsChanging` is used to block multiple driver inputs at once.

## Shift Control

Shifting is controlled via two pneumatic solenoids, one for upshifting, and one for downshifting. The stroke length of the shift is controlled via the time the solenoid is held open. If both clutch paddles are pulled, a half shift can be performed in either direction. A global boolean `shifting` is used to block multiple driver inputs at once.

## Clutch Control

The clutch is controlled via a servo. Two clutch paddles are used and the maximum input is taken. Driver input controls the clutch on a hyperbolic curve, where the clutch is properly engaged for the majority of the stroke of the clutch paddle. 

## CAN

The state of the DRS (open or closed) and the position of the clutch are sent over CAN.