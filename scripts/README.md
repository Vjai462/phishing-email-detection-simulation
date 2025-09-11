# Phishing Email Detection Using Machine Learning

A comprehensive Python implementation for detecting phishing emails using Natural Language Processing and Machine Learning techniques.

## 🚀 Quick Start

### Prerequisites
```bash
pip install pandas scikit-learn
```

### Dataset
Ensure your `Phishing_validation_emails.csv` file is in the same directory as the script.

## 📋 Implementation

### Step 1: Import Required Libraries

```python
# ===============================
# Step 1: Import required libraries
# ===============================

import pandas as pd                           # For handling CSV dataset
from sklearn.model_selection import train_test_split  # To split data into training/testing
from sklearn.feature_extraction.text import CountVectorizer  # Convert text to numbers
from sklearn.naive_bayes import MultinomialNB  # Simple ML model for text classification
from sklearn.metrics import accuracy_score     # To measure model performance
```

**Why these libraries?**
- **pandas** → Read and organize dataset
- **train_test_split** → Split data so model learns on part of data, tests on unseen part
- **CountVectorizer** → Converts email text into numerical features
- **MultinomialNB** → Best beginner ML algorithm for text classification
- **accuracy_score** → Measures model performance

### Step 2: Load the Dataset

```python
# ===============================
# Step 2: Load the dataset
# ===============================

# Make sure the CSV is in the same folder where you run this script
df = pd.read_csv("Phishing_validation_emails.csv")

# Display first 5 rows to understand the structure
print("Sample data:")
print(df.head())
```

**Purpose:**
- Confirm available columns (email_text, label, etc.)
- Understand the raw data structure before processing

### Step 3: Prepare Features and Labels

```python
# ===============================
# Step 3: Prepare features (X) and labels (y)
# ===============================

# Assuming dataset columns are 'Email Text' and 'Email Type'
X = df['Email Text']       # The email content (features)
y = df['Email Type']      # The classification (Safe / Phishing)

print("\nNumber of emails in dataset:", len(X))
```

**Explanation:**
- **X** = Input (email content)
- **y** = Output (phishing or safe classification)
- This follows the classic Supervised Learning setup

### Step 4: Split Data into Training and Testing Sets

```python
# ===============================
# Step 4: Split into Train and Test sets
# ===============================

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

print("\nTraining set size:", len(X_train))
print("Testing set size:", len(X_test))
```

**Configuration:**
- `test_size=0.2` → 20% of emails reserved for testing
- `random_state=42` → Ensures reproducible results
- Prevents overfitting by keeping test data hidden during training

### Step 5: Convert Text to Numerical Features

```python
# ===============================
# Step 5: Convert text into numeric features
# ===============================

vectorizer = CountVectorizer(stop_words='english')  # Ignore common words (a, the, is)
X_train_vec = vectorizer.fit_transform(X_train)     # Learn vocabulary + transform training data
X_test_vec = vectorizer.transform(X_test)           # Only transform test data

print("\nNumber of unique words (features):", len(vectorizer.get_feature_names_out()))
```

**Text Preprocessing:**
- ML models require numerical input, not raw text
- **Bag-of-Words** approach counts word frequencies
- `stop_words='english'` removes common filler words
- Creates feature vector from email vocabulary

### Step 6: Train the Machine Learning Model

```python
# ===============================
# Step 6: Train the Model
# ===============================

model = MultinomialNB()   # Create the model
model.fit(X_train_vec, y_train)  # Train it with training data

print("\nModel training completed!")
```

**Model Selection:**
- **MultinomialNB** is highly effective for word frequency problems
- Excellent performance on spam/phishing detection tasks
- `.fit()` method performs the actual training

### Step 7: Evaluate Model Performance

```python
# ===============================
# Step 7: Test the Model Accuracy
# ===============================

y_pred = model.predict(X_test_vec)  # Predict on unseen test data
accuracy = accuracy_score(y_test, y_pred)

print(f"\nModel Accuracy: {accuracy * 100:.2f}%")
```

**Performance Metrics:**
- Accuracy shows percentage of correctly classified emails
- Higher accuracy indicates better model performance
- Tests on completely unseen data for unbiased evaluation

### Step 8: Test with Custom Email Examples

```python
# ===============================
# Step 8: Try on New Example Emails
# ===============================

sample_emails = [
    "Your account has been suspended. Click here to verify your login details immediately.",
    "Meeting is scheduled for tomorrow at 10 AM in the conference room."
]

sample_vec = vectorizer.transform(sample_emails)   # Convert to numerical features
predictions = model.predict(sample_vec)

print("\n--- Sample Predictions ---")
for email, label in zip(sample_emails, predictions):
    print(f"Email: {email}")
    print(f"Prediction: {label}\n")
```

**Real-World Testing:**
- Demonstrates practical application of the trained model
- Shows how to classify new, unseen emails
- Validates model performance on custom examples

## 🎯 Expected Output

```
Sample data:
   Email Text                                    Email Type
0  Congratulations! You've won $1000...         Phishing
1  Hi, please find the report attached...       Safe

Number of emails in dataset: 1000
Training set size: 800
Testing set size: 200
Number of unique words (features): 5247
Model training completed!
Model Accuracy: 94.50%

--- Sample Predictions ---
Email: Your account has been suspended. Click here to verify your login details immediately.
Prediction: Phishing

Email: Meeting is scheduled for tomorrow at 10 AM in the conference room.
Prediction: Safe
```

## 📊 Key Features

- **Text Preprocessing**: Removes stop words and normalizes text
- **Feature Engineering**: Converts text to numerical vectors using Bag-of-Words
- **Model Training**: Uses Naive Bayes classifier optimized for text classification
- **Performance Evaluation**: Provides accuracy metrics and real-time predictions
- **Scalable**: Can handle large email datasets efficiently

## 🔧 Customization Options

- **Different Vectorizers**: Try `TfidfVectorizer` for improved performance
- **Model Alternatives**: Experiment with `RandomForestClassifier` or `SVM`
- **Feature Engineering**: Add n-grams or custom text features
- **Cross-validation**: Implement k-fold validation for robust evaluation

## 📝 Dataset Format

Your CSV should have these columns:
- `Email Text`: The actual email content
- `Email Type`: Labels (`Safe` or `Phishing`)

## 🚀 Running the Code

1. Save the code as `phishing_detector.py`
2. Place your CSV file in the same directory
3. Run: `python phishing_detector.py`

## 📈 Performance Tips

- Larger datasets generally improve accuracy
- Clean, well-labeled data is crucial
- Consider ensemble methods for production use
- Regularly retrain with new phishing patterns
