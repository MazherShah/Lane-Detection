# Advanced Lane Detection (Single-File Project)

This project is a **single-file** implementation of the classical Udacity-style **Advanced Lane Finding** pipeline.  
It processes one or more input videos and outputs annotated videos with:

- detected lane area overlay
- lane curvature (meters)
- vehicle offset from lane center (meters)

The script performs:
1. **Camera calibration** (from chessboard images) and caches the result
2. **Undistortion**
3. **Binary thresholding** (gradient + color)
4. **Perspective transform** (bird’s-eye view)
5. **Lane pixel detection** (sliding windows, then tracking around polynomial)
6. **Polynomial fit** + temporal smoothing
7. **Curvature & offset measurement**
8. **Lane overlay** back onto original view
9. **Write output video(s)**

---

## Files

- `lane_detection_single.py` — the entire project in one Python file

Expected folders/files (Udacity-style):
- `camera_cal/calibration*.jpg` (camera calibration chessboard images)
- input videos in project root, e.g.:
  - `project_video.mp4`
  - `challenge_video.mp4`
  - `harder_challenge_video.mp4`

Outputs:
- `output_videos/out_<input_video_name>.mp4`
- `calibration.pkl` (auto-created calibration cache)

---

## Requirements

### Python
- Python 3.8+ recommended

### Install dependencies
```bash
pip install numpy opencv-python moviepy
```

---

## How to Run

### 1) Place calibration images
Make sure you have:
```
camera_cal/
  calibration1.jpg
  calibration2.jpg
  ...
```
(or any filenames that match `camera_cal/calibration*.jpg`)

### 2) Put input videos in the project root
Example:
```
project_video.mp4
challenge_video.mp4
harder_challenge_video.mp4
```

### 3) Run the script
```bash
python lane_detection_single.py
```

The script will:
- calibrate the camera (first run only) and save `calibration.pkl`
- process any videos listed in the `VIDEOS = [...]` list inside the script
- save results in `output_videos/`

---

## Using Your Own Input Video

### Option A: edit the `VIDEOS` list
Inside `lane_detection_single.py`, set:
```python
VIDEOS = ["my_input.mp4"]
```
then run:
```bash
python lane_detection_single.py
```

### Option B: add CLI support (optional)
If you want to pass `--video` from the command line, you can add argparse support (ask if you want me to patch your file).

---

## Output

The output video shows:
- a green lane polygon overlay
- text with:
  - **Curvature** (meters)
  - **Offset** from lane center (meters)

Output location:
```
output_videos/out_<input_video_name>.mp4
```

---

## Calibration Cache

The first run computes calibration and writes:
- `calibration.pkl`

If you change calibration images or camera, delete the cache and rerun:
```bash
rm calibration.pkl
python lane_detection_single.py
```

---

## Troubleshooting

### `AttributeError: 'VideoFileClip' object has no attribute 'fl_image'`
This usually means you’re using **MoviePy v2.x**, where `fl_image()` was removed.

Fix:
- Replace `clip.fl_image(...)` with:
  ```python
  out_clip = clip.image_transform(pipeline.process_frame)
  ```

Or install MoviePy v1.x:
```bash
pip uninstall -y moviepy
pip install "moviepy<2"
```

### “No calibration images found”
Check:
- folder name is `camera_cal`
- images match: `camera_cal/calibration*.jpg`

### Lane detection is unstable on challenge videos / real dashcam
You may need to tune:
- `SRC_RATIOS` (perspective transform source points)
- thresholds in `combined_binary()`

---

## Notes / Limitations

- This is a **classical computer vision** pipeline; performance depends heavily on:
  - lighting conditions
  - lane paint quality
  - camera placement and resolution
- For tougher real-world conditions (night/rain/worn lanes), consider:
  - improving thresholding
  - adding stronger sanity checks / recovery
  - using deep-learning segmentation

---

## Credits
This implementation follows the common Udacity “Advanced Lane Finding” approach:
calibration → undistort → threshold → warp → sliding windows → polynomial fit → curvature/offset → overlay.
