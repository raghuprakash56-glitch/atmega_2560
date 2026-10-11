# Project Overview

## Problem
Drivers may need assistance judging distance to an obstacle and identifying whether a parking slot is available.

## Objective
Build a microcontroller-based prototype that senses nearby obstacles and/or slot status, processes readings on an ATmega2560, and presents feedback using a numeric display and buzzer.

## Design approach
The firmware is divided into modules so that low-level hardware access is separated from application logic. Each driver should expose a small public API through a header file, with register manipulation kept in the implementation.

## Scope and limitations
This is a prototype. Sensor performance depends on mounting, surface reflectivity, lighting, wiring, and calibration. A threshold such as 512 is only a software decision boundary; it is not a distance measurement and must be validated for the actual sensor and circuit.
