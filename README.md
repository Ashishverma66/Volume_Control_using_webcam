# Volume Control Using Webcam

Control your system volume in real time using hand gestures. A webcam tracks your hand, measures the distance between your thumb and index finger, and maps that distance to the speaker volume.

Built with Python, OpenCV, and MediaPipe Hand Landmarker.

## Features

- Real-time hand tracking via MediaPipe Hand Landmarker
- Volume control from thumb–index finger distance (pinch open = louder, pinch closed = quieter)
- On-screen volume bar and percentage display
- Cross-platform system volume control:
  - **Windows** — [pycaw](https://github.com/AndreMiras/pycaw)
  - **macOS** — built-in `osascript` volume control
- Visual feedback: landmarks, finger line, and a green indicator when volume is near minimum

## How It Works

1. The webcam feed is captured with OpenCV.
2. `HandTrackingModule` runs MediaPipe Hand Landmarker on each frame and extracts 21 hand landmarks.
3. Landmark 4 (thumb tip) and landmark 8 (index tip) are used to compute pixel distance.
4. Distance is mapped to a 0–100% volume range with `numpy.interp`.
5. System volume is updated each frame:
   - On Windows, volume is set through the Core Audio API via pycaw.
   - On macOS, volume is set with AppleScript.

## Project Structure

```
Volume_Control_using_webcam/
├── VolumnHandControl.py    # Main app: webcam loop, volume mapping, UI overlay
├── HandTrackingModule.py   # Hand detector wrapper around MediaPipe Hand Landmarker
├── hand_landmarker.task    # MediaPipe hand landmark model (required)
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.9+
- A working webcam
- **Windows:** `pycaw`, `comtypes` (in addition to the packages below)

Core Python packages:

- `opencv-python`
- `numpy`
- `mediapipe`

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/Ashishverma66/Volume_Control_using_webcam.git
   cd Volume_Control_using_webcam
   ```

2. Create and activate a virtual environment (recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate   # macOS / Linux
   # .venv\Scripts\activate    # Windows
   ```

3. Install dependencies:

   ```bash
   pip install opencv-python numpy mediapipe
   ```

   On **Windows**, also install:

   ```bash
   pip install pycaw comtypes
   ```

   Ensure `hand_landmarker.task` is present in the project root (it ships with this repo).

## Usage

Run the main script:

```bash
python VolumnHandControl.py
```

- Show one hand to the camera.
- Move your thumb and index finger closer or farther apart to change volume.
- A vertical bar on the left shows the current level; the percentage is displayed below it.
- Press **`q`** in the video window to quit.

### Tips

- Good lighting and a clear view of your hand improve tracking.
- Pinch your thumb and index finger together to lower volume; spread them apart to raise it.
- When finger distance drops below ~50 px, the center marker turns green (near-minimum volume).

## Technologies

| Technology | Role |
|------------|------|
| Python | Application runtime |
| OpenCV | Webcam capture and on-screen overlays |
| MediaPipe Hand Landmarker | Hand detection and landmark extraction |
| NumPy | Distance-to-volume interpolation |
| pycaw / comtypes | Windows system volume (Windows only) |
| osascript | macOS system volume (macOS only) |

## License

This project is open source. See the repository for license details.
