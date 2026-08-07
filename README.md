# AnemiaVision AI

AI-powered anemia screening platform for conjunctiva and fingernail image analysis using deep learning. The application provides anemia prediction, Grad-CAM explainability, PDF report generation, patient record management, and analytics through a Flask-based web application.

---

## Author

**Gunti Hemanth**

---

## Features

- 🩺 AI-assisted anemia screening from conjunctiva and fingernail images
- 🧠 EfficientNet-B3 transfer learning model
- 🔥 Grad-CAM visualization for model explainability
- 📄 Automatic PDF report generation
- 📊 Patient analytics dashboard
- 📱 Mobile-friendly image capture and upload
- 🧾 Patient history management with SQLite
- 📈 CSV export and search functionality
- 🚦 Rate-limited prediction API
- 🐳 Docker and Gunicorn deployment support

---

## Project Overview

AnemiaVision AI is designed to assist healthcare professionals by providing quick anemia risk assessment using smartphone images.

### Workflow

1. Upload or capture an eye conjunctiva or fingernail image.
2. Validate image quality.
3. Perform anemia prediction using EfficientNet-B3.
4. Generate Grad-CAM visualization.
5. Store patient information.
6. Generate downloadable PDF report.
7. View historical reports and analytics.

---

## Tech Stack

### Backend
- Flask
- Flask-SQLAlchemy
- Gunicorn

### Deep Learning
- PyTorch
- Torchvision
- EfficientNet-B3

### Frontend
- HTML
- Bootstrap 5
- Chart.js
- JavaScript

### Database
- SQLite

### Image Processing
- OpenCV
- Pillow

### Reports
- ReportLab

### Deployment
- Docker
- Docker Compose

---

## Dataset Structure

```
dataset/
├── train/
│   ├── anemic/
│   └── non-anemic/
├── valid/
│   ├── Anemia/
│   └── Non_Anemia/
└── test/
    ├── Anemic/
    └── Non-anemic/
```

The application automatically supports multiple folder naming conventions such as:

- anemic
- Anemic
- Anemia
- non-anemic
- Non-anemic
- Non_Anemia

Run dataset validation:

```bash
python utils/check_dataset.py
```

---

## Installation

### Clone Repository

```bash
git clone https://github.com/yourusername/anemia-detection.git
cd anemia-detection
```

### Create Virtual Environment

```bash
python -m venv .venv
```

Activate:

**Windows**

```bash
.venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Verify dataset:

```bash
python utils/check_dataset.py
```

---

## Docker

```bash
docker compose up --build
```

---

## Model Training

Train model

```bash
python train.py
```

Resume training

```bash
python train.py --resume models/last_checkpoint.pth
```

Evaluate model

```bash
python evaluate.py --split test
```

Generated artifacts:

- models/best_model.pth
- models/last_checkpoint.pth
- logs/training.log
- logs/evaluation/

---

## Running the Application

Development

```bash
python app.py
```

Production

```bash
gunicorn --bind 0.0.0.0:5000 --workers 2 app:app
```

Health endpoint

```
GET /health
```

---

## API Endpoint

### POST `/api/predict`

Example request

```json
{
  "image": "<base64-image>",
  "patient_name": "Aarav Kumar",
  "age": 25,
  "gender": "M",
  "phone": "9999999999",
  "image_type": "Eye Conjunctiva",
  "notes": "Fatigue for 2 weeks"
}
```

Example response

```json
{
  "success": true,
  "scan_id": 42,
  "prediction": "Non-Anemic",
  "confidence": 0.91,
  "risk_level": "Low Risk",
  "gradcam_url": "/static/gradcam/scan_042.jpg",
  "pdf_url": "/export/pdf/42"
}
```

---

## Project Structure

```
anemia-detection/
│
├── app.py
├── train.py
├── predict.py
├── evaluate.py
├── model.py
├── dataset.py
├── requirements.txt
├── templates/
├── static/
├── models/
├── reports/
├── database/
├── deploy/
├── utils/
└── Dockerfile
```

---

## Deployment

- Python 3.10
- Docker
- Docker Compose
- Gunicorn
- Flask

Persistent folders:

- database/
- models/
- reports/
- logs/
- static/uploads/
- static/gradcam/

---

## Future Improvements

- Multi-class anemia severity prediction
- Cloud deployment support
- Integration with Electronic Health Records (EHR)
- Mobile application
- Improved explainability methods
- Larger clinical dataset support

---

## License

This project is intended for academic and research purposes.

---

## Disclaimer

This application is intended for anemia screening assistance only and should not be considered a replacement for professional medical diagnosis. Clinical decisions should always be made by qualified healthcare professionals.