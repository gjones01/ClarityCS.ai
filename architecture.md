### 1. Frame Extraction Pipeline
- **Input**: CS2 gameplay video (.mp4 or demo)
- **Output**: JPEG frames sampled every 5 frames (60FPS samples)
- Built using OpenCV and FFmpeg

### 2. Behavior Detection Model
- **Model Type**: Custom CNN inspired by MobileNetV2
- **Input**: Raw or preprocessed game frame (RGB)
- **Output**: Binary prediction — `Cheater` or `Legit`
- **Trained on**: Labeled frames curated from known cheater/legit gameplay

- ### 3. Visual Explainability Module
- Uses **Grad-CAM** to generate heatmaps
- Shows what parts of the image influenced the model’s decision
- Useful for validation, transparency, and potential appeal systems

Currently, ClearVision operates on **individual JPEG frames** extracted from gameplay videos. This approach allows for faster labeling, easier visualization, and simpler training using standard CNNs.

**Why still frames?**
  - More efficient for early models
  - Easier to apply Grad-CAM heatmaps
  - Computationally more efficient to understand model vision

---

### Planned: Video-Based Input

The system is being designed with future **video ingestion** in mind:

- Extract frames directly from gameplay recordings
- Support temporal patterns (e.g., burst flicks, movement pacing)
- Use temporal-aware models like 3D CNNs or Transformer-based video classifiers. Temporal context is paramount and this will be the next stepping stone of the project.

