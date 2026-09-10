# AI-Prompts-and-Scripts
Real-time crypto risk auditing, liquidity tracking, and trade execution scripts using CCXT and the Kraken API, alongside AI automation workflows.

🚀 Crypto Risk Audit & Execution Bot (24_audit.py)

A dynamic Python command-line utility built on top of CCXT to perform real-time crypto market risk audits, liquidity checks, wallet balance tracking, and dynamic position sizing with optional live order execution on Kraken.

📌 Features

Live Market Analysis: Fetches real-time price feeds, 24h trading volume, and top-10 bid/ask order book depth.

Smart Account Tracking: Displays active crypto balance alongside available USD cash reserves.

Dynamic Position Sizing: Automatically calculates purchase quantities based on a risk-adjusted percentage of available USD cash.

Microsecond Nonce Handling: Native handling for Kraken API microsecond nonce constraints (time.time() * 1000000) and automatic transient retry logic.

Dual Execution Modes:

Simulation (Default): Runs paper audits and generates limit, stop-loss, and take-profit parameters safely without placing real trades.

Live Execution (--live): Submits actual limit buy orders to Kraken with attached stop-loss and take-profit parameters.

⚙️ Prerequisites & Setup

1. Requirements
Python 3.8+

Active Kraken API Key & Secret (with trading and query permissions enabled)

2. Installation
Clone the repository and install the required dependencies:

Bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY

pip install ccxt python-dotenv
3. Environment Configuration
Create a .env file in the root directory of the project:

Bash
touch .env
Add your API credentials to the .env file using the template below:

Code snippet
# Kraken API Credentials
KRAKEN_API_KEY=ENTER_API_KEY_HERE
KRAKEN_API_SECRET=ENTER_API_SECRET_HERE

⚠️ Security Notice: Never commit your .env file or actual API keys to GitHub. Ensure .env is listed inside your .gitignore file.

🛠️ Usage Guide

1. Simulation Mode (Default & Safe)
Runs market analysis, pulls account balance, and calculates position sizing without placing real trades:

Bash
# Default asset (NEAR) on Kraken
./24_audit.py

# Specify a custom ticker
./24_audit.py BTC

# Specify custom ticker and exchange
./24_audit.py ETH kraken
2. Live Order Execution Mode
To execute real limit buy orders on Kraken based on your USD risk sizing, append the --live flag:

Bash
# Execute live order for NEAR
./24_audit.py NEAR kraken --live

# Execute live order for BTC
./24_audit.py BTC kraken --live

📊 Sample Terminal Output

Plaintext
=================== 24-HOUR RISK AUDIT ===================
Target Ticker : NEAR
Exchange      : Kraken
Active Pair   : NEAR/USD
Mode          : [SIMULATION]
==========================================================

+---------------------+-----------------------------------+
| Market Metric       | Value                             |
+---------------------+-----------------------------------+
| Live Price (USD)    | $2.5148                           |
| 24h Volume          | 3,664,753.53                      |
| Bid Depth (Top 10)  | 10,015.28                         |
| Ask Depth (Top 10)  | 10,298.73                         |
| Whale Dump Risk     | LOW                               |
+---------------------+-----------------------------------+

+---------------------+-----------------------------------+
| Account & Sizing    | Value                             |
+---------------------+-----------------------------------+
| Available NEAR      | 76.5360                           |
| Crypto Value ($)    | $192.47                           |
| USD Cash Available  | $500.00                           |
| Risk Sizing (20%)   | $100.00                           |
| Target Buy Quantity | 39.7646                           |
+---------------------+-----------------------------------+

+---------------------+-----------------------------------+
| Execution Parameter | Value                             |
+---------------------+-----------------------------------+
| Action              | BUY                               |
| Execution Mode      | SIMULATION                        |
| Limit Order Price   | $2.5148                           |
| Calculated Quantity | 39.7646                           |
| Stop Loss (-15%)    | $2.1376                           |
| Take Profit (+100%) | $5.0296                           |
+---------------------+-----------------------------------+

🔒 Security Best Practices

API Key Permissions: Only grant Query Funds and Create/Modify Orders permissions on Kraken. Do NOT enable withdrawal permissions.

Git Ignore: Ensure your .gitignore contains the following:

Code snippet
.env
__pycache__/
*.pyc
