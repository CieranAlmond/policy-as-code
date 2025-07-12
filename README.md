# policy-as-code
Policy as Code lab provided by Ashley Pearce - www.linkedin.com/in/ashley-thornhill


# what we are trying to achieve

This lab helps you prevent a common and dangerous mistake: making an AWS S3 bucket public (which means anyone online can see or download your files — not good!).

To catch this mistake early, you’ll build a security rule (called a "policy") in code that checks for this risky setting, before it goes live.

🛠️ Tools Used:
GitHub – where you store and edit your code

GitHub Codespaces – an online coding environment (no installs needed)

Rego – a simple language for writing security rules

Conftest – a tool that tests your files against your rules

🚶 STEP-BY-STEP EXPLANATION
# 🔹 Step 1: Create a GitHub Repo
🧾 What you're doing:
Creating a project folder on GitHub where all your files will live.

👣 Steps:

Log into github.com

Click the + in the top-right, choose New repository

Name it something like no-public-s3

Check the box to add a README (this just creates a starting file)

Click Create repository

🧠 Why: This is your workspace for the rest of the lab.

# 🔹 Step 2: Add These Files
🧾 What you're doing:
Creating a fake AWS S3 configuration, a policy to catch public buckets, and a config file to help test it.

👣 Files to create:

✅ 1. input.json
This simulates a cloud resource (like a Terraform or cloud config file):

json
Copy
Edit
{
  "resource_type": "aws_s3_bucket",
  "acl": "public-read"
}
📌 What this means:
You're pretending to create an S3 bucket that’s public ("acl": "public-read"), which is what we want to block.

✅ 2. policy/input.rego
This is your security policy, written in the Rego language.

rego
Copy
Edit
package s3policy

deny[message] {
  input.resource_type == "aws_s3_bucket"
  input.acl == "public-read"
  message := "S3 buckets cannot be publicly readable (acl: public-read)"
}
📌 What this means:
If the resource is an S3 bucket and it's set to public-read, then this rule will deny it and print a message.

✅ 3. conftest.toml
This tells Conftest where your policies live.

toml
Copy
Edit
policy = "./policy"
📌 Why: Makes it easier to run tests by telling Conftest where to find your Rego file.

# 🔹 Step 3: Open in Codespaces
🧾 What you're doing:
Launching an online coding environment and installing the Conftest testing tool.

👣 Steps:

In your GitHub repo, click the green Code button

Choose Open with Codespaces → Create new codespace

In the terminal at the bottom, paste these one at a time:

bash
Copy
Edit
wget https://github.com/open-policy-agent/conftest/releases/download/v0.45.0/conftest_0.45.0_Linux_x86_64.tar.gz
tar -xzf conftest_0.45.0_Linux_x86_64.tar.gz
sudo mv conftest /usr/local/bin
Run this to confirm it worked:

bash
Copy
Edit
conftest --version
📌 Why:
You need Conftest installed so you can test your security rule. The --version command checks if it installed correctly.

# 🔹 Step 4: Test the Policy
🧾 What you're doing:
Running your security rule against the fake input file.

👣 Command to run:

bash
Copy
Edit
conftest test input.json --all-namespaces
📌 What happens:
Conftest looks at input.json, checks it against the rule in input.rego, and tells you if the input breaks the rule.

✅ Expected output:

pgsql
Copy
Edit
FAIL - input.json - S3 buckets cannot be publicly readable (acl: public-read)
🎉 What this means:
It caught the bad config like we wanted — your policy is working!
