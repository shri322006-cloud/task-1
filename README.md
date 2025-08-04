# task-1

import pandas as pd
import os

# Set path to the downloaded CSV
data_path = os.path.join(path, "KaggleV2-May-2016.csv")

# Load the dataset
df = pd.read_csv(data_path)

# 1. View initial info
print("Initial dataset info:")
print(df.info())

# 2. Rename columns to lowercase and snake_case
df.columns = df.columns.str.strip().str.lower().str.replace("-", "_").str.replace(" ", "_")

# 3. Remove duplicates
df = df.drop_duplicates()

# 4. Handle missing values
print("Missing values:\n", df.isnull().sum())

# 5. Standardize gender column
df['gender'] = df['gender'].str.upper().str.strip()

# 6. Convert date columns to datetime
df['scheduledday'] = pd.to_datetime(df['scheduledday'])
df['appointmentday'] = pd.to_datetime(df['appointmentday'])

# 7. Remove negative ages and unrealistic entries
df = df[df['age'] >= 0]

# 8. Save cleaned dataset
cleaned_path = os.path.join(path, "medical_appointments_cleaned.csv")
df.to_csv(cleaned_path, index=False)
#Renamed columns to lowercase with underscores

Removed duplicate rows

Removed negative ages

Standardized gender column

Converted scheduledday and appointmentday to datetime

Checked for and retained rows without missing values


print(f"✅ Cleaned dataset saved to: {cleaned_path}")

