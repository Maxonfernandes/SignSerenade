# SignSerenade

### Sign Language Learning Platform with YOLO & MediaPipe Integration

---

**Live Website:** [SignSerenade](https://sign-serenade.vercel.app/)

SignSerenade is an interactive sign language learning platform designed to make sign language learning more accessible through **gesture recognition, real-time sign detection, and interactive learning tools**.

Built using **Next.js** and **Python**, the platform integrates **YOLO-based object detection and MediaPipe-based hand landmark detection** to support sign language gesture recognition and validation. YOLO identifies supported gestures, while MediaPipe provides hand landmark tracking for gesture analysis and validation, enabling visual feedback through bounding boxes and hand landmarks.

## Features

* **Sign Language Recognition** — Detect and recognize supported sign language gestures using a YOLO model.
* **Real-Time Sign Detection** — Process camera input and display detected gestures with bounding boxes.
* **Hand Landmark Detection** — Use MediaPipe to detect and track hand landmarks for gesture analysis.
* **Interactive Learning** — Provide interactive tools to support sign language learning.
* **Quiz System** — Test knowledge and reinforce learning through quizzes.
* **Gesture Validation** — Validate sign language gestures using the implemented gesture recognition and landmark-processing components.
* **Text-to-Sign Translation** — Translate text into corresponding sign language videos.

## System Architecture

The following diagram illustrates the overall architecture of SignSerenade, including the user interface, Flask API, learning platform, translation components, video mapping, MediaPipe hand landmark detection, and YOLO-based gesture recognition.

System Architecture
flowchart TD
    U["User Interface"] --> API["Flask API"]

    API --> LP["Learning Platform"]
    API --> TR["Translate"]

    LP --> L["Lesson"]
    L --> P["Practice"]
    P --> MCQ["MCQ Quiz Generator"]
    P --> SV["Sign Validation"]

    TR --> VM["Video Mapping"]
    TR --> ML["MediaPipe Landmarks"]

    VM --> VIDEOS["Sign Videos"]
    ML --> YOLO["YOLO Model"]
    YOLO --> OUT["Text Output"]

    classDef core fill:#dbeafe,stroke:#2563eb,color:#172554,stroke-width:2px
    classDef learning fill:#dcfce7,stroke:#16a34a,color:#14532d,stroke-width:1.5px
    classDef translation fill:#f3e8ff,stroke:#9333ea,color:#581c87,stroke-width:1.5px

    class U,API core
    class LP,L,P,MCQ,SV learning
    class TR,VM,ML,VIDEOS,YOLO,OUT translation

## Demo Video

Watch the project demonstration to explore the user interface, learning features, and sign language detection capabilities.

[Watch the SignSerenade Demo](https://drive.google.com/file/d/1Df5bM2WIQDIt9xOVjM84RAOWNR5IGUsL/view)

## Research Paper

The research paper documenting the project is available in the `docs` directory.

[**Read the SignSerenade Research Paper (PDF)**](docs/research_paper.pdf)

## Technology Stack

| Category                    | Technologies                      |
| --------------------------- | --------------------------------- |
| **Frontend**                | Next.js, React                    |
| **Styling and Animations**  | Tailwind CSS, Framer Motion       |
| **Backend**                 | Python, Flask                     |
| **Computer Vision**         | OpenCV, MediaPipe                 |
| **Machine Learning**        | PyTorch, YOLO, Ultralytics        |
| **Hand Landmark Detection** | MediaPipe                         |
| **Containerization**        | Docker, Docker Compose (Optional) |

## Prerequisites

Before running the application, ensure the following dependencies are installed:

* **Node.js** 18 or later
* **npm**
* **Python** 3.8 or later, subject to compatibility with the installed dependencies
* **Docker and Docker Compose** (Optional)

## Installation and Setup

### Option 1: Using Docker Compose

**Step 1: Clone the repository**

```bash
git clone <repository-url>
cd SignSerenade
```

**Step 2: Configure the YOLO model**

Place the trained model file, `best(4).pt`, inside the `backend` directory.

**Step 3: Build and start the application**

```bash
docker-compose up --build
```

**Step 4: Access the application**

Once the services are running, open the frontend in your browser:

* **Frontend:** http://localhost:3001
* **Backend API:** http://localhost:3000

> **Note:** Ensure that the Docker Compose configuration maps the frontend and backend to the appropriate ports.

### Option 2: Manual Setup

#### 1. Backend Setup

Navigate to the backend directory:

```bash
cd backend
```

Install the required Python dependencies:

```bash
pip install -r requirements.txt
```

Place the trained YOLO model file, `best(4).pt`, in the `backend` directory.

Ensure that the required MediaPipe dependencies are installed as specified in `requirements.txt`.

Start the Flask server:

```bash
python app.py
```

The backend API should be available at http://localhost:3000.

#### 2. Frontend Setup

Open a separate terminal in the project root directory.

Install the frontend dependencies:

```bash
npm install
```

Create a `.env.local` file in the project root and add the following configuration:

```env
NEXT_PUBLIC_API_URL=http://localhost:3000
```

Start the Next.js development server:

```bash
npm run dev
```

Access the frontend at http://localhost:3001.

> **Note:** If Next.js starts on a different port, configure the development server to use port `3001`.

## Usage

1. Start the application by running both the frontend and backend services.
2. Open the frontend in your browser.
3. Navigate to the **Detection** page.
4. Grant camera access when prompted.
5. Perform a supported sign language gesture in front of the camera.
6. View detected gestures, bounding boxes, and hand landmarks where supported by the implementation.
7. Explore the available learning tools, quizzes, gesture validation, and text-to-sign translation features.

**Recognition performance** depends on the trained model, supported gestures, hand landmark detection, lighting conditions, camera quality, and the implementation of the recognition pipeline.

## API Reference

The Flask backend provides the following endpoints:

| Endpoint           | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `/health`          | Checks backend health and model-loading status.          |
| `/detect`          | Detects signs in an image.                               |
| `/classify_action` | Classifies sign language gestures or actions.            |
| `/video_feed`      | Streams camera video for real-time detection.            |
| `/translate`       | Translates text into corresponding sign language videos. |
| `/validate`        | Validates sign language gestures.                        |
| `/quiz`            | Retrieves quiz data for learning activities.             |

> **Note:** Supported HTTP methods, request parameters, and response formats depend on the implementation in `backend/app.py`.

## Project Structure

The project includes a Next.js frontend, a Python Flask backend, and supporting documentation.

```text
SignSerenade/
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── best(4).pt
├── docs/
│   ├── architecture.png
│   └── research_paper.pdf
├── public/
├── app/
├── pages/
├── package.json
├── .env.local
├── docker-compose.yml
├── README.md
└── LICENSE
```

*Note: The directory structure is illustrative. Adjust it to match the actual repository layout.*

## Configuration

| File or Variable           | Description                                                                                            |
| -------------------------- | ------------------------------------------------------------------------------------------------------ |
| `NEXT_PUBLIC_API_URL`      | Specifies the backend API URL used by the frontend.                                                    |
| `backend/best(4).pt`       | Trained YOLO model used for sign detection.                                                            |
| `backend/requirements.txt` | Lists the Python dependencies required by the backend, including MediaPipe if used by the application. |
| `docker-compose.yml`       | Defines the services and configuration for containerized deployment.                                   |
| `docs/architecture.png`    | System architecture diagram.                                                                           |
| `docs/research_paper.pdf`  | Research paper documenting the project.                                                                |

Ensure that the API URL, model path, dependency versions, and port configuration match your local environment.

## Docker Commands

| Command                        | Description                                          |
| ------------------------------ | ---------------------------------------------------- |
| `docker-compose up --build`    | Builds and starts the application.                   |
| `docker-compose up -d --build` | Builds and starts the application in the background. |
| `docker-compose down`          | Stops and removes the application containers.        |

## License

Refer to the [`LICENSE`](LICENSE) file for licensing information.

---

**SignSerenade — Making sign language learning more accessible through computer vision and interactive technology.**

**Live Application:** https://sign-serenade.vercel.app/
