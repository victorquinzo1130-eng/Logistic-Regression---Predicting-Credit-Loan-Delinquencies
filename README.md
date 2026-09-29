# Logistic-Regression---Predicting-Credit-Loan-Delinquencies
Logistic Regression to predict future delinquencies for hypothetical bank
# Build future outcome
df = may[may["DPD"] == 0].merge(
    june[["Account_ID", "DPD"]],
    on="Account_ID", how="left",
    suffixes=("_May", "_June"))
df["Y"] = (df["DPD_June"] > 0).astype(int)

# Fit and validate
features = ["FICO", "Exposure", "Rate"]
X_train, X_test, y_train, y_test = train_test_split(
    df[features], df["Y"], stratify=df["Y"], random_state=14)
scaler.fit(X_train)
model.fit(scaler.transform(X_train), y_train)

# Score current accounts
june_current["July_PD"] = model.predict_proba(
    scaler.transform(june_current[features]))[:, 1]
<img width="579" height="390" alt="image" src="https://github.com/user-attachments/assets/2fba275a-a21a-4c4b-8a93-cf32d0be6158" />
