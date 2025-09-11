# ===============================
# Step 1: Import required libraries
# ===============================

import pandas as pd                           # For handling CSV dataset
from sklearn.model_selection import train_test_split  # To split data into training/testing
from sklearn.feature_extraction.text import CountVectorizer  # Convert text to numbers
from sklearn.naive_bayes import MultinomialNB  # Simple ML model for text classification
from sklearn.metrics import accuracy_score     # To measure model performance

Why these?

pandas → read and organize dataset.
train_test_split → so our model learns on part of data, tests on unseen part.
CountVectorizer → turns email text into numbers.
MultinomialNB → best first ML algorithm for text classification.
accuracy_score → to check how good the model is.


# ===============================
# Step 2: Load the dataset
# ===============================

# Make sure the CSV is in the same folder where you run this script
df = pd.read_csv("Phishing_validation_emails.csv")

# Display first 5 rows to understand the structure
print("Sample data:")
print(df.head())

Why?

We need to confirm what columns are available (email_text, label, etc.).
Helps you understand the raw data before using it.


# ===============================
# Step 3: Prepare features (X) and labels (y)
# ===============================

# Assuming dataset columns are 'text' and 'label' (adjust if different)
X = df['Email Text']       # The email content (features)
y = df['Email Type']      # The classification (Safe / Phishing)

print("\nNumber of emails in dataset:", len(X))

Why?

X = input (emails).
y = output (is it phishing or safe?).
This is the classic Supervised Learning setup


# ===============================
# Step 4: Split into Train and Test sets
# ===============================

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

print("\nTraining set size:", len(X_train))
print("Testing set size:", len(X_test))

Why?

We don’t train on all data → keeps part of data hidden for testing accuracy.
test_size=0.2 → 20% of emails are for testing.
random_state=42 → ensures reproducibility (same split every run).


# ===============================
# Step 5: Convert text into numeric features
# ===============================

vectorizer = CountVectorizer(stop_words='english')  # ignore common words (a, the, is)
X_train_vec = vectorizer.fit_transform(X_train)     # Learn vocab + transform training data
X_test_vec = vectorizer.transform(X_test)           # Only transform test data

print("\nNumber of unique words (features):", len(vectorizer.get_feature_names_out()))

Why?

ML models only work on numbers, not raw text.
Bag-of-Words (CountVectorizer) → counts how many times each word appears.
stop_words='english' removes filler words like and, the, is.


# ===============================
# Step 6: Train the Model
# ===============================

model = MultinomialNB()   # Create the model
model.fit(X_train_vec, y_train)  # Train it with training data

print("\nModel training completed!")

Why?

MultinomialNB is very effective for word frequency problems like spam/phishing detection.
.fit() = training step.


# ===============================
# Step 7: Test the Model Accuracy
# ===============================

y_pred = model.predict(X_test_vec)  # Predict on unseen test data
accuracy = accuracy_score(y_test, y_pred)

print("\nModel Accuracy:", accuracy * 100, "%")

Why?

Accuracy tells us what % of emails were correctly classified.
Higher accuracy = better model.


# ===============================
# Step 8: Try on New Example Emails
# ===============================

sample_emails = [
    "Your account has been suspended. Click here to verify your login details immediately.",
    "Meeting is scheduled for tomorrow at 10 AM in the conference room."
]

sample_vec = vectorizer.transform(sample_emails)   # Convert to numbers
predictions = model.predict(sample_vec)

print("\n--- Sample Predictions ---")
for email, label in zip(sample_emails, predictions):
    print(f"Email: {email}\nPrediction: {label}\n")

Why?

This is the “real test” → you feed your own text, see if model detects phishing vs safe.
Makes your project feel practical.
