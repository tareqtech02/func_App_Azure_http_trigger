# Azure Function App — HTTP Trigger (.NET 8)

A basic Azure Function App using .NET 8 with an HTTP trigger, deployed to Azure.

---

## 📋 Prerequisites

Make sure you have all the required tools installed before starting.

### Required Tools

| Tool | Version |
|------|---------|
| .NET 8 SDK + Runtime | 8.x |
| Azure Functions Core Tools | 4.x |
| Azure CLI | Latest |

### Verify Installation

```bash
dotnet --version
dotnet --list-runtimes
func --version
az --version
```

---

## 🚀 Run Locally

```bash
cd ~
git clone XXXXXXXXXXXXXXXXXXXXXXXXXX
cd ~/my-func-app
func start
```

You should see:
```
HttpExample: [GET,POST] http://localhost:7071/api/HttpExample
```

Test it:
```bash
curl http://localhost:7071/api/HttpExample
```

---

## ☁️ Deploy to Azure

### Step 1 — Create Resource Group

```bash
az group create \
  --name rg-my-func-app \
  --location southeastasia
```

### Step 2 — Create Storage Account

```bash
az storage account create \
  --name stmyfuncapp$RANDOM \
  --resource-group rg-my-func-app \
  --location southeastasia \
  --sku Standard_LRS
```

### Step 3 — Create the Function App

```bash
az functionapp create \
  --resource-group rg-my-func-app \
  --consumption-plan-location southeastasia \
  --runtime dotnet-isolated \
  --runtime-version 8 \
  --functions-version 4 \
  --name my-func-app-tareq \
  --storage-account stmyfuncappXXXXXX
```

### Step 4 — Publish Your Code

```bash
cd ~/my-func-app
func azure functionapp publish my-func-app-tareq
```

---

## 🌐 Live URL

```
https://my-func-app-tareq.azurewebsites.net/api/HttpExample
```

Test the live function:
```bash
curl https://my-func-app-tareq.azurewebsites.net/api/HttpExample
```

Expected response:
```
Welcome to Azure Functions!
```

---

## 📁 Project Structure

```
my-func-app/
├── HttpExample.cs        # HTTP trigger function
├── Program.cs            # App entry point
├── host.json             # Global function settings
├── local.settings.json   # Local environment variables
└── my-func-app.csproj    # .NET project file
```
