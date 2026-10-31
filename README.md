# rogue-ap-detection

## Vulnerability Summary
Document the target device, what you uncovered, and the security impact.

# Rogue Access Point Detection Experiment

**Track:** Experiment / Audit  
**Status:** Planning

## Research question

How well can a passive edge device use observed 802.11 management-frame
information and signal-strength patterns to flag unexpected access points
in an authorized, controlled lab?

## Purpose

This project evaluates a wireless-monitoring prototype. It does not assume
that a matching SSID, a particular BSSID, or an RSSI pattern alone proves
that an access point is malicious.

The experiment will measure detection behavior under documented lab
conditions and report false positives, missed detections, alert latency,
and device resource use where those measurements are available.

## Safety and scope

- Monitor only networks and devices owned by the project author or covered
  by explicit authorization.
- Keep tests within a controlled lab.
- Do not attempt to disrupt networks or devices.
- Do not publish raw captures that may contain information about other
  people's networks.
- Treat results as limited to the documented hardware, software, and test
  conditions.

## Hardware under test

See [`target_device/Device_Profile.md`](target_device/Device_Profile.md).
Record exact hardware and software versions there; do not guess them.

## Repository layout

- `src/esp32_monitor/` — ESP32 monitoring firmware.
- `analysis/scripts/` — analysis and reporting scripts.
- `results/` — experiment measurements and conclusions.
- `media/` — lab data-flow diagram and sanitized figures.

## Methodology

To be completed after recording the exact board model and software versions.
The procedure will describe the authorized test setup, observations collected,
and how each metric is calculated.

## Results

To be completed after running the experiment. Do not fill in example numbers
as though they were measured results.

## Limitations

To be completed after testing. Discuss what the experiment did not test and
why the observed signals should not be treated as definitive proof of a rogue
access point.
