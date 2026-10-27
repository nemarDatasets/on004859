[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on004859-blue)](https://doi.org/10.82901/nemar.on004859)

<!-- nemar:provenance -->
## Provenance

This dataset is mirrored on NEMAR from OpenNeuro.

- Source: [ds004859](https://openneuro.org/datasets/ds004859)
- DOI: [10.18112/openneuro.ds004859.v1.0.0](https://doi.org/10.18112/openneuro.ds004859.v1.0.0)

## Channel names follow the data headers (18 Oct 2026)

In 9 recordings the channel list of channels.tsv did not equal the data-file header (names, order or count), so `mne_bids.read_raw_bids` stopped with 'Channel mismatch' (or 'Duplicate channel names'); EEGDash renamed the data channels by position to the channels.tsv names, which gives wrong labels wherever the two lists are not aligned. Since 18 Oct 2026 every channels.tsv lists exactly the header channels, in header order, with the header names (MNE names: duplicated header labels numbered -0, -1).

Rows were matched to header channels BY NAME, never by position (exact; then case/whitespace; then the recorder prefix 'EEG '/'POL ', '_' and zero padding; then a trailing '-<reference>' token). Matched rows keep all their columns (type, units, status, ...); 0 rows took the header name.

129 header channels had no channels.tsv row (9 files) and got a new row: type from the name (ECG/EMG/EOG/trigger) or from the other contacts of the same shaft, else MISC; units from the header; status n/a. Examples: `sub-001_ses-01_task-stroop_run-01_ieeg.edf`: E, DC01, DC02, DC03; `sub-002_ses-01_task-stroop_run-01_ieeg.edf`: E, DC01, DC02, DC03; `sub-003_ses-01_task-stroop_run-01_ieeg.edf`: E, DC01, DC02, DC03.

130 channels.tsv rows had no channel in the data file (7 files) and were removed; they are kept verbatim under `sourcedata/channels-removed-2026-10-18/` (same relative path). Examples: `sub-002_ses-01_task-stroop_run-01_ieeg.edf`: B41, B42, B43, B44, B45; `sub-003_ses-01_task-stroop_run-01_ieeg.edf`: B53, B54, B55, B56, B57; `sub-004_ses-01_task-stroop_run-01_ieeg.edf`: B47, B48, B49, B50, B51.

9 files listed the channels in another order than the header; rows now follow the header order.

EEGDash's positional renaming had given wrong labels to 1001 channels in 9 files (rows missing, extra or out of order before that position).

## Electrode locations (19 Oct 2026)

Add coordsystem.json fsaverage/mm next to 9 electrodes.tsv. Evidence: Paper PMC11500755 (Methods): "we standardized each electrode location to the FreeSurfer standard coordinates, commonly referred to as FSaverage"; 7 of the 9 electrodes files are byte-identical to ds006234/on005545 (MNI-305) and 5 to on007118 (fsaverage / mm). fsaverage is a millimetre space by definition.

Scope: these files declare the frame and units of the existing electrodes.tsv only; no coordinate value changed. This dataset mirrors OpenNeuro; the same change belongs upstream.
