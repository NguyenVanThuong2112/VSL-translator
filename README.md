# VSL-translator
Vietnamese Sign Language (VSL) Recognition System 🤟

📌 Overview

This project is an AI-powered system designed to recognize and translate Vietnamese Sign Language (VSL) into text. By utilizing computer vision and machine learning (packaged in VSL.pickle), the system aims to bridge the communication gap for the deaf and hard-of-hearing community in Vietnam.

✨ Features

Real-time Recognition: Translates sign language gestures into text/voice in real-time using webcam input.

Pre-trained Model: Includes a lightweight, pre-trained machine learning model (VSL.pickle) for quick deployment.

Customizable Layout: Features an adaptable user interface (currently updated to V2.3).

📂 Project Structure

To keep the repository clean and maintainable, the project files are organized as follows:

├── data/                   # Raw and processed datasets (if any)
├── docs/                   # Documentation and project planning
│   ├── CHANGES.txt         # Changelog history
│   ├── LAYOUT_CHANGE_V2.3.txt  # Details on UI layout updates
│   └── UPDATE_PLAN.md      # Future development plans
├── models/                 # Pre-trained models
│   └── VSL.pickle          # The core Machine Learning model
├── src/                    # Source code files (.py)
│   └── main.py             # Main application script
├── .gitignore              # Files to be ignored by Git
├── requirements.txt        # Python dependencies
└── README.md               # Project overview and setup guide


🚀 Installation & Setup

1. Clone the repository:

git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name


2. Create a virtual environment (Recommended):

python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate


3. Install dependencies:

pip install -r requirements.txt


💻 Usage

To run the application, execute the main script from the root directory:

python src/main.py


(Note: Ensure your webcam is connected and accessible if the project requires real-time camera input).

🗺️ Roadmap & Updates

Please refer to the docs/UPDATE_PLAN.md file for our upcoming features and docs/CHANGES.txt for the version history.

🤝 Contributing

Contributions are welcome! If you have suggestions to improve this project, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".

📜 License

Distributed under the MIT License. See LICENSE for more information.
