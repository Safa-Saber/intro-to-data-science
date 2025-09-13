# TablePlus Installation and Usage Guide

## What is TablePlus?

TablePlus is a **modern database management tool** - think of it as a user-friendly window into your database. While MySQL Workbench (which you already installed) works fine, TablePlus is:
- **Cleaner and simpler** to use
- **Faster** for everyday tasks
- **Better looking** and less intimidating for beginners
- Works with multiple database types (MySQL, PostgreSQL, SQLite, etc.)

## How We'll Use TablePlus

In class, we'll use TablePlus to:
- **View data** in your tables (like a neat spreadsheet)
- **Write and run SQL queries** with syntax highlighting
- **Edit data directly** by clicking on cells
- **Import/Export data** from CSV or Excel files
- **See table relationships** visually

Think of it as a more modern alternative to MySQL Workbench - both do the same job, but TablePlus is easier for beginners.

## Installation Steps

### Step 1: Download TablePlus

Go to: https://tableplus.com/windows

- Click **"Download for Windows"**
- Choose **"Download Free Trial"** (it's free forever with some limitations, which is fine for learning)

### Step 2: Install

1. Run the downloaded file
2. Click **"Next"** → **"I Agree"** → **"Next"** → **"Install"**
3. Click **"Finish"** when done

### Step 3: Connect to Your MySQL Database

1. Open TablePlus
2. Click **"Create a new connection"**
3. Choose **"MySQL"**
4. Fill in these details:
   - **Name:** My Local MySQL (or any name you want)
   - **Host:** localhost (or 127.0.0.1)
   - **Port:** 3306 (should be default)
   - **User:** root
   - **Password:** password
   - **Database:** (leave empty for now)

5. Click **"Test"** (should show "connection is OK")
6. Click **"Save"**

### Step 4: Connect and Explore

- Double-click your saved connection to connect
- You'll see your databases on the left side
- Click on any database to see its tables
- Double-click a table to view its data

## Your Connection Details (Same as MySQL)

- **Host:** localhost
- **Port:** 3306
- **Username:** root
- **Password:** password

## Quick Tips

- **To run SQL:** Click "SQL" button or press Ctrl+T
- **To view data:** Double-click any table name
- **To refresh:** Press F5
- **To save queries:** Use Ctrl+S

## Free Version Limitations

The free version has some limits (2 tabs, 2 windows) but it's completely sufficient for learning. You won't need the paid features for class.

## If Connection Fails

- Make sure MySQL is running (you installed it earlier)
- Check password is exactly: **password**
- Try host as **127.0.0.1** instead of localhost