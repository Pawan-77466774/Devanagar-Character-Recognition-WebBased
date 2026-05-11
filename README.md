# Devanagari Character Recognition - Web Based

A web-based deep learning application for recognizing handwritten **Devanagari characters**, **Devanagari multi-digit numbers**, and **Nepali currency notes** from uploaded images, canvas drawings, or camera input.

The project combines a FastAPI backend, a deep learning recognition model, and a responsive vanilla HTML/CSS/JavaScript frontend to provide real-time predictions, confidence scores, Grad-CAM visualization, preprocessing outputs, voice feedback, and model evaluation metrics.

---

## Overview

This system is designed to help users recognize handwritten Devanagari characters through a simple browser interface. Users can upload an image, draw directly on a canvas, or capture an image using a camera. The backend processes the image, performs prediction using a trained deep learning model, and returns the predicted character along with helpful metadata such as transliteration, Nepali name, confidence level, top predictions, and visualization outputs.

The project also includes additional modules for:

- Multi-digit Devanagari number recognition
- Nepali currency note recognition
- Grad-CAM attention heatmap visualization
- Training and evaluation metric display
- Voice output and pronunciation support
- Prediction history and CSV export

---

## Features

### Character Recognition
- Recognizes handwritten Devanagari characters
- Supports image upload, drawing canvas, and camera capture
- Displays predicted character, romanized form, Nepali name, type, and example word
- Shows confidence score and confidence level
- Provides top 3 and top 5 prediction alternatives

### Multi-Digit Recognition
- Supports recognition of 2-8 Devanagari digits
- Works with uploaded images, drawing canvas, or camera input
- Displays detected digit count, full recognized number, and confidence
- Shows per-digit breakdown and segmentation output

### Nepali Currency Note Reader
- Supports Nepali note denomination recognition
- Handles common denominations such as Rs. 5, 10, 20, 50, 100, 500, and 1000
- Provides denomination metadata, Nepali numeral, color hint, and voice output

### Model Explainability
- Grad-CAM heatmap visualization
- Preprocessing pipeline display:
  - Original image
  - Grayscale image
  - Thresholded/processed image
  - Final model input

### Dashboard and Analytics
- Total prediction count
- Average confidence
- Highest confidence prediction
- Last prediction
- Confidence trend
- Prediction history
- CSV export option

### User Experience
- Light/dark theme support
- Drag-and-drop upload
- Camera capture
- Drawing canvas with stroke control
- Voice output using browser speech synthesis
- Feedback buttons for correct/wrong predictions

---

## Tech Stack

### Frontend
- HTML5
- CSS3
- Vanilla JavaScript
- Canvas API
- Browser Camera API
- Web Speech API

### Backend
- Python
- FastAPI
- Uvicorn
- Pydantic
- Python Multipart
- CORS Middleware

### Machine Learning
- TensorFlow / Keras
- NumPy
- OpenCV
- Pillow
- Scikit-learn
- Matplotlib
- Seaborn

---

## Project Structure

```text
Devanagar-Character-Recognition-WebBased/
│
├── backend/
│   ├── app.py
│   ├── predictor.py
│   ├── multidigit_predictor.py
│   ├── note_predictor.py
│   ├── character_metadata.py
│   ├── note_metadata.py
│   └── requirements.txt
│
├── frontend/
│   ├── index.html
│   ├── script.js
│   └── style.css
│
├── ml/
│   ├── model.py
│   ├── train.py
│   ├── evaluate.py
│   ├── generate_multidigit_dataset.py
│   ├── evaluate_multidigit.py
│   ├── note_model.py
│   └── train_note_model.py
│
├── requirements.txt
├── .gitignore
└── README.md
```

---

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Pawan-77466774/Devanagar-Character-Recognition-WebBased.git
cd Devanagar-Character-Recognition-WebBased
```

### 2. Create a Virtual Environment

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Running the Application

### 1. Start the Backend Server

```bash
cd backend
uvicorn app:app --reload --host 127.0.0.1 --port 8000
```

The backend will run at:

```text
http://127.0.0.1:8000
```

You can check whether the API is working by opening:

```text
http://127.0.0.1:8000/health
```

### 2. Start the Frontend

Open the `frontend/index.html` file directly in a browser.

Alternatively, you can serve the frontend locally:

```bash
cd frontend
python -m http.server 5500
```

Then open:

```text
http://127.0.0.1:5500
```

---

## Important Configuration

The frontend uses the following API base URL inside `frontend/script.js`:

```javascript
const API_BASE = "http://127.0.0.1:8000";
```

If your backend runs on another host or port, update this value accordingly.

---

## API Endpoints

### General

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | API root and endpoint list |
| GET | `/health` | Checks API and model status |
| GET | `/model-info` | Returns model architecture and parameter summary |
| GET | `/metrics` | Returns available training/evaluation artifact paths |
| GET | `/evaluation-summary` | Returns model evaluation summary |
| GET | `/training-history` | Returns training history |
| GET | `/session-stats` | Returns current session analytics |

### Character Recognition

| Method | Endpoint | Description |
|---|---|---|
| POST | `/predict` | Predicts a character from an uploaded image |
| POST | `/predict-base64` | Predicts a character from a base64 image |
| POST | `/batch-predict` | Predicts multiple images |
| GET | `/character-info/{label}` | Returns metadata for a character label |
| GET | `/voice-data/{label}` | Returns voice/pronunciation text |
| POST | `/feedback` | Stores user feedback on predictions |
| GET | `/feedback-stats` | Returns feedback statistics |

### Note Reader

| Method | Endpoint | Description |
|---|---|---|
| POST | `/predict-note` | Predicts Nepali currency note from uploaded image |
| POST | `/predict-note-base64` | Predicts Nepali currency note from base64 image |
| GET | `/note-info/{label}` | Returns metadata for a note denomination |
| GET | `/note-voice-data/{label}` | Returns voice text for note result |

### Multi-Digit Recognition

| Method | Endpoint | Description |
|---|---|---|
| POST | `/predict-multidigit` | Predicts multi-digit Devanagari number from uploaded image |
| POST | `/predict-multidigit-base64` | Predicts multi-digit Devanagari number from base64 image |

---

## Model Training

The `ml/` directory contains scripts for model development, training, evaluation, and multi-digit dataset generation.

Example commands:

```bash
cd ml
python train.py
python evaluate.py
```

For note recognition:

```bash
python train_note_model.py
```

For multi-digit dataset generation or evaluation:

```bash
python generate_multidigit_dataset.py
python evaluate_multidigit.py
```

After training, ensure the trained model and generated artifacts are available to the backend in the expected model/artifact directory.

---

## Expected Model Artifacts

The backend serves saved evaluation and visualization files from the model artifact directory. Depending on training output, this may include:

```text
training_plot.png
confusion_matrix.png
per_class_accuracy.png
lr_schedule.png
training_history.json
evaluation_summary.json
model_summary.txt
```

These files are used by the frontend to display model performance and explainability results.

---

## Usage Guide

1. Start the backend server.
2. Open the frontend in a browser.
3. Choose one input mode:
   - Upload
   - Draw
   - Camera
   - Note Reader
4. Select either:
   - Single Character
   - Multi-Digit Number
5. Provide an image or drawing.
6. Click **Predict**.
7. View the prediction, confidence score, top predictions, Grad-CAM output, and preprocessing pipeline.

---

## Screenshots

Add screenshots of your project here after running the application.

```markdown
![Home Page](screenshots/home.png)
![Prediction Result](screenshots/prediction.png)
![Grad-CAM Output](screenshots/gradcam.png)
```

Recommended screenshots:

- Home page
- Upload prediction result
- Drawing canvas prediction
- Camera prediction
- Note reader result
- Multi-digit recognition result
- Training metrics section

---

## Future Improvements

- Improve model accuracy with a larger and more balanced dataset
- Add user authentication for saving prediction history
- Store feedback in a database instead of memory
- Add deployment using Docker
- Improve camera preprocessing for low-light images
- Add support for more Nepali scripts, words, and full handwritten text recognition
- Deploy backend and frontend online

---

## Contributors

- Pawan-77466774

---

## License

This project currently does not specify a license. Add a license file if you want others to use, modify, or distribute the project.

---

## Acknowledgement

This project is developed as a deep learning based handwritten Devanagari recognition system with additional support for note reading, multi-digit recognition, model visualization, and educational metadata.
