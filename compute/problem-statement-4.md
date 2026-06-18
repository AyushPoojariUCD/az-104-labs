# Lab 4 – Serverless Order Processing using Azure Functions

## Objective

Build a **serverless order processing system** that automatically processes files uploaded to Azure Blob Storage.

When an order file is uploaded:

1. Azure Function is triggered automatically.
2. The file is processed.
3. The processed result is stored in another Blob Storage container.
4. No servers are managed.
5. Billing occurs only when the function executes.

---

# Company

**ShopKart**

---

# Background

ShopKart receives customer order files throughout the day. Whenever a new order file is uploaded to Azure Blob Storage, the company wants it to be processed automatically without running any virtual machines or servers continuously.

---

# Requirements

- Trigger execution whenever a file is uploaded.
- Store processed results in another storage container.
- No servers should run continuously.
- Pay only for execution time.

---

# Azure Services Used

| Azure Service | Purpose |
|--------------|---------|
| Resource Group | Organize resources |
| Storage Account | Store input and output files |
| Blob Containers | Store uploaded and processed files |
| Azure Function | Process uploaded files |
| Function App | Host the Azure Function |
| Consumption Plan | Pay only when function runs |
| Application Insights | Monitor execution |

---

# Solution Architecture

```
Customer Uploads Order File
            │
            ▼
Input Blob Container
            │
     Blob Trigger
            │
            ▼
Azure Function
(Process Order)
            │
            ▼
Processed Blob Container
```

---

# Azure Resources Required

| Resource | Name |
|----------|------|
| Resource Group | rg-shopkart |
| Storage Account | shopkartstorage |
| Blob Container | orders |
| Blob Container | processed-orders |
| Function App | shopkart-orderprocessor |
| Hosting Plan | Consumption (Serverless) |

---

# Hands-on Solution

## Step 1 – Create a Resource Group

1. Open **Azure Portal**.
2. Search **Resource Groups**.
3. Click **Create**.

Configuration

| Setting | Value |
|----------|-------|
| Resource Group | rg-shopkart |
| Region | East US |

Click **Create**.

---

## Step 2 – Create a Storage Account

Navigate to

```
Storage Accounts
→ Create
```

Configuration

| Setting | Value |
|----------|-------|
| Resource Group | rg-shopkart |
| Storage Account | shopkartstorage |
| Region | East US |
| Performance | Standard |
| Redundancy | LRS |

Click **Review + Create**.

---

## Step 3 – Create Blob Containers

Open the Storage Account.

Go to

```
Data Storage
→ Containers
```

Create two containers.

### Container 1

```
orders
```

This stores uploaded order files.

---

### Container 2

```
processed-orders
```

This stores processed output files.

---

## Step 4 – Create a Function App

Search

```
Function App
```

Click

```
Create
```

Configuration

| Setting | Value |
|----------|-------|
| Resource Group | rg-shopkart |
| Function App Name | shopkart-orderprocessor |
| Runtime Stack | .NET 8 (or Python/Node.js) |
| Region | East US |
| Hosting Plan | Consumption |

Click **Create**.

---

## Step 5 – Create a Blob Trigger Function

Open the Function App.

Navigate to

```
Functions
→ Create
```

Choose

```
Blob Trigger
```

Configuration

| Setting | Value |
|----------|-------|
| Trigger | Blob Trigger |
| Storage Account | shopkartstorage |
| Container | orders |

Finish creating the function.

---

## Step 6 – Sample Function Code (C#)

```csharp
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;

public class OrderProcessor
{
    private readonly ILogger _logger;

    public OrderProcessor(ILoggerFactory loggerFactory)
    {
        _logger = loggerFactory.CreateLogger<OrderProcessor>();
    }

    [Function("OrderProcessor")]
    public void Run(
        [BlobTrigger("orders/{name}", Connection = "AzureWebJobsStorage")] string inputBlob,
        string name)
    {
        _logger.LogInformation($"Processing Order File: {name}");

        // Process the file
        var processed = inputBlob.ToUpper();

        // Output can be written to processed-orders container
    }
}
```

---

## Step 7 – Configure Output Binding

Add an output binding.

```
Blob Output
```

Container

```
processed-orders
```

Whenever the function completes, the processed file is automatically saved into the output container.

---

## Step 8 – Deploy the Function

Deployment options include:

- Visual Studio
- Visual Studio Code
- Azure CLI
- GitHub Actions

Deploy the Azure Function to the Function App.

---

## Step 9 – Test the Solution

Upload a sample file.

Example

```
order1.txt
```

Contents

```
Order ID: 1001

Customer: John

Amount: 500
```

Upload it into

```
orders
```

---

## Step 10 – Verify Trigger Execution

Navigate to

```
Function App
→ Monitor
```

You should see

```
Execution Successful
```

---

## Step 11 – Verify Output

Open

```
processed-orders
```

You should see

```
order1.txt
```

The processed file has been created automatically.

---

# Why This Is Serverless

Azure Functions on the **Consumption Plan** provide:

- No virtual machines to manage.
- Automatic scaling.
- Automatic trigger execution.
- Billing only while code runs.
- Zero cost when idle.

---

# Expected Outcome

When a customer uploads a file:

```
Upload File
      │
      ▼
orders Container
      │
Blob Trigger
      │
      ▼
Azure Function Executes
      │
Processes File
      │
      ▼
processed-orders Container
```

---

# Verification Checklist

| Requirement | Status |
|-------------|--------|
| Storage Account Created | ✅ |
| Orders Container Created | ✅ |
| Processed Container Created | ✅ |
| Function App Created | ✅ |
| Blob Trigger Configured | ✅ |
| Output Binding Configured | ✅ |
| Sample File Uploaded | ✅ |
| Function Executed Successfully | ✅ |
| Processed File Generated | ✅ |

---

# Learning Outcomes

After completing this lab, you will be able to:

- Create an Azure Function App.
- Configure a Blob Storage trigger.
- Build serverless event-driven applications.
- Automatically process uploaded files.
- Store processed data in another Blob container.
- Understand the Consumption Plan billing model.
- Implement a serverless architecture using Azure Functions.