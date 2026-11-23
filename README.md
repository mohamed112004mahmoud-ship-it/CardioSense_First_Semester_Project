# CardioSense — Heart Disease Prediction App

CardioSense is a university project that combines a Flutter app with a machine-learning prediction service. Users can enter clinical measurements, request a heart-disease prediction, save cases to Firebase, review case history, and preview or share a PDF report.

> **Educational project only.** Predictions are not a medical diagnosis and must not be used to make treatment decisions.

## Features

- Email registration, verification, login, and logout with Firebase Authentication.
- A patient case form for 13 clinical features.
- Prediction requests to a Flask REST API (`POST /predict`).
- Per-user case history stored in Cloud Firestore, with case review and deletion.
- Prediction result and probability display.
- PDF report preview, printing, and sharing.

## Project components

- **Mobile app:** Flutter and Dart; Android and web platform files are included.
- **Machine learning:** `AI/train.py` compares Logistic Regression, Random Forest, and XGBoost using randomized hyperparameter search, then selects a model by ROC AUC.
- **Dataset:** `AI/heart.csv` contains 303 rows and 14 columns (13 features plus a binary `target`). It is based on the [UCI Heart Disease dataset](https://archive.ics.uci.edu/dataset/45/heart).
- **Saved model:** `AI/model.pkl` is included as a trained model artifact.
- **Backend integration:** The app calls a hosted Flask endpoint configured in `lib/Utils/constants.dart`. The Flask API source code is not included in this repository.
- **Cloud services:** Firebase Authentication and Cloud Firestore.

## Technology stack

Flutter, Dart, Python, Flask, scikit-learn, XGBoost, Pandas, NumPy, Firebase Authentication, and Cloud Firestore.

## Repository structure

```text
heart-disease-app-main/
├── AI/
│   ├── heart.csv
│   ├── model.pkl
│   ├── requirements.txt
│   └── train.py
├── Chart image/
├── assets/
├── android/
├── lib/
│   ├── screens/
│   ├── services/
│   ├── models/
│   ├── widgets/
│   └── main.dart
├── web/
└── pubspec.yaml
```

## Run the Flutter app

### Requirements

- Flutter SDK compatible with the Dart SDK constraint in `pubspec.yaml` (`>=3.0.0 <4.0.0`).
- Android Studio/Android SDK for Android, or a supported browser for Flutter web.
- Your own Firebase project.
- A reachable Flask prediction API implementing `POST /predict` and returning `prediction` and `probability` fields.

### Setup

1. Clone the repository and enter its folder.

   ```bash
   git clone <your-repository-url>
   cd heart-disease-app-main
   ```

2. Configure Firebase for your own project. Add the Firebase-generated `android/app/google-services.json` locally and update the Firebase options in `lib/main.dart`. Enable Email/Password sign-in and set Firestore rules so users can access only their own cases. The Firebase config file is ignored by Git and should not be committed.
3. Set the API base URL in `lib/Utils/constants.dart` to your deployed Flask API. The archived code points to a hosted Railway URL; its availability is not guaranteed.
4. Fetch Flutter dependencies and run the app.

   ```bash
   flutter pub get
   flutter run
   ```

The archive does not include `google-services.json` or the Flask API source, so you need to supply/configure those services to run the full prediction flow with your own accounts and deployment.

## Train the model

Run the training script from the `AI/` directory so it can find `heart.csv` and write `model.pkl` there.

```bash
cd AI
python -m pip install -r requirements.txt
python train.py
```

The requirements include XGBoost, which is imported by `train.py`. The script compares models using Accuracy, Precision, Recall, F1, and ROC AUC. No performance scores are listed because training output was not included in the archive.

## Screenshots

The project includes six screenshots in `Chart image/`:

![CardioSense screenshot 1](Chart%20image/Screenshot%202025-12-21%20151912.png)

![CardioSense screenshot 2](Chart%20image/Screenshot%202025-12-21%20151954.png)

![CardioSense screenshot 3](Chart%20image/Screenshot%202025-12-21%20152109.png)

![CardioSense screenshot 4](Chart%20image/Screenshot%202025-12-21%20152236.png)

![CardioSense screenshot 5](Chart%20image/Screenshot%202025-12-21%20152308.png)

![CardioSense screenshot 6](Chart%20image/Screenshot%202025-12-21%20152358.png)

## Team

As credited in the supplied project README:

- Mohamed Mahmoud Mohamed Ahmed
- Hassan Saleh Mohamed Ahmed
- Hassan Ayman Ramadan Abbas
- Ahmed AbdelKarim Abdelrahman
- Farouk Mohamed Mohamed Shabana
- Fares Mansour AbdElRouf

**Supervisor:** Dr. Zahraa Youssef

## License and medical-use note

This is an academic project. No open-source license is included; add a license file if you want to specify reuse permissions. The app is for educational demonstration only, not clinical diagnosis or medical advice.
