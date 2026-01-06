# 🛡️ Lab 0 — Guardrails (Cost + Safety)

In this lab, I set up **cost and safety guardrails** *before* starting any infrastructure work for the **EC2 to Aurora PostgreSQL migration series**. The goal was to **prevent accidental spend**, **enable fast cleanup**, and **stay in full control** while experimenting.

---

## 📋 Lab Overview

**Goal:**

* Establish a clear **resource naming prefix**
* Apply **consistent tags** to everything created
* Set a **hard monthly cost limit** using AWS Budgets
* Ensure the lab can be **identified and deleted quickly**

**Learning Outcomes:**

* Understand why guardrails come **before** infrastructure
* Design a reusable **tagging strategy**
* Create an AWS **monthly cost budget**
* Prevent unexpected cloud spend during labs

---

## 🛠 Step-by-Step Journey

### Step 1: Define a Lab Prefix & Tagging Strategy

**Why this matters:**
Before creating *any* resources, I decided how everything would be identified and cleaned up later.

---

#### 🔖 Chosen Prefix

```
lab-aurora-mig
```

* Short
* Descriptive
* Easy to search and delete later

---

#### 🏷 Tagging Strategy

All resources created in this lab will use the same tags:

| Key     | Value          | Purpose                              |
| ------- | -------------- | ------------------------------------ |
| project | lab-aurora-mig | Identify all migration lab resources |
| owner   | suleyman       | Ownership & accountability           |
| ttl     | 24h            | Signals temporary resources          |

**Key Idea:**
Tags act like **labels on boxes** — they let you quickly find, filter, and delete everything related to a lab.

---

### Step 2: Choose the Correct AWS Region

Before touching billing, I verified I was in the correct region:

```
eu-west-2 (London)
```

* Matches where the lab resources will be deployed
* Avoids confusion across regions

---

### Step 3: Create a Hard Cost Limit with AWS Budgets

**Objective:**
Prevent accidental overnight spending.

---

#### Navigation Path

```
AWS Console → Billing → Budgets → Create budget
```

---

#### Budget Configuration

* **Budget Type:** Monthly cost budget (template)
* **Budget Name:** My Monthly Cost Budget
* **Budget Amount:** `$15`
* **Email Alerts:** Enabled (my email)

<img width="489" height="50" alt="Screenshot 2026-01-06 at 13 54 15" src="https://github.com/user-attachments/assets/271029f7-5cae-4124-aa3d-842587c56b0e" />

---

#### Alert Thresholds

AWS will notify me when:

1. **85%** of budget is reached
2. **100%** of actual spend is reached
3. **Forecasted spend** is expected to hit 100%

---

### Step 4: Expected Outcome

With these guardrails in place:

* I **won’t accidentally burn money overnight**
* Every resource is **easy to identify**
* Cleanup is **fast and safe**
* I can experiment confidently

---

## ✅ Key Actions Summary

| Task                        | Result |
| --------------------------- | ------ |
| Lab prefix defined          | ✅      |
| Tagging strategy created    | ✅      |
| AWS region verified         | ✅      |
| Monthly cost budget created | ✅      |
| Email alerts enabled        | ✅      |

---

## 💡 Notes / Tips

* Always set **guardrails before infrastructure**
* Tags are your **safety net for cleanup**
* Budgets protect you from **human error**
* Low budgets are perfect for **labs and experiments**
* TTL tags are especially useful in teams

---

## 📌 Lab Summary

| Area             | Status | Key Takeaway              |
| ---------------- | ------ | ------------------------- |
| Naming strategy  | ✅      | Clear, searchable prefix  |
| Resource tagging | ✅      | Enables fast cleanup      |
| Cost control     | ✅      | Hard spend limit in place |
| Safety posture   | ✅      | Ready for experimentation |

---

## ✅ References

* [https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)
* [https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html](https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html)
* [https://docs.aws.amazon.com/whitepapers/latest/aws-well-architected-framework/cost-optimization.html](https://docs.aws.amazon.com/whitepapers/latest/aws-well-architected-framework/cost-optimization.html)
