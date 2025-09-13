# MySQL Installation Guide for Windows

## What is SQL and MySQL?

### SQL (Structured Query Language)
- SQL is a **language** used to communicate with databases
- Just like we use English to talk to people, we use SQL to talk to databases
- It lets you ask questions like:
  - "Show me all customers from New York"
  - "What were our total sales last month?"
  - "Which products are running low in stock?"
- SQL is universal - once you learn it, you can use it with almost any database
- Every data analyst needs to know SQL - it's essential for the job

### MySQL
- MySQL is **database software** - it's the actual program that stores and manages data
- Think of it like this: If SQL is the language, MySQL is the person you're talking to
- It's completely **free** (that's why we use it for learning)
- Real companies use it: Facebook, Twitter, YouTube, Netflix, Spotify
- Other database software exists (Oracle, SQL Server, PostgreSQL) but they all understand SQL
- We'll use MySQL to practice writing SQL and managing databases

### Why This Matters
- In the real world, company data isn't in Excel files - it's in databases
- To analyze that data, you need to know how to get it out using SQL
- MySQL gives us a real database environment to practice with

## Step 1: Download MySQL

Go to: https://dev.mysql.com/downloads/installer/

Choose the **second option**:
- **Windows (x86, 32-bit), MSI Installer** (Size: ~450MB)
- Click **"Download"**
- Click **"No thanks, just start my download"**

## Step 2: Install MySQL

1. **Run the downloaded file**
2. **Choose Setup Type:** Select **"Developer Default"** → Next
3. **Check Requirements:** Click **Next** → Execute → Next
4. **Installation:** Click **Execute** → Next
5. **Configuration:** Click **Next** → Next

## Step 3: Set Password

When you see **"Accounts and Roles"**:
- Set Root Password: **password**
- Repeat Password: **password**
- Click **Next**

## Step 4: Finish Setup

- Keep clicking **Next** → Execute → Finish
- Do this until installer closes

## Step 5: Test Installation

1. Open **MySQL Workbench** from Start Menu
2. Double-click **"Local instance MySQL80"**
3. Enter Password: **password**
4. If it connects - you're done!

## Remember Your Login

- **Username:** root
- **Password:** password

## If Something Goes Wrong

- Restart your computer and try MySQL Workbench again
- Make sure you typed password: **password**