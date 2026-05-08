# CODE-ALPHA-PYTHON-PROGRAMMING-INTERNSHIP-TASK-3
```markdown
# 🤖 Task Automation with Python Scripts

> **CodeAlpha Python Programming Internship – Task 3**  
> A collection of small Python scripts to automate repetitive real‑life tasks, including extracting email addresses from text files, moving image files, and scraping webpage titles.

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Made with Colab](https://img.shields.io/badge/Made%20with-Colab-orange)](https://colab.research.google.com/)

---

## 📖 Table of Contents

- [Project Description](#project-description)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
  - [1. Extract Email Addresses](#1-extract-email-addresses)
  - [2. Move JPG Files](#2-move-jpg-files)
  - [3. Scrape Webpage Title](#3-scrape-webpage-title)
- [Screenshots / Demo](#screenshots--demo)
- [Future Improvements](#future-improvements)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)
- [Contact](#contact)

---

## 📌 Project Description

This project provides **three simple automation scripts** that solve everyday repetitive tasks using Python. You can choose to implement one (or more) of the following:

- **Email Extractor** – Reads a `.txt` file, finds all email addresses using regular expressions, and saves them to a new file.
- **File Organiser** – Moves all `.jpg` images from a source folder to a destination folder.
- **Web Scraper** – Fetches the title of a given webpage and saves it to a text file.

All scripts use only the Python standard library (plus `requests` for web scraping, which is also pre‑installed in Colab). They are designed to run in **Google Colab** or any local Python environment.

---

## ✨ Features

### Common to all scripts
- **No external dependencies** except `requests` (already available in Colab).
- **Clear console output** with status messages.
- **Error handling** for missing files, invalid URLs, etc.
- **Easy to customise** – change source/destination paths or target URL.

### Script‑specific features

| Script                      | Highlights                                                                 |
| --------------------------- | -------------------------------------------------------------------------- |
| **Email Extractor**         | Uses regex `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}` to find emails. |
| **File Mover**              | Creates destination folder automatically, uses `shutil.move`.              |
| **Web Scraper**             | Fetches HTML, parses `<title>` tag, works with any valid URL.              |

---

## 🛠 Tech Stack

| Category         | Tools / Libraries                                      |
| ---------------- | ------------------------------------------------------ |
| **Language**     | Python 3.8+                                            |
| **Standard libs**| `os`, `shutil`, `re`, `glob`, `urllib` (or `requests`) |
| **Web scraping** | `requests` (included in Colab)                         |
| **Environment**  | Google Colab / any terminal                            |

---

## 📁 Project Structure

```
CodeAlpha_Task_Automation/
├── email_extractor.py        # Extract emails from a text file
├── move_jpg_files.py         # Move all .jpg images to a new folder
├── webpage_title_scraper.py  # Scrape and save webpage title
├── sample.txt                # Example input file for email extraction
├── README.md                 # This file
├── requirements.txt          # (empty – only Python standard library + requests)
└── output/                   # Generated output files
    ├── emails_found.txt
    ├── page_title.txt
    └── jpg_destination/
```

---

## 🚀 Installation & Setup

### Option 1: Google Colab (Recommended – zero setup)

1. Open the notebook version in Colab:  
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/shaikhdaiyaan251-cloud/CODE-ALPHA-PYTHON-PROGRAMMING-INTERNSHIP-TASK-3/blob/main/Task_Automation.ipynb)

2. Run the cell corresponding to the automation task you want.

3. For file‑based tasks (email extraction, file moving), you will need to upload a sample `.txt` file or create a folder with `.jpg` images. Colab's file upload widget makes this easy.

### Option 2: Local Python environment

1. Clone the repository:
   ```bash
   git clone https://github.com/shaikhdaiyaan251-cloud/CODE-ALPHA-PYTHON-PROGRAMMING-INTERNSHIP-TASK-3.git
   cd CODE-ALPHA-PYTHON-PROGRAMMING-INTERNSHIP-TASK-3
   ```

2. (Optional) Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   ```

3. Install `requests` if you plan to use the web scraper (Colab already has it):
   ```bash
   pip install requests
   ```

4. Run any script directly:
   ```bash
   python email_extractor.py
   ```

---

## 💻 Usage

### 1. Extract Email Addresses

**Script:** `email_extractor.py`  
**Input:** A text file (e.g., `sample.txt`) containing text with email addresses.  
**Output:** A file `emails_found.txt` containing one email per line.

**How to use (Colab):**
- Upload your `.txt` file when prompted.
- The script will scan it and save the result.

**Code snippet** (local version):
```python
import re

def extract_emails(file_path, output_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        text = f.read()
    emails = re.findall(r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}', text)
    with open(output_path, 'w') as f_out:
        f_out.write('\n'.join(emails))
    print(f"Found {len(emails)} email(s). Saved to {output_path}")

extract_emails('sample.txt', 'emails_found.txt')
```

---

### 2. Move JPG Files

**Script:** `move_jpg_files.py`  
**Input:** Source folder (where `.jpg` files are located) and destination folder.  
**Output:** All `.jpg` files moved to the destination folder (folders are created automatically).

**How to use (Colab):**
- Create a folder in the Colab environment (or upload a zip with images).
- The script will scan the source directory and move every `.jpg` file.

**Code snippet** (local version):
```python
import os
import shutil
import glob

source = 'path/to/source_folder'
destination = 'path/to/destination_folder'

if not os.path.exists(destination):
    os.makedirs(destination)

for file_path in glob.glob(os.path.join(source, '*.jpg')):
    shutil.move(file_path, destination)
    print(f"Moved: {file_path}")

print("All .jpg files moved successfully.")
```

---

### 3. Scrape Webpage Title

**Script:** `webpage_title_scraper.py`  
**Input:** A URL (you can hardcode it or ask the user).  
**Output:** A text file `page_title.txt` containing the title of the webpage.

**How to use (Colab):**
- The script uses `requests` to fetch the HTML and extracts the `<title>`.
- Save the title to a file.

**Code snippet** (local version):
```python
import requests
from bs4 import BeautifulSoup  # not needed, we can use regex or split

def get_title(url, output_path):
    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
        # Quick way to extract title without BeautifulSoup
        if '<title>' in response.text:
            start = response.text.find('<title>') + 7
            end = response.text.find('</title>')
            title = response.text[start:end].strip()
            with open(output_path, 'w') as f:
                f.write(title)
            print(f"Title saved: {title}")
        else:
            print("No <title> tag found.")
    except Exception as e:
        print(f"Error: {e}")

get_title('https://example.com', 'page_title.txt')
```

---

## 📸 Screenshots / Demo

> *Placeholder for actual screenshots. For example:*

**Email extraction – sample run:**
```
📂 Upload your .txt file: sample.txt
✅ Found 5 email addresses.
💾 Results saved to emails_found.txt
```

**File moving:**
```
📁 Source: /content/images/
📁 Destination: /content/jpg_backup/
✅ Moved: image1.jpg
✅ Moved: image2.jpg
```

**Web scraper:**
```
🌐 Fetching: https://codealpha.tech
✅ Title: "CodeAlpha – Software Development Company"
💾 Saved to page_title.txt
```

---

## 🔮 Future Improvements

- **Add a graphical user interface** (e.g., using `tkinter` or a simple web interface).
- **Support more file types** – PNG, PDF, DOCX.
- **Schedule automation** – run scripts periodically using `cron` (Linux/macOS) or Task Scheduler (Windows).
- **Extract emails from multiple files** in a directory.
- **Scrape more information** – meta descriptions, headings, etc.

---

## 🤝 Contributing

Contributions are welcome! If you improve a script or add a new automation idea:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/new-automation`).
3. Commit your changes (`git commit -m 'Add new automation script'`).
4. Push to the branch (`git push origin feature/new-automation`).
5. Open a Pull Request.

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

## 🙏 Acknowledgements

- **CodeAlpha** – for the internship opportunity and task ideas.
- Python’s `re`, `shutil`, `glob`, and `requests` – making automation effortless.

---

## 📬 Contact

**DAIYAAN SHAIKH** – [LinkedIn](https://www.linkedin.com/in/daiyaan-shaikh-159909377?utm_source=share_via&utm_content=profile&utm_medium=member_android) – [GitHub](https://github.com/shaikhdaiyaan251-cloud)  
Project Link: [[https://github.com/shaikhdaiyaan251-cloud/CODE-ALPHA-PYTHON-PROGRAMMING-INTERNSHIP-TASK-3](https://github.com/shaikhdaiyaan251-cloud/CODE-ALPHA-PYTHON-PROGRAMMING-INTERNSHIP-TASK-3)]

---

⭐ **If these automation scripts saved you time, please give the repository a star!** ⭐
```
