# Passive Rogue Access Point Detection Experiment

## Status

- Track: Experiment / Audit
- Status: Planned; formal testing has not started
- Last updated: 2026-10-31

## Objective

Evaluate whether a passive ESP32 sensor can distinguish approved edge-infrastructure access points from controlled, unapproved test access points using 802.11 management-frame information and RSSI patterns.

The ESP32 will send captured metadata to a Raspberry Pi over USB serial. The Pi will log observations and run the analysis.

## Hypothesis

Using configured access-point identity and management-frame features, together with measured RSSI patterns, the prototype will alert on controlled unapproved test access points while keeping false alerts on approved access points within a measured range.

The experiment will report measured results; it will not assume a particular detection or false-positive rate in advance.

## Scope and safety

- Conduct tests only with access points and equipment controlled by the experimenter, in a controlled lab.
- The sensor is passive: it must not transmit, associate with access points, inject frames, or disrupt wireless service.
- Analyze relevant management-frame metadata and RSSI; do not collect application or user data.
- The ESP32 sensor is limited to 2.4 GHz Wi-Fi. Document the channels monitored in each run.
- Results apply only to the tested hardware, firmware, configuration, environment, and test cases.

## Planned system

1. ESP32 firmware passively captures selected 802.11 management-frame information and RSSI.
2. Firmware sends timestamped records to the Raspberry Pi over USB serial.
3. Python analysis on the Raspberry Pi applies the configured detection rules, logs alerts, and calculates metrics.

Implementation details and versions will be recorded before formal testing:

- ESP32 firmware commit/version: TBD
- PlatformIO framework and project configuration: TBD
- Raspberry Pi analysis software commit/version: TBD
- Detection-rule configuration version: TBD
- Serial settings: TBD
- Monitored channel plan and any channel dwell times: TBD

## Ground truth and test cases

Before each run, record the access-point identity and configuration used as ground truth. The test access points must be controlled by the experimenter.

| Case | Test condition | Ground-truth label | Expected detector outcome |
|---|---|---|---|
| K1 | Approved access point, using its registered configuration | Known | No suspicious alert |
| S1 | Controlled test access point with an unapproved BSSID; other settings held as close as practical to the approved AP | Suspicious | Alert |
| S2 | Controlled test access point with a configured management-frame or security-setting mismatch | Suspicious | Alert |
| N1 | Normal variation in received signal strength from an approved access point | Known | No suspicious alert |

The exact APs, BSSIDs, settings, locations, and number of trials are TBD. Record them in the run log before collecting results. Keep test cases and configuration changes consistent across repeated trials.

## Detection configuration

The rules will be configurable and versioned. Candidate features to evaluate include:

- Approved SSID and BSSID inventory
- Observed channel and security-related management-frame fields
- Selected management-frame information elements
- RSSI observations and their variation over time

The final set of fields, rule thresholds, and RSSI baseline method are TBD. Record each value in the configuration file and do not change it midway through a trial. If a rule or threshold changes, assign a new configuration version and rerun the affected tests.

## Controlled test conditions

Record the following for every run:

- Run ID, date/time, operator, and software/configuration versions
- ESP32 board and sensor placement
- Access-point identity and configuration for each test case
- Sensor and access-point positions and orientations
- Monitored channel(s) and channel dwell times, if applicable
- Test start/end times and any interruptions
- Relevant environmental changes, such as people moving or equipment being repositioned

Use marked, repeatable positions for the sensor and access points. Decide the trial duration, number of repetitions, and any RSSI-variation scenarios before formal testing; these are TBD.

## Metrics

Calculate metrics at the **trial level**, using the ground-truth label assigned before the run:

- **Detection rate** = TP / (TP + FN)
- **False-positive rate** = FP / (FP + TN)
- **Alert latency** = time from the first eligible observation of a suspicious test AP to the first corresponding alert

Where:

- TP = suspicious trial that produced an alert
- FN = suspicious trial that produced no alert
- FP = known-AP trial that produced a suspicious alert
- TN = known-AP trial that produced no suspicious alert

Report counts as well as percentages. Report alert latency for detected suspicious trials, and report missed trials separately rather than assigning them a latency.

## Resource-use measurements

Record resource use during each test run:

- ESP32 minimum free heap observed
- ESP32 receive-queue overflow or dropped-record count
- ESP32 CPU-use measure, if the implementation can measure it reliably
- Raspberry Pi analysis-process CPU use and peak resident memory
- Serial records received and records successfully analyzed

Record the measurement method, sampling interval, and units before formal testing; these are TBD.

## Trial procedure

1. Confirm the approved and test AP configurations match the run log.
2. Start the Pi logger and record the run ID and configuration version.
3. Start the ESP32 sensor and confirm serial records are being received.
4. Run the predeclared test condition for the predeclared duration without changing the detector configuration.
5. Stop collection and save the raw log, alert log, resource measurements, and run notes.
6. Repeat according to the predeclared trial count.
7. Run the analysis script against the saved logs and preserve its output.

Do not exclude or silently edit failed, interrupted, or unexpected trials. Mark their status and reason in the run log.

## Results and reproducibility

For each completed run, preserve:

- Ground-truth and test-condition record
- Versioned detector configuration
- Raw sensor-to-Pi records and alert log
- Resource-use measurements
- Analysis command and generated output
- Notes on deviations, failures, and exclusions

The public results summary will state the test setup, trial counts, metric values, limitations, and any deviations from this plan. No results are reported until the corresponding trials have been run.
