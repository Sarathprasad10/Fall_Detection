# ⚠️ Fall Detection Using YOLOv8 Pose & Deep SORT (Colab Edition)

This project uses **YOLOv8 Pose Estimation**, **Deep SORT tracking**, and **advanced pose logic** to detect human falls in video sequences. It's designed to work efficiently in **Google Colab** and supports video input/output from Google Drive.

## 🚀 Features
- 🔍 **YOLOv8-Pose**: Detects human keypoints for 17 body parts.
- 🧠 **Advanced Fall Detection**: Uses angle, pose confidence, aspect ratio, movement, and body proportions to determine if a person has fallen.
- 🔄 **Deep SORT Tracking**: Assigns consistent IDs to people across frames.
- ✅ **Improved Filtering**: Skips close-ups, blurred detections, and low-confidence poses.
- 🟢 **Live Feedback**: Shows live detection results frame-by-frame in Colab output.
- 💾 **Video Output**: Saves the final annotated video to Drive.

## 📦 Dependencies

Install the following libraries (especially if not using Colab):

```bash
pip install ultralytics
pip install deep_sort_realtime
```

## 📂 Input/Output Paths

Make sure to replace these with your own paths on Google Drive:

```python
video_path = "/content/drive/MyDrive/Colab Notebooks/FallDetetction/videoplayback.mp4"
output_path = "/content/drive/MyDrive/Colab Notebooks/FallDetetction/04082025FallDetection_Improved.mp4"
```

## 🧠 Fall Detection Logic

The `is_fall_advanced()` function includes:
- Head-to-ankle height thresholds
- Pose completeness check
- Bounding box size and aspect ratio filtering
- Pose angle (shoulder-hip alignment)
- Head–hip distance
- Movement patterns
- Optional kicking detection (to reduce false positives from actions like kicking)

## 📈 How It Works

1. **Pose Detection**: YOLOv8 detects humans and extracts 17 keypoints.
2. **Tracking**: Deep SORT tracks each person and assigns unique IDs.
3. **Fall History**: Pose history is stored for each tracked ID.
4. **Fall Detection**: Each frame is analyzed for posture, movement, and spatial cues.
5. **Annotation**: Detected falls are drawn in red; normal postures in green.
6. **Video Output**: Annotated results are saved to an output MP4.

## 📸 Example Label

```plaintext
ID 4: Fall    ← when a sustained fall is detected
ID 7: Normal  ← otherwise
```

## 📌 Notes
- Minimum person height threshold avoids detecting small distant figures.
- `POSE_CONFIDENCE_THRESHOLD` ensures only accurate keypoints are used.
- False positives from portraits and close-ups are suppressed.
