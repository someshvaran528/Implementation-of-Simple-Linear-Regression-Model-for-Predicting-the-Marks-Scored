# Implementation-of-Simple-Linear-Regression-Model-for-Predicting-the-Marks-Scored

## AIM:
To write a program to predict the marks scored by a student using the simple linear regression model.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
1. Load the dataset into a DataFrame and explore its contents to understand the data structure.
2.Separate the dataset into independent (X) and dependent (Y) variables, and split them into training and testing sets.
3.Create a linear regression model and fit it using the training data.
4.Predict the results for the testing set and plot the training and testing sets with fitted lines.
5.Calculate error metrics (MSE, MAE, RMSE) to evaluate the model’s performance.
## Program:
```
/*
Program to implement the simple linear regression model for predicting the marks scored.
Developed by: M.Someshvaran
RegisterNumber: 212225230270

# Implementation of Simple Linear Regression Model
# for Predicting Student Marks

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from pathlib import Path

from sklearn.metrics import mean_absolute_error, mean_squared_error
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# 1. Load the dataset
file_name = "exp_2_dataset_student_scores.csv"

# Check the current folder and Downloads folder
possible_paths = [
    Path(file_name),
    Path.home() / "Downloads" / file_name,
    Path.home() / "Desktop" / file_name
]

file_path = next((p for p in possible_paths if p.is_file()), None)

if file_path is None:
    print("ERROR: CSV file not found!")
    print("Please save the file in your current folder or Downloads folder.")
    print("Current working folder:", Path.cwd())
else:
    # Read the CSV file
    df = pd.read_csv(file_path)

    # Remove extra spaces from column names
    df.columns = df.columns.str.strip()

    print("First 5 rows:\n", df.head())
    print("\nLast 5 rows:\n", df.tail())

    # 2. Prepare input (X) and output (Y)
    if df.shape[1] < 2:
        raise ValueError("The CSV file must contain at least two columns.")

    # Use the first column as input and last column as target
    X = df.iloc[:, 0].to_numpy().reshape(-1, 1)
    Y = df.iloc[:, -1].to_numpy()

    # Convert values to numeric
    X = pd.to_numeric(pd.Series(X.flatten()), errors="coerce").to_numpy()
    Y = pd.to_numeric(pd.Series(Y), errors="coerce").to_numpy()

    # Remove rows containing missing or invalid values
    valid_rows = np.isfinite(X) & np.isfinite(Y)
    X = X[valid_rows].reshape(-1, 1)
    Y = Y[valid_rows]

    if len(X) < 3:
        raise ValueError("At least 3 valid numeric rows are required.")

    print("\nInput values (X):", X.flatten())
    print("Target values (Y):", Y)

    # 3. Split data into training and testing sets
    X_train, X_test, Y_train, Y_test = train_test_split(
        X, Y, test_size=1/3, random_state=0
    )

    print("\nTraining samples:", len(X_train))
    print("Testing samples:", len(X_test))

    # 4. Create and train the model
    regressor = LinearRegression()
    regressor.fit(X_train, Y_train)

    print("\nSlope:", regressor.coef_[0])
    print("Intercept:", regressor.intercept_)

    # 5. Predict test results
    Y_pred = regressor.predict(X_test)

    print("\nPredicted values:", np.round(Y_pred, 2))
    print("Actual values:", Y_test)

    # 6. Plot training results
    train_order = np.argsort(X_train.flatten())

    plt.figure(figsize=(7, 4))
    plt.scatter(X_train, Y_train, color="orange", label="Training data")
    plt.plot(
        X_train.flatten()[train_order],
        regressor.predict(X_train)[train_order],
        color="red",
        label="Regression line"
    )
    plt.title("Hours vs Scores (Training Set)")
    plt.xlabel(df.columns[0])
    plt.ylabel(df.columns[-1])
    plt.legend()
    plt.grid(True)
    plt.tight_layout()
    plt.show()

    # 7. Plot testing results
    test_order = np.argsort(X_test.flatten())
    X_test_sorted = X_test.flatten()[test_order]

    plt.figure(figsize=(7, 4))
    plt.scatter(X_test.flatten(), Y_test, color="blue", label="Actual scores")
    plt.plot(
        X_test_sorted,
        regressor.predict(X_test[test_order]),
        color="green",
        marker="o",
        label="Predicted scores"
    )
    plt.title("Hours vs Scores (Testing Set)")
    plt.xlabel(df.columns[0])
    plt.ylabel(df.columns[-1])
    plt.legend()
    plt.grid(True)
    plt.tight_layout()
    plt.show()

    # 8. Evaluate the model
    mae = mean_absolute_error(Y_test, Y_pred)
    mse = mean_squared_error(Y_test, Y_pred)
    rmse = np.sqrt(mse)

    print("\nMean Absolute Error (MAE):", round(mae, 2))
    print("Mean Squared Error (MSE):", round(mse, 2))
    print("Root Mean Squared Error (RMSE):", round(rmse, 2))

    # 9. Predict marks for new students
    new_hours = np.array([[2.5], [8.0]])
    pred_new = regressor.predict(new_hours)

    print("\nPredictions for new input values:")
    for hours, marks in zip(new_hours.flatten(), pred_new):
        print(f"{hours} hours -> Predicted marks: {marks:.2f}")

*/
```

## Output:
<img width="1042" height="642" alt="Screenshot 2026-10-28 090025" src="https://github.com/user-attachments/assets/d2195026-235d-47d6-b2fc-f505e10a4b7d" />
<img width="1078" height="492" alt="Screenshot 2026-10-28 090034" src="https://github.com/user-attachments/assets/fd6aee83-40ab-47bf-9a5c-34544fd451b5" />
<img width="1005" height="676" alt="Screenshot 2026-10-28 090040" src="https://github.com/user-attachments/assets/f1370873-e3d0-4555-8684-6edd05728ad0" />






## Result:
Thus the program to implement the simple linear regression model for predicting the marks scored is written and verified using python programming.
