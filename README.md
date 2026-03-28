<p align="center">
  <img src="PlistParser.jpg" alt="PlistParser Banner" width="850">
</p>

# PlistParser

**PlistParser** is a forensic tool for parsing macOS property list (plist) files in binary and XML formats. Built for DFIR and working with live macOS systems or offline triage images, it supports flexible export formats and a live system scan mode for rapid forensic collection.

## Features

- Parses **binary**, **XML** plist formats.
- Exports results as **TXT**, **JSON**, or **CSV** with auto-detected columns per plist.
- **Live scan mode** (`--live`) - scans relevant forensic plist locations on a live macOS system including Safari, Preferences, LaunchAgents/Daemons, Containers, iCloud, and more.
- Supports **single file**, **recursive directory**, and **live system** scanning modes.
- Handles **duplicate filenames** across directories - renames and logs automatically.
- Available as a **standalone executable** for Windows, Linux, and macOS - no dependencies required.

## Download

| Platform | Download |
|----------|----------|
| Windows  | [PlistParser_Windows.7z](./PlistParser_Windows.7z) |
| Linux    | [PlistParser_Linux.7z](./PlistParser_Linux.7z) |
| macOS    | [PlistParser_macOS.7z](./PlistParser_macOS.7z) |

## Installation and Usage

### Windows

- Extract the `.7z` archive.
- Open **Command Prompt** or **PowerShell** in the folder where the executable is located.
- Run:

  ```
  PlistParser.exe --help
  ```

---

### Linux

- Extract the `.7z` archive:
  ```bash
  7z x PlistParser_Linux.7z
  ```
- Grant executable permission:
  ```bash
  chmod +x PlistParser
  ```
- Run:
  ```bash
  ./PlistParser --help
  ```

---

### macOS

- Extract the `.7z` archive:
  ```bash
  7z x PlistParser_macOS.7z
  ```
- Grant executable permission:
  ```bash
  chmod +x PlistParser
  ```
- Run:
  ```bash
  ./PlistParser --help
  ```

---

## Modes

### Single File Mode

Parse a single plist file and print results to the console:

```bash
PlistParser Downloads.plist
```

Parse and export to one or more formats:

```bash
PlistParser Downloads.plist --txt
PlistParser Downloads.plist --json
PlistParser Downloads.plist --txt --json --csv
```

Parse and save to a specific output folder (no console output):

```bash
PlistParser.exe Downloads.plist --txt -o C:\results          # Windows
./PlistParser Downloads.plist --txt -o ~/results         # Linux / macOS
```

---

### Directory Mode

Scan a folder recursively and export all parsed plists:

```bash
PlistParser.exe C:\Triage\ --txt                             # Windows
./PlistParser /mnt/triage/ --txt                         # Linux
./PlistParser ~/Library/Preferences/ --txt               # macOS
```

Output is saved to `Desktop\PlistParser_Results\` (Windows) or `~/Desktop/PlistParser_Results/` (macOS/Linux) unless `-o` is specified.

---

### Live Mode - macOS Only

Scan all forensically relevant plist locations on the live macOS system:

```bash
./PlistParser --live --txt
./PlistParser --live --txt --json --csv
./PlistParser --live --txt --json --csv -o ~/Desktop/case01
```

For full access to system-level plists, run with elevated privileges:

```bash
sudo ./PlistParser --live --txt
```

---

## Flags

| Flag | Description |
|------|-------------|
| `--txt` | Save parsed output as plain text (`.parsed.txt`) |
| `--json` | Save parsed output as JSON (`.parsed.json`) |
| `--csv` | Save structured CSV with auto-detected columns (`.parsed.csv`) |
| `--live` | Scan forensic plist locations on the live macOS system *(macOS only)* |
| `-o <dir>` | Custom output directory |
| `-h, --help` | Show help message |

---

## Output

- **TXT** - human-readable parsed output, one file per plist.
- **JSON** - full structured output preserving all data types.
- **CSV** - auto-detects the structure of each plist and creates proper columns. For example, `Downloads.plist` produces a CSV with one row per download entry and named columns like `DownloadEntryURL`, `DownloadEntryPath`, `DownloadEntryDateAddedKey`, etc.
- **duplicates_log.txt** - created when duplicate filenames are found across directories, listing original paths and renamed output files.

---

## Important Notice

Some antivirus software may flag the executable as a false positive. This is due to the way the tool is packaged using **Python** and **PyInstaller**, which can sometimes trigger heuristic detections.

If you encounter warnings, consider:

- Running the tool in a sandbox or isolated environment.
- Adding an exclusion rule for the executable in your antivirus software.
- Temporarily disabling your antivirus software.

---

## Contact

For questions or feedback, contact me via https://www.linkedin.com/in/guy-eldad/

---

*Copyright © 2025 Guy Eldad. All rights reserved.*
