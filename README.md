# CyberSecurity Awareness Bot (CSAB) — Part 3

A WPF desktop application built in C# that educates users on cybersecurity through an interactive chatbot, task manager, quiz, and activity log.

---

## Table of Contents
- [About the Project](#about-the-project)
- [Features](#features)
- [Requirements](#requirements)
- [Setup Instructions](#setup-instructions)
- [How to Run](#how-to-run)
- [How to Use](#how-to-use)
- [Project Structure](#project-structure)
- [Database Structure](#database-structure)

---

## About the Project

CSAB is a Cybersecurity Awareness Chatbot developed as Part 3 of a multi-part academic project. It builds on Parts 1 and 2 by adding a Task Manager with MySQL database integration, a cybersecurity quiz mini-game, an NLP simulation engine, and an Activity Log — all wrapped in a WhatsApp-style GUI using XAML and WPF.

---

## Features

### Chat Tab
- WhatsApp-style chat bubbles with timestamps
- Remembers your name and favourite topic across the conversation
- Sentiment detection — responds differently if you seem worried, frustrated, or curious
- Covers topics: passwords, phishing, privacy, malware, safe browsing, social engineering, and 2FA

### Tasks Tab
- Add cybersecurity tasks with a title, description, and optional reminder
- Tasks are saved to a MySQL database
- Mark tasks as completed or delete them
- Changes reflect in the database instantly

### Quiz Tab
- 12 cybersecurity questions covering phishing, passwords, malware, 2FA, and more
- Questions and answer options are shuffled randomly every time
- Instant feedback with explanations after each answer
- Live score tracking with a final result and performance message

### NLP Simulation
- Understands natural phrasing — no need for exact commands
- Recognises phrases like *"remind me to..."*, *"add a task"*, *"test me"*, *"what have you done?"*
- Keyword detection using `string.Contains()` and a custom `ContainsAny()` method

### Activity Log Tab
- Records every significant action with a timestamp
- Logs task additions, completions, deletions, quiz activity, and chat topics
- Displays the 10 most recent entries
- Also accessible in chat by typing `show activity log`

---

## Requirements

| Requirement | Details |
|---|---|
| IDE | Visual Studio 2022 or later |
| Framework | .NET 10.0 (Windows) |
| Language | C# with WPF (XAML) |
| Database | MySQL Server 8.0+ |
| NuGet Package | MySql.Data 9.3.0 |
| OS | Windows 10 or Windows 11 |

---

## Setup Instructions

### Step 1 — Install MySQL
Download and install MySQL from:
https://dev.mysql.com/downloads/installer/

Choose **Developer Default** during setup and set a root password you'll remember.

### Step 2 — Create the Database
Open **MySQL Workbench**, connect to your local instance, and run:
```sql
CREATE DATABASE IF NOT EXISTS csab_db;
```
The app will automatically create the `Tasks` table on first launch.

### Step 3 — Update the Connection String
Open `MainWindow.xaml.cs` and find this line near the top:
```csharp
private const string ConnStr =
    "Server=localhost;Database=csab_db;Uid=root;Pwd=;";
```
Replace `Pwd=` with your MySQL root password:
```csharp
private const string ConnStr =
    "Server=localhost;Database=csab_db;Uid=root;Pwd=YourPasswordHere;";
```

### Step 4 — Install the NuGet Package
In Visual Studio:
> Tools → NuGet Package Manager → Manage NuGet Packages for Solution

Search for `MySql.Data`, select it, and click **Install**.

### Step 5 — Add Greeting Sound (Optional)
Place a file named `greeting.wav` in the project folder. The app will automatically play it on startup.

---

## How to Run

1. Open `CyberSecurityBot Part3.sln` in Visual Studio
2. Press **Ctrl + Shift + B** to build the project
3. Press **F5** to run

---

## How to Use

### Chat Tab
| What you type | What happens |
|---|---|
| Your name (first message) | Bot greets you personally |
| `topics` or `help` | Shows all available topics |
| `password`, `phishing`, `malware` etc. | Gets a cybersecurity tip |
| `show activity log` | Displays recent bot actions |
| `add a task` / `remind me to...` | Bot directs you to the Tasks tab |
| `quiz` / `test me` | Bot directs you to the Quiz tab |
| `bye` / `exit` | Bot says goodbye |

### Tasks Tab
1. Enter a **title** for your task (required)
2. Enter a **description** (optional)
3. Enter a **reminder** — e.g. `3 days` or `2026-07-10` (optional)
4. Click **Add Task**
5. Use **Mark Done** or **Delete** on each task card

### Quiz Tab
1. Click **Start Quiz**
2. Read the question and click your chosen answer
3. Feedback and explanation appear immediately
4. Click **Next** to continue
5. Your final score and performance message appear at the end

### Activity Log Tab
- All actions are listed newest first with timestamps
- Click **Clear Log** to reset the display

---

## Project Structure

```
CyberSecurityBot Part3/
│
├── MainWindow.xaml          # All UI layout and styling
├── MainWindow.xaml.cs       # All application logic
├── App.xaml                 # Application entry point
├── App.xaml.cs              # App class
├── greeting.wav             # Optional startup sound
└── CyberSecurityBot Part3.csproj   # Project and NuGet references
```

---

## Database Structure

**Database:** `csab_db`

**Table:** `Tasks`

| Column | Type | Description |
|---|---|---|
| Id | INT (Auto) | Unique task ID |
| Title | VARCHAR(200) | Task title |
| Description | TEXT | Task details |
| Reminder | VARCHAR(100) | Reminder date or timeframe |
| IsCompleted | TINYINT(1) | 0 = pending, 1 = done |
| CreatedAt | DATETIME | When the task was created |

---

## Author

**Itebogeng**
CyberSecurity Awareness Bot — Part 3 (Academic Project)
© 2026 The Independent Institute of Education
