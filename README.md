# 🔴 RedRuby Enterprise – AI-Powered Employee Surveillance & Tracking System

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-green)
![React](https://img.shields.io/badge/React-19-61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-6-blue)
![YOLO](https://img.shields.io/badge/YOLOv8-Person%20Detection-purple)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-red)

## 📌 Project Overview

RedRuby Enterprise is an AI-powered employee surveillance and tracking system designed to detect, recognize, and track employees and unknown individuals from uploaded video footage and images.

The system integrates deep learning, computer vision, face recognition, and Person Re-Identification (ReID) to identify individuals and maintain consistent identities even when they temporarily disappear from the camera frame or reappear in different video footage.

The platform provides a modern enterprise dashboard for monitoring employee activity, tracking unknown visitors, analyzing images, comparing two videos, and viewing real-time detection events.

## ✨ Key Features

### 1. Real-Time Employee Detection and Tracking
- Detects people using YOLOv8.
- Tracks multiple individuals using ByteTrack.
- Assigns unique tracking IDs to detected individuals.
- Processes uploaded video footage frame by frame.
- Displays detection progress and processing statistics.

### 2. Face Recognition
- Uses InsightFace for facial recognition.
- Automatically enrolls employees from stored reference images.
- Generates facial embeddings.
- Matches detected faces against registered employees.
- Uses confidence thresholds to reduce incorrect identity assignments.
- Identifies unrecognized individuals as unknown visitors.

### 3. Person Re-Identification (ReID)
- Uses OSNet-x0.25 for body feature extraction.
- Generates body appearance embeddings.
- Matches individuals when facial information is unavailable.
- Maintains identity consistency across temporary disappearances.
- Supports employee recognition using multiple reference images.

### 4. Persistent Unknown Person Tracking
- Assigns unique IDs such as `UNK-1`, `UNK-2`, etc.
- Maintains unknown-person identities across multiple videos.
- Uses cosine similarity for embedding comparison.
- Stores identity embeddings in a persistent JSON database.
- Maintains a rolling gallery of up to 15 embeddings per unknown person.
- Separates permanent internal IDs from session display IDs.

### 5. Dual Video Comparison
- Upload two videos simultaneously.
- Process both video streams independently.
- Compare unknown-person identities across videos.
- Identify repeated appearances using ReID embeddings.
- Display processing progress for both videos.

### 6. Image Analysis
- Upload individual images for person detection.
- Identify known employees using face recognition.
- Apply body ReID for unknown-person matching.
- Generate annotated images with bounding boxes.
- Display individual person snapshots.
- Generate detection summaries and confidence information.
- Maintain an isolated unknown-person gallery for image analysis.

### 7. Employee Management
- Automatically loads employee reference images.
- Displays registered employees and detected unknown individuals.
- Shows employee identification confidence.
- Tracks first-seen and last-seen timestamps.
- Displays detection counts and snapshots.
- Supports CSV and JSON data export.

### 8. Enterprise Dashboard
- Displays known employee statistics.
- Monitors unknown visitors.
- Shows real-time detection alerts.
- Provides WebSocket-based dashboard updates.
- Displays video processing progress.
- Includes configurable detection and recognition settings.

## 🧠 Technologies Used

| Component | Technology |
|---|---|
| Programming Language | Python |
| Frontend | React 19, TypeScript |
| Backend | FastAPI |
| Object Detection | YOLOv8 |
| Multi-Object Tracking | ByteTrack |
| Face Recognition | InsightFace |
| Person Re-Identification | OSNet-x0.25 |
| Image Processing | OpenCV |
| Deep Learning | PyTorch |
| Feature Matching | Cosine Similarity |
| Real-Time Communication | WebSockets |
| Data Storage | JSON |
| Build Tool | Vite |
| Visualization | Recharts |
| UI Icons | Lucide React |

## 🏗️ System Architecture

The system follows a modular AI processing architecture.

```text
             VIDEO / IMAGE INPUT
                     |
                     v
              YOLOv8 DETECTION
                     |
                     v
              PERSON TRACKING
                  ByteTrack
                     |
                     v
              PERSON CROPPING
                     |
          +----------+----------+
          |                     |
          v                     v
    FACE RECOGNITION        BODY ReID
      InsightFace          OSNet-x0.25
          |                     |
          +----------+----------+
                     |
                     v
              IDENTITY FUSION
                     |
             +-------+-------+
             |               |
             v               v
        KNOWN EMPLOYEE   UNKNOWN PERSON
             |               |
             v               v
       Employee ID       Persistent
       Recognition       Unknown ID
             |               |
             +-------+-------+
                     |
                     v
             SNAPSHOT STORAGE
                     |
                     v
             FASTAPI BACKEND
                     |
                     v
              WEBSOCKET UPDATES
                     |
                     v
             REACT DASHBOARD
```

## 📂 Project Structure

```text
redruby-enterprise/
│
├── backend/
│   ├── app.py
│   ├── config.py
│   ├── detector.py
│   ├── tracker.py
│   ├── reid.py
│   ├── face_recognition_module.py
│   ├── unknown_tracker.py
│   ├── employee_loader.py
│   ├── image_analysis.py
│   ├── snapshot_quality.py
│   ├── websocket_manager.py
│   │
│   ├── employees/
│   │   ├── EMP001_MEERA/
│   │   │   ├── meera1.jpeg
│   │   │   └── meera2.jpeg
│   │   │
│   │   └── EMP003_SHERIN/
│   │       ├── sherin1.jpeg
│   │       └── sherin2.jpeg
│   │
│   ├── uploads/
│   ├── snapshots/
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── StatCard.tsx
│   │   │   ├── PersonCard.tsx
│   │   │   └── Sidebar.tsx
│   │   │
│   │   ├── data/
│   │   │   └── index.tsx
│   │   │
│   │   ├── pages/
│   │   │   ├── DashboardPage.tsx
│   │   │   ├── DualVideoPage.tsx
│   │   │   ├── ImageAnalysisPage.tsx
│   │   │   ├── EmployeesPage.tsx
│   │   │   └── SettingsPage.tsx
│   │   │
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   └── index.css
│   │
│   ├── package.json
│   └── vite.config.ts
│
├── start.bat
└── README.md
```

## ⚙️ Installation and Setup

### Prerequisites

Install the following:

- Python 3.10 or above
- Node.js and npm
- Git (optional)
- NVIDIA GPU with CUDA support (recommended)
- Windows 10/11 or Linux

### Step 1: Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd redruby-enterprise
```

### Step 2: Create a Python Virtual Environment

```bash
python -m venv .venv
```

Activate the environment.

**Windows:**

```bash
.venv\Scripts\activate
```

**Linux/macOS:**

```bash
source .venv/bin/activate
```

### Step 3: Install Backend Dependencies

```bash
cd backend
pip install -r requirements.txt
```

Important dependencies include:

```text
fastapi
uvicorn
opencv-python
ultralytics
supervision
insightface
onnxruntime
torch
torchvision
torchreid
numpy
python-multipart
```

For GPU acceleration, install compatible CUDA-enabled PyTorch and ONNX Runtime GPU packages as required by your hardware and dependency versions.

### Step 4: Install Frontend Dependencies

Open another terminal:

```bash
cd frontend
npm install
```

### Step 5: Start the Application

Return to the project root and execute:

```bat
start.bat
```

The startup script automatically:

1. Clears existing processes on ports 8003 and 5173.
2. Starts the FastAPI backend.
3. Starts the React frontend.
4. Opens the application in your browser.

## 🌐 Application URLs

| Service | URL |
|---|---|
| Frontend Dashboard | http://localhost:5173 |
| Backend API | http://localhost:8003 |
| Swagger Documentation | http://localhost:8003/docs |
| WebSocket | ws://localhost:8003/ws |

## 👥 Adding New Employees

The system automatically enrolls employees using reference images stored in the backend employee directory.

Create a folder using the following format:

```text
backend/employees/
│
├── EMP001_EmployeeName/
│   ├── image1.jpg
│   ├── image2.jpg
│   └── image3.jpg
│
└── EMP002_EmployeeName/
    ├── image1.jpg
    └── image2.jpg
```

### Enrollment Process

1. Create an employee folder.
2. Use the format `EMPXXX_Name`.
3. Add multiple clear reference images.
4. Restart the backend.
5. The system automatically extracts facial and body embeddings.
6. The employee becomes available for recognition.

## 🔧 Configuration and Model Parameters

The system provides configurable parameters through `backend/config.py`.

| Parameter | Default | Description |
|---|---:|---|
| YOLO Model | yolov8m.pt | Person detection model |
| YOLO Confidence | 0.45 | Detection confidence threshold |
| Process Every N Frames | 3 | Frame processing interval |
| ByteTrack Buffer | 60 | Lost-track retention buffer |
| Face Model | buffalo_l | InsightFace recognition model |
| Face Confidence | 0.50 | Face similarity threshold |
| Face Margin | 0.08 | Minimum separation from runner-up |
| ReID Model | osnet_x0_25 | Body ReID model |
| ReID Threshold | 0.65 | Employee ReID threshold |
| Unknown ReID Threshold | 0.60 | Unknown identity matching threshold |
| ReID Gallery Size | 15 | Maximum stored embeddings per unknown |

These parameters can be adjusted according to the camera quality, environment, and processing hardware.

## 🔌 Backend API Endpoints

The FastAPI backend exposes the following endpoints.

| Method | Endpoint | Description |
|---|---|---|
| GET | `/cameras` | Retrieve camera information |
| GET | `/employees` | Retrieve recognized employees |
| GET | `/unknowns` | Retrieve unknown persons |
| GET | `/events` | Retrieve detection events |
| GET | `/settings` | Retrieve system settings |
| POST | `/settings` | Update system settings |
| POST | `/reset` | Reset dashboard session |
| POST | `/upload-video` | Upload and process a video |
| POST | `/upload-dual-video` | Upload two videos |
| POST | `/analyze-image` | Analyze a single image |
| POST | `/compare-images` | Compare two images |
| WS | `/ws` | Real-time dashboard communication |

API documentation:

http://localhost:8003/docs

## 🔄 Persistent Unknown Person Identification

One of the important features of RedRuby Enterprise is persistent unknown-person identification.

When an unknown individual is detected:

1. The system extracts the person's body embedding.
2. It compares the embedding with previously stored unknown identities.
3. Cosine similarity determines whether the person matches an existing identity.
4. If a match exceeds the configured threshold, the existing identity is reused.
5. Otherwise, a new unknown identity is created.
6. The identity gallery is saved to JSON for future sessions.

The persistent identity database is stored in:

```text
backend/unknowns_db.json
```

Image analysis uses a separate database:

```text
backend/unknowns_db_images.json
```

This separation prevents image-analysis identities from interfering with video-tracking identities.

## 📊 Expected Outputs

The dashboard provides:

- Detected employee names and employee IDs.
- Persistent unknown-person IDs.
- Person snapshots and cropped images.
- Face recognition confidence.
- Body ReID confidence.
- Detection counts and timestamps.
- Video processing progress.
- Cross-video identity matching.
- Annotated image outputs.
- Real-time detection events.

## ⚠️ Important Notes

- YOLO model weights may be downloaded automatically on the first execution.
- InsightFace and OSNet pretrained weights may require initial model downloads.
- A CUDA-compatible environment is recommended for faster processing.
- Employee reference images should be clear and sufficiently varied.
- Recognition accuracy depends on lighting, image resolution, occlusion, and camera angle.
- Unknown-person identification relies on body appearance similarity and is not guaranteed to be correct.
- The project processes uploaded video and image files; live CCTV camera integration is not included in the current implementation.
- The supplied project does not include a dedicated automated test suite.

## 🔮 Future Enhancements

- Live CCTV camera integration.
- Multi-camera real-time employee tracking.
- Improved ReID accuracy under significant appearance changes.
- Advanced identity fusion between face and body embeddings.
- Database-backed employee management.
- Automated attendance management.
- Email and SMS notifications.
- Role-based authentication and access control.
- Advanced analytics and employee movement reports.

## 🔐 Privacy and Security

This project processes facial images and biometric embeddings. Deploy it only with appropriate authorization and informed consent, where required.

- Protect employee reference images and biometric data.
- Restrict access to surveillance records.
- Secure uploaded videos and generated snapshots.
- Apply appropriate retention and deletion policies.
- Follow applicable privacy and data protection laws.

## 📄 License

This project is developed for academic and educational purposes. Add an appropriate open-source license before public distribution.
