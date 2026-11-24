# Data

The raw *Simulation 2021* data are not included and should be requested from the authors of Islam et al. (2021),
"Cybersickness Prediction from Integrated HMD's Sensors: A Multimodal Deep Fusion Approach using Eye-tracking and
Head-tracking Data".

## Preprocessing

1. For each FMS report at time *t*, keep the 11-s segment [*t* − 10 s, *t* + 1 s] of eye- and head-tracking data
   (20 Hz). The segment is labelled with the CS level of that report: None (FMS 0–1), Low (1, 2], Medium (2, 4],
   High (> 4).
2. In each signal channel, remove frames that deviate by more than three standard deviations from the mean.
3. Apply exponential smoothing with a smoothing factor of 0.08.
4. Divide each segment into non-overlapping 60-frame windows.

## `window_features.csv` (one row per 60-frame window)

Used by the machine learning notebooks and by `incremental`.

| Column | Description |
|---|---|
| `participant` | user ID (1–23) |
| `simulation` | scenario: `Roller` (Roller Coaster), `Sea` (SeaVoyage), `Beach` (Beach City), `Walk` (Road Side), `Room` (Furniture Shop) |
| `segment_marker` | ID of the 11-s segment, increasing with time within each user |
| `seg_win_index` | index of the window within its segment |
| `seg_win_start_row`, `seg_win_end_row` | first and last frame of the window within its segment |
| `cs` | CS level: 0 None, 1 Low, 2 Medium, 3 High |
| `<channel>__mean` | window mean of each of the 40 eye and head channels listed below |

## `frame_features.csv` (one row per frame, after steps 1–3)

Used by `model_comparison/dl_models.ipynb` and by the feature-extraction timing in `incremental`.

| Column | Description |
|---|---|
| `datetime` | time stamp of the frame |
| `participant`, `simulation`, `cs` | as above |
| `window_marker` | ID of the 11-s segment (same values as `segment_marker`) |
| `<channel>` | the 40 eye and head channels listed below |

## Channels

- Convergence distance: `Convergence_distance`
- Eye openness: `Left_Eye_Openness`, `Right_Eye_Openness`
- Pupil diameter: `LeftPupilDiameter`, `RightPupilDiameter`
- Pupil position: `LeftPupilPosInSensorX/Y`, `RightPupilPosInSensorX/Y`
- Eye gaze direction (HMD): `NrmSRLeftEyeGazeDirX/Y/Z`, `NrmSRRightEyeGazeDirX/Y/Z`
- Eye origin: `NrmLeftEyeOriginX/Y/Z`, `NrmRightEyeOriginX/Y/Z`
- Combined gaze origin: `GazeOriginLclSpc_X/Y/Z` (HMD), `GazeOriginWrldSpc_X/Y/Z` (world)
- Combined gaze direction: `GazeDirectionLclSpc_X/Y/Z` (HMD), `GazeDirectionWrldSpc_X/Y/Z` (world)
- Head quaternion rotation: `HeadQRotationX/Y/Z/W`
- Head Euler angles: `HeadEulX/Y/Z`
