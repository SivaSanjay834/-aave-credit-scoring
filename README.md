# 🧠 Aave V2 Wallet Credit Scoring

This project builds a robust credit scoring system for wallets interacting with the Aave V2 protocol. Given a set of raw user transactions, the goal is to assign a **credit score between 0 and 1000** to each wallet, based solely on its historical transaction behavior.

---

## 🚀 Objective

- Analyze transaction-level data from the Aave V2 protocol
- Engineer wallet-level behavioral features
- Use both rule-based logic and machine learning models to generate scores
- Visualize and explain wallet behavior patterns

---

## 📂 Input

**File:** `user-wallet-transactions.json`  
Each record includes:
- `userWallet`: Wallet address
- `action`: Type of transaction (`deposit`, `borrow`, `repay`, etc.)
- `actionData`: Amount, token symbol, token price
- `timestamp`: When the action occurred

---

## 🧮 Feature Engineering

For each wallet, the following features were extracted:
- Total deposit and repay value in USD
- Count of `deposit`, `borrow`, `repay`, `redeemunderlying`, `liquidationcall`
- First and last transaction timestamps
- Number of active days
- Number of total transactions

Amounts were converted into USD using token decimals and asset price.

---

## 📊 Credit Score (Rule-Based)

A rule-based credit scoring system assigns scores as follows:

- Base score: **500**
- + Up to 100 for total deposits
- + Up to 100 for total repayments
- + Up to 50 for repay frequency
- + Up to 100 for wallet activity span
- − 100 if borrowed but never repaid
- − 20 per liquidation
- − 50 for very low activity (≤2 txs)

---

## 📈 Unsupervised Clustering with KMeans

To analyze wallet behavior patterns:

- KMeans was applied to scaled wallet features.
- Wallets were grouped into 5 clusters.
- Each cluster was assigned a credit score based on behavior.

---

## 🤖 ML-Based Scoring (Random Forest)

A **Random Forest Regressor** was trained using:
- Input: Behavioral features
- Target: Credit score (from KMeans or rule-based)

The trained model predicts a `ml_credit_score` for each wallet.

---

## 📁 Output

**wallet_scores.csv** – contains:
- `wallet`
- `credit_score` (rule-based or KMeans)
- `ml_credit_score` (from Random Forest)

---

## 🛠️ How to Run

1. Place `user-wallet-transactions.json` in your project folder
2. Run the script:  
   ```bash
   python score_wallets.py
---

## 📌 Dependencies

- Python 3.8+
- pandas
- scikit-learn
- matplotlib
- seaborn

---

## 👨‍💻 Author

**SivaSanjay Uppalapati**  
Credit Scoring Challenge — Aave V2 (July 2025)
