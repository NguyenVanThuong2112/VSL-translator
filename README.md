# 🤟 Vietnamese Sign Language (VSL) Translator

![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)
![MediaPipe](https://img.shields.io/badge/MediaPipe-hand_tracking-green)
![OpenCV](https://img.shields.io/badge/OpenCV-computer_vision-red)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-classifier-orange)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

A real-time desktop application that translates **Vietnamese Sign Language (VSL)** hand gestures into text and speech. It uses **MediaPipe** to track the hand from a webcam, **Scikit-Learn** to classify each gesture, and a **Tkinter** interface to show the result.

The repository covers the whole workflow: collecting a dataset, extracting hand landmarks, training a model, and running it live.

## 🎬 Demo

*Real-time recognition of VSL hand gestures from a webcam.*
https://github.com/user-attachments/assets/bdc859c4-3434-4ecd-b81c-460e05383d05




## 🎯 Scope

This project recognizes **individual VSL hand signs for letters** (the Vietnamese alphabet, [N] classes in total). Recognized letters are combined into Vietnamese words, and a word suggester (dictionary of about 79,000 words) proposes completions.

**Not supported:** full sentences, continuous signing, and signs that depend on facial expression or movement.

## ✨ Features

- **Real-time recognition:** reads the webcam feed and classifies VSL hand gestures instantly.
- **Tkinter GUI:** a lightweight, easy-to-use interface (`src/gui.py`).
- **Word suggester:** suggests complete Vietnamese words from the recognized characters (`src/word_suggester.py`).
- **Text-to-speech:** reads the translated Vietnamese text aloud with `pyttsx3`.
- **Custom training pipeline:** scripts to collect your own gestures and train a new model (`data/collect_images.py`, `data/create_dataset.py`).

## 📊 Model Performance

<!-- TODO: fill in with your real numbers and delete any row you cannot back up. -->

| Item | Value |
|---|---|
| Number of classes | [X] |
| Number of samples | [X] |
| Classifier | [e.g. Random Forest] |
| Features | MediaPipe hand landmarks |
| Test accuracy | [X]% |

## 🔬 How It Works

1. **Capture:** OpenCV reads frames from the webcam.
2. **Hand tracking:** MediaPipe detects the hand and returns 21 landmark points.
3. **Classification:** the landmark coordinates are fed to a Scikit-Learn classifier that predicts the sign.
4. **Output:** the predicted character is added to the text, the word suggester proposes completions, and `pyttsx3` can speak the result.

## 📁 Repository Structure

```
VSL-translator/
├── data/
│   ├── collect_images.py       # Capture hand images via webcam
│   ├── create_dataset.py       # Extract MediaPipe landmarks and save the dataset
│   ├── words.csv               # Vocabulary dictionary
│   └── download_dataset.txt    # Link to the full raw dataset
├── docs/                       # Version history and development notes
├── legacy/                     # [TODO: one line on what this contains]
├── models/
│   ├── model.p                 # Trained classifier
│   └── download_model.txt      # Link to download the main model
├── notebooks/
│   └── model_testing.ipynb     # Train and evaluate models
├── src/
│   ├── backend.py              # Inference engine and MediaPipe wrapper
│   ├── config.py               # App settings (colors, thresholds, ...)
│   ├── gui.py                  # Tkinter UI
│   └── word_suggester.py       # Word suggestion algorithm
├── tests/
├── requirements.txt
└── main.py                     # Entry point
```

## ⚙️ Installation

**1. Clone the repository**

```bash
git clone https://github.com/NguyenVanThuong2112/VSL-translator.git
cd VSL-translator
```

**2. Install dependencies**

```bash
pip install -r requirements.txt
```

**3. Download the pre-trained model**

The main model is too large for the repository. Open `models/download_model.txt`, download the file from the link, and place it in the `models/` folder.

<!-- TODO: use one model file name everywhere (model.p or VSL.pickle) and make sure it matches the path in src/config.py. -->

## 🚀 Usage

### Run the application

```bash
python main.py
```

A webcam is required.

### Train your own gestures

1. **Collect data:** `python data/collect_images.py` opens the webcam and captures images for each new class.
2. **Build the dataset:** `python data/create_dataset.py` extracts hand landmarks with MediaPipe and saves them.
3. **Train:** open `notebooks/model_testing.ipynb`, train a Scikit-Learn classifier on your data, and export the new model into `models/`.

### Run the tests

<!-- TODO: replace with the real command, e.g. `pytest tests/` -->

## ⚠️ Limitations

<!-- TODO: edit to match what you observed. Examples: -->
- Accuracy depends on lighting and background.
- [One hand / both hands] supported.
- Recognizes individual signs only, not continuous signing or full sentences.
- Trained on a limited number of signers, so it may perform worse for hand shapes and styles it has not seen.

## 🗺️ Roadmap

<!-- TODO: 2-3 real next steps, e.g. add more signs, support two hands, improve the word suggester. See docs/UPDATE_PLAN.md. -->

## 🤝 Contributing

Issues and pull requests are welcome. If you plan a larger change, please open an issue first to discuss it.

## 📝 License

This project is released under the [MIT License](LICENSE).

## 👤 Author

**Nguyễn Văn Thương** (check the spelling of your name) · [@NguyenVanThuong2112](https://github.com/NguyenVanThuong2112)
<!-- TODO: add email or LinkedIn. -->
