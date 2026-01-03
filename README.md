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

