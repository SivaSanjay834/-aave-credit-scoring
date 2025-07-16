# 📊 Wallet Credit Score Analysis

## Score Distribution

The histogram below shows how wallets are distributed across score ranges (0 to 1000):

![score-distribution](score_distribution.png)

---

## 🔍 Observations

### 🔴 Low-score Wallets (0–200)
- Typically have very few transactions
- Often borrowed but **never repaid**
- Higher number of `liquidationcall` events
- Suggests high-risk or bot-like behavior

### 🟢 High-score Wallets (800–1000)
- Made frequent `repay` and `deposit` actions
- Long wallet activity span
- No liquidations
- Responsible borrowing behavior

---

## ✅ Takeaways

- Rule-based scoring effectively highlights bad actors
- ML predictions align well with clustering patterns
- This model can be extended with real-time scoring on live DeFi wallets
