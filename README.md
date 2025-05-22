ASL Live Sign Language Recognition

  

An end-to-end American Sign Language (ASL) recognition system that:

Captures real-time video from your webcam

Uses MediaPipe Hands to extract 63-dimensional hand landmarks

Classifies ASL letters with a pretrained XGBoost model

Displays predictions and builds complete sentences on-screen

Logs each scanned phrase with a timestamp into a SQLite database

🔍 Features

Real-time Detection: Instant hand-pose estimation and classification at webcam speeds.

High Accuracy: Over 99% validation accuracy on a 29-class ASL alphabet dataset.

Sentence Builder: Automatically groups detected letters into sentences, with support for spaces.

Confidence Thresholding: Only appends letters when confidence ≥ 0.8, avoiding false positives.

Persistent Logging: Saves every scanned sentence with a timestamp into scanned_texts.db.

Lightweight & Portable: Pure Python dependencies, no GPU required.

🚀 Getting Started

Prerequisites

Python 3.9 or higher

Webcam (built-in or USB)

Installation

Clone this repository

git clone https://github.com/yourusername/asl-live-recognition.git
cd asl-live-recognition

Create a virtual environment (optional but recommended)

python -m venv venv
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate     # Windows

Install dependencies

pip install -r requirements.txt

▶️ Usage

Train & save your XGBoost model (if you haven’t already):

python train_model.py

Produces asl_xgb_model.json in the project root.

Run live recognition:

python live_recognition.py

Controls:

Press e to exit the application.

Detected letters with confidence ≥ 0.8 are appended to the sentence.

Space sign (space) is inserted as an actual space in the sentence.

View logs:

sqlite3 scanned_texts.db
sqlite> SELECT * FROM scans;

🛠 How It Works

MediaPipe Hands extracts 21 3D landmarks (x, y, z) of the detected hand.

Landmarks are flattened into a 63-dimensional feature vector.

XGBoost predicts one of 29 classes: A–Z, nothing, or space.

Letters are buffered into a sentence string when the model’s confidence ≥ 0.8.

On exit, the scanned sentence + timestamp is inserted into a SQLite table for persistence.

📂 Project Structure

├── train_model.py         # Trains & saves the XGBoost model
├── live_recognition.py    # Real-time ASL detection & logging
├── requirements.txt       # Python dependencies
├── scanned_texts.db       # SQLite database (auto-generated)
├── asl_xgb_model.json     # Pretrained XGBoost model file
└── README.md              # Project documentation

🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to:

Fork this repository

Create a pull request

Star the project ⭐


Built with ❤️ by Mohamed Adel

