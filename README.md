# file-audit-report
A reliable, read-only Python script used to scan a folder and generate an audit report of all known files.

A safe, read-only Python tool that scans a folder and generates a clear audit report of files — including size, age, and type... without modifying anything.

Designed for businesses that want visibility before cleanup or automation.

This file audit report tool works out by scanning a target folder, counting total files, calculating total storage size, identifing the largest, smallest, newest and oldest files, along with exporting a informative CSV report that contains a clear terminal summary of it all.

As this is a read-only tool, no files are deleted or altered.

Before I come into a business pushing my automation tools, I'll need to run this tool to be able to provide insight for the business owner/individuals. The answers to this will include:
What’s taking up space?
How old are the files?
What types of files exist?
Where are the risks?

This file audit report tool will provide clarity and confidence before any action is taken, providing relief to anyone who requires work being done on their computers/systems.

How I had ran this is by:
Clone or download the repository
Add files to the test_files folder
Apply the filepath in question that has the test_files folder into PowerShell
Run the python script in PowerShell:
python audit.py

The audit report should show up with something like this:
>>> MAIN() IS RUNNING <<<
SCRIPT LOCATION: C:\Users\Zain\Documents\Python Work\File Audit Report
TARGET FOLDER: C:\Users\Zain\Documents\Python Work\File Audit Report\test_files
REPORT FILE: C:\Users\Zain\Documents\Python Work\File Audit Report\audit_report.csv
===== FILE AUDIT SUMMARY =====
Folder: C:\Users\Zain\Documents\Python Work\File Audit Report\test_files
Total files: 7
Total size : 25.428 MB
Largest file: 22920-AudiRS3ComparativeDataNovemberFINAL.pdf (16.85 MB)
Oldest file : 4790-AudiRS5CoupéPricelistMay2018.pdf (modified 2026-01-03 01:11:50.291219)
Newest file : 2D274906865153-today-clea-paul-newman-140926-tease-02_2500x.webp (modified 2026-01-03 01:13:29.913595)

In this CSV, the audit report, you can see that this contains:
filename
extension
size (bytes & MB)
last modified date
full file path

Like I mentioned above in this, there is:
No file modifications
No deletions
No overwrites
No permissions required

For this tool and the other tools that I had made with Python and Visual Studio Code, I will target:
law firms
accountants
agencies
small businesses
compliance-sensitive environments

Version 1 of this contains:
Initial release
Folder scan
Summary output
CSV export

The code for this is as follows:

from pathlib import Path
from datetime import datetime
import csv

# ======================
# CONFIG
# ======================
BASE_DIR = Path(__file__).parent
TARGET_FOLDER = BASE_DIR / "test_files"
REPORT_FILE = BASE_DIR / "audit_report.csv"
# =======================


def bytes_to_mb(num_bytes: int) -> float:
    return num_bytes / (1024 * 1024)


def safe_mtime(path: Path) -> datetime:
    return datetime.fromtimestamp(path.stat().st_mtime)


def main() -> None:
    print(">>> MAIN() IS RUNNING <<<")
    print("SCRIPT LOCATION:", BASE_DIR)
    print("TARGET FOLDER:", TARGET_FOLDER)
    print("REPORT FILE:", REPORT_FILE)
    if not TARGET_FOLDER.exists():
        print(f"[ERROR] Target folder not found: {TARGET_FOLDER}")
        return

    files = [p for p in TARGET_FOLDER.iterdir() if p.is_file()]

    if not files:
        print("No files found in target folder.")
        return

    rows = []
    total_size = 0

    for f in files:
        size = f.stat().st_size
        total_size += size
        rows.append(
            {
                "name": f.name,
                "extension": f.suffix.lower(),
                "size_bytes": size,
                "size_mb": round(bytes_to_mb(size), 3),
                "modified": safe_mtime(f).strftime("%Y-%m-%d %H:%M:%S"),
                "full_path": str(f),
            }
        )

    total_files = len(files)
    total_mb = round(bytes_to_mb(total_size), 3)

    largest = max(files, key=lambda p: p.stat().st_size)
    oldest = min(files, key=lambda p: p.stat().st_mtime)
    newest = max(files, key=lambda p: p.stat().st_mtime)

    print("===== FILE AUDIT SUMMARY =====")
    print(f"Folder: {TARGET_FOLDER}")
    print(f"Total files: {total_files}")
    print(f"Total size : {total_mb} MB")
    print(
        f"Largest file: {largest.name} ({round(bytes_to_mb(largest.stat().st_size), 3)} MB)"
    )
    print(f"Oldest file : {oldest.name} (modified {safe_mtime(oldest)})")
    print(f"Newest file : {newest.name} (modified {safe_mtime(newest)})")

    with open(REPORT_FILE, "w", newline="", encoding="utf-8") as f:
        writer = csv.DictWriter(f, fieldnames=rows[0].keys())
        writer.writeheader()
        writer.writerows(rows)

    print(f"\nReport created: {REPORT_FILE}")

if __name__ == "__main__":
    main()

#### Author ####

Zain Barkatali
Barkatali Technology
Automation & IT systems for small businesses
