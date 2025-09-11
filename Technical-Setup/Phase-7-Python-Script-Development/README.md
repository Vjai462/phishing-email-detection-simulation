## What We're Learning

In this phase, we learned how to use **Python and Machine Learning (ML)** to automatically detect phishing emails.

We built a simple model using a **public dataset** of phishing vs. safe emails, and wrote a Python script to train and test the model.

This phase teaches us:

- How datasets are used in ML.
- How to turn text (emails) into numerical features a computer can understand.
- How to train and test a classification model.
- How automation can assist a SOC analyst in identifying phishing attempts.

## Why This Phase Matters

SOC teams often receive large volumes of emails. A **phishing detector** can serve as a **first line of defense**, helping analysts prioritize alerts. Even a simple ML model shows how automation can reduce human workload and improve accuracy.


## Tools Needed

- **Operating System:** Kali Linux (VM)
- **Python 3.13** (already available on Kali)
- **Libraries:**
    - `pandas` (for handling datasets like spreadsheets)
    - `scikit-learn` (for ML algorithms)
- **Editor:** `nano` (for writing Python script)
- **Dataset:** Phishing Emails Dataset (CSV format)


## Step-by-Step Process

1. **Created Project Folder**
    - Made a directory `PhishDetector` on Desktop.
    - Inside it, created a virtual environment (`venv`).
2. **Installed Python Libraries in venv**
    - Installed `pandas` and `scikit-learn`.
3. **Added Dataset**
    - Downloaded phishing email dataset in CSV format.
    - Saved it as `phishing_dataset.csv` in `PhishDetector` folder.
4. **Created Script (detector.py)**
    - Wrote a Python script to:
        - Load dataset.
        - Split into training and testing data.
        - Convert text emails into numerical features.
        - Train a Naive Bayes model.
        - Test with new email samples.
5. **Ran the Script**
    - Activated venv and executed script: python detector.py
  
## Folder Structure

```
PhishDetector/
├── venv/                  → Virtual environment (don’t modify manually)
├── phishing_dataset.csv   → Dataset file
└── detector.py            → Python script

```

## Success Checkpoints

- Libraries installed without breaking system Python.
- Dataset loaded correctly (`Email Text` and `Email Type` columns visible).
- Model trained with 2000 emails (80% train, 20% test split).
- Accuracy reported: **100%** (small dataset).
- Custom test emails classified correctly (Phishing vs. Safe).

## Output / Results

- **Training set size:** 1600
- **Testing set size:** 400
- **Unique features (words):** 129
- **Model Accuracy:** 100%
- **Sample Predictions:**
    - *Phishing Email*: “Your account has been suspended. Click here…”
    - *Safe Email*: “Meeting is scheduled for tomorrow at 10 AM…”

## Key Concepts Learned

- **Dataset** = structured collection of labeled data (emails + phishing/safe label).
- **Vectorization** = converting text into numbers using word counts.
- **Naive Bayes Classifier** = simple ML model that predicts categories based on word probability.
- **Train/Test Split** = splitting dataset to measure model accuracy on unseen data.
- **Virtual Environment (venv)** = keeps libraries isolated and avoids system conflicts.


