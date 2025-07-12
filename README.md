# policy-as-code
Policy as Code lab provided by Ashley Pearce - www.linkedin.com/in/ashley-thornhill


# 📚 Overview

You’ll create a lightweight security rule that blocks public AWS S3 buckets from being deployed — using policy as code.

By the end, you’ll:

✅ Understand how policy-as-code works

✅ Write a Rego policy

✅ Test it against a fake S3 config

✅ Run everything in GitHub Codespaces (no setup needed)

# 🛠️ Tools Used

GitHub – to host your files

GitHub Codespaces – browser-based development

Rego – the policy language

Conftest – tests your config files against your rules

# 🚀 Step 1: Create a GitHub Repo

What you're doing: Setting up a safe place online to store all your code files. This is like creating a new folder in the cloud where everything related to your security rule will live.

# 📂 Step 2: Add These Files

🔸 1. Create input.json

What you're doing: Making a pretend AWS S3 bucket config file. This simulates a real-world cloud setup, and you'll test your rule against this file.

🔸 2. Create policy/input.rego

What you're doing: Writing the actual rule that blocks public S3 buckets. It's like saying, "If the bucket is public, stop it and show a warning message."

🔸 3. Create conftest.toml

What you're doing: Pointing your test tool (Conftest) to where your policy rule lives. It tells the tester, "Look in this folder to find the rules."

🔸 4. Commit All Files

What you're doing: Saving your progress and locking in all the files so they’re tracked in your project history.

# 💻 Step 3: Open in GitHub Codespaces

What you're doing: Opening an online coding environment so you can test everything in your browser without needing to install anything.

📦 Install Conftest in the Terminal

What you're doing: Installing a tool (Conftest) that checks if your config files follow your rules. It's like adding a safety inspector to your workspace.

✅ Confirm Conftest Installed

What you're doing: Making sure your safety inspector (Conftest) is ready to work. You're checking that it was installed correctly.

# 🧪 Step 4: Test the Policy

What you're doing: Running the inspector tool (Conftest) to check if your pretend S3 bucket violates the rule. If the bucket is public, it will fail the test and show a warning.

🌟 What You Did

You just:

✅ Wrote a security rule using simple logic

✅ Tested it against a pretend setup

✅ Got automatic feedback when something didn’t follow the rule

🔐 The Impact

Without this kind of check:

A developer could accidentally push a public bucket

You risk exposing data to the entire internet

Compliance, trust, and your company's name are on the line

With policy-as-code:

👨‍💻 Developers get early feedback

❌ Risky misconfigs are blocked early

🛌 Compliance teams sleep better


