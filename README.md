#  Wallet Risk Scoring – Zeru Assignment (Round 2)

This project aims to assess the on-chain creditworthiness of Ethereum wallets by analyzing their activity in the Compound V2 protocol, using unsupervised learning techniques. Each wallet is assigned a risk score between 0 and 1000, where a higher score indicates lower risk.

---

##  Problem Statement

Given 100 Ethereum wallet addresses, our objective is to:

1. Fetch each wallet's transaction history using Compound V2/V3.
2. Engineer meaningful features from lending protocol activity.
3. Cluster similar wallets using machine learning.
4. Assign a risk score (0–1000) based on behavioral patterns.

---

##  Data Collection

- Source: [Compound V2 Protocol](https://compound.finance/)
- API Tool: [GoldRush by Zeru]
- Tracked activities:
  - `deposit`
  - `borrow`
  - `repay`
  - `redeem`
  - `liquidation`

Each wallet's transaction history was aggregated across these key actions.

---

##  Feature Engineering

Engineered features capturing wallet behavior include:

| Feature Name               | Description                                 |
|---------------------------|---------------------------------------------|
| total_deposits            | Total amount deposited into protocol        |
| total_borrows             | Total amount borrowed from protocol         |
| total_repaid              | Total repaid amount                         |
| total_liquidations        | Count of times wallet was liquidated        |
| borrow_to_deposit_ratio   | Ratio of borrowed to deposited assets       |
| repayment_ratio           | Ratio of repaid to borrowed funds           |
| avg_borrow_duration       | Average time between borrow and repay       |

Features were scaled using `StandardScaler` before clustering.

---

##  Risk Scoring Methodology

- Clustering Algorithm: `KMeans`
- Optimal Clusters: 4 (based on silhouette score)
- Silhouette Score: `0.446`

## Cluster to Risk Score Mapping

| Cluster | Risk Category     | Score |
|---------|-------------------|-------|
| 1       | Low Risk          | 900   |
| 2       | Medium–Low Risk   | 800   |
| 0       | Medium–High Risk  | 700   |
| 3       | High Risk         | 400   |

Each wallet is assigned a risk score based on its cluster.

---

##  Output

Final output file: `wallet_scores.csv`

| wallet_id                                 | score |
|-------------------------------------------|-------|
| 0xfaa0768bde629806739c3a4620656c5d26f44ef2| 732   |
| ...                                       | ...   |

---

##  Why This Works

- Unsupervised Learning allows us to discover natural wallet behavior clusters without labels.
- Risk indicators such as liquidation frequency, repayment habits, and borrowing patterns are strong predictors of creditworthiness.

---

##  Folder Structure

wallet-risk-scoring/
├── data/
│ └── wallets.csv
├── notebooks/
│ └── risk_scoring.ipynb
├── outputs/
│ └── wallet_scores.csv
├── README.md
└── requirements.txt

---

##  Tech Stack

- Language: Python
- Libraries: `pandas`, `numpy`, `sklearn`, `matplotlib`, `seaborn`
- Notebook: Google Colab

---

## Author

Sanjay Chaudhary  
MSc Statistics – Delhi University  
GitHub: [github.com/YourUsername](https://github.com/sanjaystats7057)  
Email: chaudharysanjay2001@gmail.com

---
##  Use Case

This project was built as a practical assignment to simulate real-world DeFi wallet risk scoring.


##  Notes

- DBSCAN was also tested (Silhouette Score: 0.467), but KMeans provided more interpretable clusters.
- Feature choices were inspired by lending protocol risks observed in real-world DeFi lending datasets.



















