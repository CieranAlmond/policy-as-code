# policy-as-code
Policy as Code lab provided by Ashley Pearce - www.linkedin.com/in/ashley-thornhill


# 🛡️ Policy-as-Code Lab 01 – No Public Buckets Allowed

Public S3 buckets mean anyone on the internet can access the data inside — no password, no warning.

Even if you don't mean to expose sensitive info, a misconfigured bucket can lead to:

* 😎 Leaked customer data
* 📂 Exposed internal files
* 📉 Compliance violations
* 🚨 Major reputation damage

**This lab teaches you how to prevent that by writing a security policy in code.**

---

## 📚 Overview

You’ll create a lightweight **security rule** that **blocks public AWS S3 buckets** from being deployed — using policy as code.

By the end, you’ll:

* ✅ Understand how policy-as-code works
* ✅ Write a Rego policy
* ✅ Test it against a fake S3 config
* ✅ Run everything in GitHub Codespaces (no setup needed)

---

## 🛠️ Tools Used

* **GitHub** – to host your files
* **GitHub Codespaces** – browser-based development
* **Rego** – the policy language
* **Conftest** – tests your config files against your rules

---

## 🚀 Step 1: Create a GitHub Repo

1. Go to [github.com](https://github.com) and log in
2. Click the **➕** in the top-right → `New repository`
3. Name it something like `no-public-s3`
4. Check the box to **Add a README**
5. Click **Create repository**

---

## 📂 Step 2: Add These Files

### 🔸 1. Create `input.json`

Click **Add file → Create new file** and name it:

```
input.json
```

Paste in this content:

```json
{
  "resource_type": "aws_s3_bucket",
  "acl": "public-read"
}
```

---

### 🔸 2. Create `policy/input.rego`

Click **Add file → Create new file** and name it:

```
policy/input.rego
```

Paste in this policy code:

```rego
package s3policy

deny[message] {
  input.resource_type == "aws_s3_bucket"
  input.acl == "public-read"
  message := "S3 buckets cannot be publicly readable (acl: public-read)"
}
```

---

### 🔸 3. Create `conftest.toml`

In the root directory, create a file called:

```
conftest.toml
```

Paste this line:

```toml
policy = "./policy"
```

---

### 🔸 4. Commit All Files

Make sure all files are saved and committed to your **main branch**.

---

## 💻 Step 3: Open in GitHub Codespaces

1. In your repo, click the green **Code** button
2. Select **Open with Codespaces → Create new codespace**
3. Wait for the Codespace to launch

---

### 📦 Install Conftest in the Terminal

Open the **Terminal** (top menu → `Terminal → New Terminal`) and paste the following commands one at a time:

```bash
wget https://github.com/open-policy-agent/conftest/releases/download/v0.45.0/conftest_0.45.0_Linux_x86_64.tar.gz
```

```bash
tar -xzf conftest_0.45.0_Linux_x86_64.tar.gz
```

```bash
sudo mv conftest /usr/local/bin
```

---

### ✅ Confirm Conftest Installed

Run this:

```bash
conftest --version
```

If you see a version number like `0.45.0`, you're good to go!

---

## 🧪 Step 4: Test the Policy

In the terminal, run:

```bash
conftest test input.json --all-namespaces
```

You should see this output:

```
FAIL - input.json - S3 buckets cannot be publicly readable (acl: public-read)
```

🎉 **Success! Your policy is working.**

---

## 🌟 What You Did

You just:

* ✅ Wrote a security policy using Rego
* ✅ Tested real-looking cloud config (`input.json`)
* ✅ Got a pass/fail result using `conftest`

---

## 🔐 The Impact

Without this kind of check:

* A developer could accidentally push a **public bucket**
* You risk exposing data to the entire internet
* Compliance, trust, and your company's name are on the line

With **policy-as-code**:

* 👨‍💻 Developers get early feedback
* ❌ Risky misconfigs are blocked early
* 🛌 Compliance teams sleep better

---

> Created by [Ashley Pearce](https://www.linkedin.com/in/ashley-thornhill)
> Senior InfoSec Analyst – CATO/RMF Wizard
