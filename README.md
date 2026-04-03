# NetSuite SuiteQL — Python & Jupyter Notebook Setup

A VS Code project for querying NetSuite data using SuiteQL via the REST API with Token-Based Authentication (TBA).

---

## Prerequisites

### Python
- Download from [python.org](https://www.python.org/downloads/) — Python 3.10 or newer
- During installation, check **"Add Python to PATH"**

### VS Code
- Download from [code.visualstudio.com](https://code.visualstudio.com/)

### VS Code Extensions
Install the following from the Extensions panel (`Ctrl+Shift+X`):

| Extension | Publisher | Purpose |
|---|---|---|
| **Python** | Microsoft | Python language support |
| **Jupyter** | Microsoft | Run `.ipynb` notebooks |
| **Pylance** | Microsoft | IntelliSense & type checking |

---

## Project Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/netsuite-suiteql.git
cd netsuite-suiteql
code .
```

### 2. Create a Virtual Environment

In the VS Code terminal (`Ctrl+``):

```bash
python -m venv .venv
```

#### Activate the Virtual Environment

**Windows PowerShell:**
```powershell
.venv\Scripts\activate
```

**Windows Command Prompt:**
```cmd
.venv\Scripts\activate.bat
```

**Mac/Linux:**
```bash
source .venv/bin/activate
```

> You should see `(.venv)` appear in your terminal prompt when activated.

---

### Windows PowerShell — Execution Policy Error

If you see this error on Windows when trying to activate:

```
.venv\Scripts\Activate.ps1 cannot be loaded. The file is not digitally signed.
```

Run this once to fix it for your user account:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then activate normally. This allows locally created scripts to run while still requiring downloaded scripts to be signed. It only affects your user account.

**Alternative — one-time bypass for the current terminal session only:**
```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
.venv\Scripts\activate
```

---

### 3. Install Required Packages

```bash
pip install -r requirements.txt
```

| Package | Purpose |
|---|---|
| `requests` | Make HTTP calls to the NetSuite REST API |
| `requests-oauthlib` | Handle OAuth 1.0a authentication |
| `ipykernel` | Connect your virtual environment to Jupyter |
| `python-dotenv` | Load credentials securely from a `.env` file |
| `pandas` | Load query results into a DataFrame |

---

## NetSuite Configuration

### Enable Token-Based Authentication in NetSuite

1. Go to **Setup → Company → Enable Features**
2. Click the **SuiteCloud** tab
3. Check **Token-Based Authentication**
4. Save

### Create an Integration Record

1. Go to **Setup → Integration → Manage Integrations → New**
2. Give it a name (e.g., `SuiteQL Python`)
3. Check **Token-Based Authentication**
4. Save and copy the **Consumer Key** and **Consumer Secret**

### Create an Access Token

1. Go to **Setup → Users/Roles → Access Tokens → New**
2. Select your Integration and User
3. Save and copy the **Token ID** and **Token Secret**

---

## Credentials Setup

### Create a `.env` File

Create a file named `.env` in the project root and add your credentials:

```env
NS_ACCOUNT_ID=your_account_id
NS_CONSUMER_KEY=your_consumer_key
NS_CONSUMER_SECRET=your_consumer_secret
NS_TOKEN_ID=your_token_id
NS_TOKEN_SECRET=your_token_secret
```

> **Account ID format:** Use `1234567` for production or `1234567_SB1` for sandbox environments.

> ⚠️ **Never commit your `.env` file to source control.**

---

## Open the Jupyter Notebook

`netsuite_query.ipynb` is already included in this repo with starter code ready to run.

1. Open `netsuite_query.ipynb` in VS Code
2. In the top-right corner of the notebook, click **Select Kernel** → choose **Python Environments...** → select **.venv**

---

## Project Structure

```
netsuite-suiteql/
├── .env                    ← credentials (never commit!)
├── .gitignore
├── README.md
├── requirements.txt        ← package dependencies
├── netsuite_query.ipynb    ← your Jupyter notebook
└── .venv/                  ← virtual environment
```

---

## .gitignore

A `.gitignore` is already included in this repo covering the following:

```
.env
.venv/
__pycache__/
*.pyc
.ipynb_checkpoints/
```
