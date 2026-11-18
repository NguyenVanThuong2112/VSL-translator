# 🤟 Vietnamese Sign Language (VSL) Translator

![Python](https://img.shields.io/badge/python-3.12-blue.svg)
![MediaPipe](https://img.shields.io/badge/MediaPipe-hand_tracking-green)
![OpenCV](https://img.shields.io/badge/OpenCV-computer_vision-red)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Random_Forest-orange)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)
![License](https://img.shields.io/badge/license-MIT-green)

A real-time desktop application that translates **Vietnamese Sign Language (VSL)** hand signs into text and speech. It tracks the hand from a webcam with **MediaPipe**, classifies each sign with a **Scikit-Learn** Random Forest (**99.39% test accuracy** on a held-out split, see [caveat](#-model-performance)), and shows the result in a **Tkinter** interface.

The repository covers the whole workflow: collecting a dataset, extracting hand landmarks, training and comparing models, and running the app live.

## 🎬 Demo

*Real-time recognition of VSL hand gestures from a webcam.*
https://github.com/user-attachments/assets/bdc859c4-3434-4ecd-b81c-460e05383d05

## 🎯 Scope

The model recognizes **23 static hand signs for Vietnamese letters**: a, b, c, d, đ (typed as `dd`), e, g, h, i, k, l, m, n, o, p, q, r, s, t, u, v, x, y.

Recognized letters are combined into words, and a word suggester (dictionary of about 79,000 Vietnamese words) proposes completions.

**Not supported:** full sentences, continuous signing, and letters outside the 23 classes above.

## ✨ Features

- **Real-time recognition** from the webcam feed (about 19 FPS on the author's laptop).
- **Stable output:** a letter is confirmed only after it is detected on 15 consecutive frames, which reduces accidental detections.
- **Word suggester** (`src/word_suggester.py`) that completes Vietnamese words from the recognized letters.
- **Text-to-speech:** reads the translated text aloud with `pyttsx3`.
- **Tkinter GUI** (`src/gui.py`), lightweight and easy to use.
- **Custom training pipeline:** scripts and a notebook to collect your own signs and train a new model.

## 🔬 How It Works

1. **Capture:** OpenCV reads frames from the webcam.
2. **Hand tracking:** MediaPipe HandLandmarker detects the hand and returns 21 landmarks. Their x and y coordinates give **42 features** per frame.
3. **Classification:** a Random Forest predicts one of the 23 letters.
4. **Confirmation:** the letter is added to the text only after 15 consecutive frames agree.
5. **Output:** the word suggester proposes completions, and `pyttsx3` can speak the text.

## 📊 Model Performance

| Item | Value |
|---|---|
| Classes | 23 static letter signs |
| Samples | 40,300 (about 1,470–1,800 per class) |
| Features | 42 (x, y of 21 MediaPipe hand landmarks, one hand) |
| Split | 80% train / 20% test (8,060 samples), stratified random split |
| Training data | Rotation (±15°) and Gaussian noise (0.02): 32,240 → 96,720 samples |
| Chosen model | Random Forest (100 trees, max depth 15) |
| **Test accuracy** | **99.39%** |
| 5-fold CV accuracy | 98.84% |

Comparison of the three classifiers I trained:

| Model | CV accuracy | Test accuracy |
|---|---|---|
| **Random Forest** | 98.84% | **99.39%** |
| Decision Tree | 95.65% | 99.31% |
| SVM (Linear) | 98.15% | 98.98% |

> **Caveat:** the test set is a random split of frames. Similar frames from the same recording can appear in both the training and test sets, so these numbers are likely higher than what you would see with a new user or different lighting.

**Runtime** (author's Windows laptop, 31 sessions): about 19 FPS on average and 13–19 ms of processing time per frame.

## 📁 Repository Structure

```
VSL-translator/
├── data/
│   ├── collect_images.py       # Capture hand images via webcam
│   ├── create_dataset.py       # Extract MediaPipe landmarks and build the dataset
│   ├── words.csv               # Vocabulary dictionary for the word suggester
│   └── download_dataset.txt    # Link to the dataset (VSL.pickle)
├── docs/                       # Version history and development notes
├── legacy/                     # Earlier versions kept for reference
├── models/
│   └── model.p                 # Trained Random Forest used by the app
├── notebooks/
│   └── model_final.ipynb       # Train, compare and evaluate models
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

Tested on **Windows with Python 3.12**. Text-to-speech uses the Windows speech engine, so other platforms may need changes.

**1. Clone the repository**

```bash
git clone https://github.com/NguyenVanThuong2112/VSL-translator.git
cd VSL-translator
```

**2. Install dependencies**

```bash
pip install -r requirements.txt
```

The model was trained with `scikit-learn==1.5.2`. Use that version to avoid errors when loading it.

**3. Get the pre-trained model**

The app loads `models/model.p` (Random Forest, about 99 MB). If the file is not in the repository because of its size, download it from the [Releases](https://github.com/NguyenVanThuong2112/VSL-translator/releases) page and put it in the `models/` folder.

**4. First run**

On the first launch the app downloads MediaPipe's `hand_landmarker.task` automatically, so an internet connection is needed once.

## 🚀 Usage

### Run the application

```bash
python main.py
```

A webcam is required. Show a sign and hold it steady for a moment until the letter is confirmed.

### Train your own signs

1. **Collect images:** `python data/collect_images.py` opens the webcam and captures images for each class.
2. **Build the dataset:** `python data/create_dataset.py` extracts hand landmarks with MediaPipe and saves them as `VSL.pickle`.
3. **Train:** open `notebooks/model_final.ipynb`, set `DATA_PATH` to your dataset and `MODEL_SAVE_PATH` to where the model should be saved. The notebook applies augmentation, compares Random Forest, Decision Tree and SVM, and saves the best model.
4. **Use it:** rename the saved model to `model.p` and put it in `models/`.

## ⚠️ Limitations

- Recognizes **individual static letter signs** only, using a **single hand**.
- Evaluated on a random split of frames, so accuracy for new users or lighting conditions is not measured.
- Tested only on Windows with Python 3.12.
- Processing time occasionally spikes above 100 ms, which can make the video stutter.
- A sign must be held for 15 consecutive frames (roughly 0.7 seconds at 20 FPS), so fast spelling is not supported.

## 🗺️ Future Work

- Collect data from more signers and lighting conditions, and evaluate on a separate test recording.
- Add more signs, such as modified vowels.
- Reduce the model size (for example with compression or a lighter classifier).

## 🤝 Contributing

Issues and pull requests are welcome. For larger changes, please open an issue first to discuss what you would like to change.

## 📝 License

Released under the [MIT License](LICENSE).

## 👤 Author

**Nguyễn Văn Thương** · [@NguyenVanThuong2112](https://github.com/NguyenVanThuong2112)
