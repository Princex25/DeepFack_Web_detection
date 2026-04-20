# Deepfake Detection (Django Application)

A Django web application that detects deepfake videos by extracting facial frames and running them through a deep learning model. Users upload a short video, choose a frame sequence length, and receive a **REAL/FAKE** prediction with a confidence score.

## ✨ Key features

- Upload short videos and analyze them in-browser.
- Frame extraction + face cropping pipeline.
- Pretrained deepfake detection models with multiple sequence lengths.
- Prediction results page with confidence and visualized frames.

## 🧠 How it works (high-level)

1. A video is uploaded and stored in `uploaded_videos/`.
2. Frames are extracted and faces are detected/cropped.
3. A ResNeXt50 backbone + LSTM model predicts **REAL** or **FAKE**.
4. The most accurate model for the selected sequence length is chosen automatically.

## 📦 Project structure (important parts)

- `ml_app/` — Django app with the prediction pipeline and views.
- `models/` — Pretrained `.pt` PyTorch models.
- `uploaded_videos/` — Uploaded video files.
- `uploaded_images/` — Saved frames and cropped faces.
- `static/` + `templates/` — UI assets and HTML templates.
- `project_settings/` — Django project settings and URLs.
- `Dockerfile`, `nginx/` — Optional container deployment setup.

## ✅ Requirements

- Python 3.8+ (recommended 3.10+)
- `pip` and `virtualenv`
- OS packages for `dlib` and `face_recognition` if wheels are unavailable

Key Python dependencies (see `requirements.txt`):

- Django 5.x
- PyTorch + TorchVision
- OpenCV
- face-recognition / dlib

## 🚀 Local setup (development)

### Option A: Clone the repo and run locally

1. Clone the repository.
2. Move into the Django app directory (the folder that contains `manage.py`).
3. Create and activate a virtual environment.
4. Install dependencies.
5. Run migrations.
6. Start the server.

Example (PowerShell):

1. `git clone <REPO_URL>`
2. `cd "Deepfake_detection_using_deep_learning-master - Copie\Django Application"`
3. `python -m venv .venv`
4. `./.venv/Scripts/Activate.ps1`
5. `pip install -r requirements.txt`
6. `python manage.py migrate`
7. `python manage.py runserver`

Open: `http://127.0.0.1:8000/`

### Option B: If you already have the code locally

1. Create and activate a virtual environment.
2. Install dependencies.
3. Run Django migrations.
4. Start the server.

Example (PowerShell):

1. `python -m venv .venv`
2. `./.venv/Scripts/Activate.ps1`
3. `pip install -r requirements.txt`
4. `python manage.py migrate`
5. `python manage.py runserver`

Open: `http://127.0.0.1:8000/`

## 🖥️ Usage

1. Navigate to the home page.
2. Upload a short video (MP4 recommended).
3. Select the sequence length (frames): **10 / 20 / 40 / 60 / 80 / 100**.
4. Click **Analyze Video**.
5. Review the prediction and extracted frames.

## 🧪 Model selection logic

Models are stored in `models/` and named like:

```
model_<acc>_acc_<sequence>_frames_<dataset>.pt
```

The app automatically selects the **highest-accuracy model** that matches the chosen sequence length.

## 🧰 Deployment notes

- The Docker image runs **Gunicorn** behind a Unix socket.
- The `nginx/` folder contains a reverse proxy config that routes traffic to Gunicorn.
- If you use Docker, you’ll typically run **both** the app container and the Nginx container (e.g., with a `docker-compose.yml`).

## 🧩 Troubleshooting

- **No faces detected**: Try a clearer, front-facing clip with better lighting.
- **CUDA out of memory**: The `cuda_full.html` page is rendered if prediction fails. Try shorter videos or smaller sequence lengths.
- **dlib install issues on Windows**: Install a compatible wheel or Visual C++ Build Tools.

## 🔒 Security & production

- The project currently uses `DEBUG = True` and a hard-coded `SECRET_KEY` in `project_settings/settings.py`.
- For production, set `DEBUG = False`, configure `ALLOWED_HOSTS`, and supply a secure secret key via environment variables.

OR Copy your trained model to the models folder.

- You can download our trained models from the [Google Drive](https://drive.google.com/drive/folders/1UX8jXUXyEjhLLZ38tcgOwGsZ6XFSLDJ-?usp=sharing) or you can train your models using the steps mentioned in Model Creation directory.
