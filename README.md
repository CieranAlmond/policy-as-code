# policy-as-code
Policy as Code lab provided by Ashley Pearce - www.linkedin.com/in/ashley-thornhill


# 🛡️ Policy-as-Code Lab 01 – No Public Buckets Allowed

Public S3 buckets mean anyone on the internet can access the data inside — no password, no warning.

Even if you don't mean to expose sensitive info, a misconfigured bucket can lead to:
- 🕵️‍♀️ Leaked customer data  
- 🗂️ Exposed internal files  
- 📉 Compliance violations  
- 🚨 Major reputation damage

**This lab teaches you how to prevent that by writing a security policy in code.**

---

## 📚 Overview

You’ll create a lightweight **security rule** that **blocks public AWS S3 buckets** from being deployed — using policy as code.

By the end, you’ll:
- ✅ Understand how policy-as-code works  
- ✅ Write a Rego policy  
- ✅ Test it against a fake S3 config  
- ✅ Run everything in GitHub Codespaces (no setup needed)

---

## 🛠️ Tools Used

- **GitHub** – to host your files  
- **GitHub Codespaces** – browser-based development  
- **Rego** – the policy language  
- **Conftest** – tests your config files against your rules

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

input.json

css
Copy
Edit

Paste in this content:

```json
{
  "resource_type": "aws_s3_bucket",
  "acl": "public-read"
} ```

🔸 2. Create policy/input.rego
Click Add file → Create new file and name it:

pgsql
Copy
Edit
policy/input.rego
Paste in this policy code:

rego
Copy
Edit
package s3policy

deny[message] {
  input.resource_type == "aws_s3_bucket"
  input.acl == "public-read"
  message := "S3 buckets cannot be publicly readable (acl: public-read)"
}
🔸 3. Create conftest.toml
In the root directory, create a file called:

Copy
Edit
conftest.toml
Paste this line:

toml
Copy
Edit
policy = "./policy"
🔸 4. Commit All Files
Make sure all files are saved and committed to your main branch.

💻 Step 3: Open in GitHub Codespaces
In your repo, click the green Code button

Select Open with Codespaces → Create new codespace

Wait for the Codespace to launch

📦 Install Conftest in the Terminal
Open the Terminal (top menu → Terminal → New Terminal) and paste the following commands one at a time:

bash
Copy
Edit
wget https://github.com/open-policy-agent/conftest/releases/download/v0.45.0/conftest_0.45.0_Linux_x86_64.tar.gz
bash
Copy
Edit
tar -xzf conftest_0.45.0_Linux_x86_64.tar.gz
bash
Copy
Edit
sudo mv conftest /usr/local/bin
✅ Confirm Conftest Installed
Run this:

bash
Copy
Edit
conftest --version
If you see a version number like 0.45.0, you're good to go!

🧪 Step 4: Test the Policy
In the terminal, run:

bash
Copy
Edit
conftest test input.json --all-namespaces
You should see this output:

pgsql
Copy
Edit
FAIL - input.json - S3 buckets cannot be publicly readable (acl: public-read)
🎉 Success! Your policy is working.

🎯 What You Did
You just:

✅ Wrote a security policy using Rego

✅ Tested real-looking cloud config (input.json)

✅ Got a pass/fail result using conftest
