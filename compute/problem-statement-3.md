# Lab 3 – Deploy a Scalable Web Application using Azure App Service

## Objective

Deploy an ASP.NET Core web application to Azure with:

- Azure App Service
- Custom Domain
- HTTPS Enabled
- Auto Scaling (CPU > 70%)
- GitHub Continuous Deployment
- High Availability without managing virtual machines

---

# Company

**FoodExpress Pvt. Ltd.**

---

# Background

FoodExpress has developed an **ASP.NET Core Web Application** that serves approximately **50,000 users daily**.

The company wants a highly available, scalable, and fully managed hosting solution in Azure.

---

# Requirements

- Deploy ASP.NET Core application in Azure
- Configure a Custom Domain
- Enable HTTPS
- Automatically scale when CPU exceeds 70%
- Configure deployment from GitHub
- Ensure High Availability without managing operating systems

---

# Azure Services Used

| Service | Purpose |
|----------|----------|
| Resource Group | Organize Azure resources |
| Azure App Service Plan | Compute resources |
| Azure App Service | Host ASP.NET Core application |
| Azure Monitor | CPU Monitoring |
| Autoscale | Automatic scaling |
| GitHub Deployment Center | CI/CD |
| Azure DNS / External DNS | Custom Domain |
| Managed Certificate | HTTPS |

---

# Architecture

```
GitHub Repository
        │
        ▼
Deployment Center (GitHub Actions)
        │
        ▼
Azure App Service
        │
        ▼
Custom Domain
        │
        ▼
HTTPS
        │
        ▼
Users
```

---

# Task 1 – Create Resource Group

Navigate to

```
Azure Portal
→ Resource Groups
→ Create
```

Configuration

| Setting | Value |
|----------|-------|
| Resource Group | rg-foodexpress |
| Region | East US |

Click **Create**

---

# Task 2 – Create App Service Plan

Navigate to

```
App Services
→ Create
```

Configuration

| Setting | Value |
|----------|-------|
| Name | foodexpress-plan |
| Publish | Code |
| Runtime Stack | .NET 8 (LTS) |
| Operating System | Windows or Linux |
| Region | East US |
| Pricing Tier | Premium V3 (Supports Autoscaling) |

Click **Review + Create**

---

# Task 3 – Create Azure App Service

Configuration

| Setting | Value |
|----------|-------|
| App Name | foodexpress-web |
| Runtime | ASP.NET Core (.NET 8) |
| Region | East US |
| App Service Plan | foodexpress-plan |

Create the web app.

---

# Task 4 – Deploy Application from GitHub

Navigate to

```
App Service
→ Deployment Center
```

Choose

```
Source:
GitHub
```

Authorize GitHub.

Select

- Repository
- Branch

Azure automatically creates a **GitHub Actions** workflow.

Every push to GitHub automatically deploys the application.

---

# Task 5 – Configure Custom Domain

Navigate to

```
App Service
→ Custom Domains
→ Add Custom Domain
```

Example

```
www.foodexpress.com
```

Create the required DNS record.

Example

```
CNAME

www
↓

foodexpress-web.azurewebsites.net
```

Validate ownership.

Add the domain.

---

# Task 6 – Enable HTTPS

Navigate to

```
App Service
→ TLS/SSL Settings
```

Choose

```
Create App Service Managed Certificate
```

Bind the certificate to

```
www.foodexpress.com
```

Enable

```
HTTPS Only = On
```

Now all HTTP traffic redirects to HTTPS.

---

# Task 7 – Configure Autoscaling

Navigate to

```
App Service Plan
→ Scale Out (App Service Plan)
```

Choose

```
Custom Autoscale
```

Configuration

| Setting | Value |
|----------|-------|
| Minimum Instances | 2 |
| Maximum Instances | 10 |
| Default Instances | 2 |

Create Rule

### Scale Out

Condition

```
CPU Percentage > 70%
Duration: 10 minutes
```

Action

```
Increase instance count by 1
```

---

Create another rule

### Scale In

Condition

```
CPU Percentage < 30%
Duration: 10 minutes
```

Action

```
Decrease instance count by 1
```

Save.

---

# Task 8 – Verify High Availability

Since Azure App Service is a **Platform as a Service (PaaS)** offering:

- No Virtual Machines to manage
- Automatic OS patching
- Built-in load balancing
- Automatic health monitoring
- SLA up to 99.95%

No operating system maintenance is required.

---

# Task 9 – Verify Deployment

Open

```
https://foodexpress-web.azurewebsites.net
```

Verify

- Application loads successfully
- HTTPS enabled
- Custom domain works
- GitHub deployment succeeds

---

# Azure Resources Created

| Resource | Name |
|----------|------|
| Resource Group | rg-foodexpress |
| App Service Plan | foodexpress-plan |
| App Service | foodexpress-web |
| Managed Certificate | App Service Managed Certificate |
| Autoscale Setting | CPU Autoscale |
| GitHub Actions | Deployment Workflow |

---

# Expected Outcome

The application should:

- Be deployed successfully to Azure
- Be accessible through a custom domain
- Use HTTPS
- Automatically scale when CPU usage exceeds 70%
- Deploy automatically from GitHub
- Achieve high availability using Azure App Service

---

# Verification Checklist

| Requirement | Status |
|-------------|--------|
| Azure App Service Created | ✅ |
| ASP.NET Core App Deployed | ✅ |
| GitHub Deployment Configured | ✅ |
| Custom Domain Added | ✅ |
| HTTPS Enabled | ✅ |
| Autoscaling Configured | ✅ |
| High Availability Achieved | ✅ |
| Application Accessible | ✅ |

---

# Learning Outcomes

After completing this lab, you will be able to:

- Deploy ASP.NET Core applications to Azure App Service.
- Configure GitHub CI/CD using Deployment Center.
- Configure custom domains and SSL certificates.
- Implement autoscaling based on CPU utilization.
- Understand Azure PaaS for hosting web applications.
- Verify application availability and scalability.