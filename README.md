# Ultimate System & Software Update Scanner

[![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-brightgreen.svg)](https://github.com/yourusername/update-scanner)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Platform: Windows](https://img.shields.io/badge/Platform-Windows-blue.svg)](https://www.microsoft.com/windows)

A comprehensive Windows utility that scans your system for software and driver updates, helping you keep your system secure and up-to-date with minimal effort.

## Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Quick Start](#quick-start)
- [Installation](#installation)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Troubleshooting](#troubleshooting)
- [FAQ](#faq)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Comprehensive Software Update Detection**: Scans all installed software on your Windows system and checks for available updates
- **Chocolatey API Integration**: Queries the Chocolatey package repository for real-time version data of popular Windows software (primary update source)
- **GitHub API Integration**: Automatically checks GitHub repositories for the latest releases of supported software
- **Driver Update Detection**: Identifies outdated drivers that might affect system performance and stability (currently using simulated checks, with real-time data integration in development)
- **Clean, Intuitive Interface**: Displays results in an organized, tabbed interface for easy navigation
- **Actionable Results**: Double-click on items with available updates to open the relevant update page or launcher
- **Detailed Logging**: Keeps a log of all scanning activities for troubleshooting and audit purposes
- **Portable Application**: No installation required - run directly from any location

## Requirements

- **Operating System**: Windows 10 or Windows 11
- **Runtime**: Python 3.6 or higher
- **Required Python Packages**:
  - tkinter (usually included with Python installation)
  - requests (for network operations)
  - packaging (for version comparison, automatically installed if missing)
  - xml.etree.ElementTree (for parsing XML responses, included with Python)
- **Permissions**: Administrative privileges required for complete system scanning

## Quick Start


1. Click the "Scan for Updates" button
2. Review the results and update your software as needed

## Installation

1. Ensure Python 3.6+ is installed on your system
   - You can download Python from [python.org](https://www.python.org/downloads/)
   - During installation, make sure to check "Add Python to PATH"
2. No additional installation is required - the program is portable and can be run from any location
3. Run the `install_chocolatey_dependencies.bat` file as administrator to install all required dependencies:
   - This will install Chocolatey (Windows package manager) if it's not already installed
   - It will also install the `requests` and `packaging` Python packages needed for the Chocolatey API integration
   - Administrator privileges are required for Chocolatey installation
4. Alternatively, if you prefer to install the dependencies manually:
   - Install Chocolatey from https://chocolatey.org/install
   - Install Python packages using pip:
     ```
     pip install requests packaging
     ```


## Usage

1. **Starting the Application**:
   - Double-click the `run_update_scanner.bat` file to start the program
   - Alternatively, you can run the main Python script directly if you prefer
   - For testing or automation, you can run in test mode: `python "update scanner.py" --test`
     - Test mode runs without GUI and outputs results to `update_scanner_output.txt`
     - Useful for scripting or automated update checking

2. **Scanning for Updates**:
   - Click the "Scan for Updates" button to begin scanning your system
   - The scan may take several minutes depending on the number of installed applications

3. **Viewing Results**:
   - Results are displayed in three tabs:
     - **Software**: Shows all installed software and available updates
     - **Drivers**: Shows installed drivers and available updates
     - **Log**: Displays detailed logging information for troubleshooting

4. **Taking Action**:
   - Double-click on any item with an "Update Available" status to open the relevant update page or launcher
   - Items with "Up to Date" status require no action

5. **Saving Results**:
   - Use the "Save Report" button to export the scan results to a text file for future reference

## How It Works

The scanner uses several methods to detect installed software and drivers:

- **Software Detection**: 
  - Scans the Windows registry for installed applications
  - Checks common installation directories
  - Identifies application version information from executable metadata

- **Driver Detection**: 
  - Uses Windows Management Instrumentation (WMI) to query driver information
  - Uses PowerShell with ExecutionPolicy Bypass for maximum compatibility
  - Checks driver version against known latest versions

- **Update Checking**:
  - Uses the Chocolatey API to check for updates for popular Windows software
  - Only checks for updates for software that is actually installed on your PC
  - Properly URL-encodes package IDs to handle spaces and special characters
  - Provides direct links to the Chocolatey package pages for easy updating
  - Uses the GitHub API to check for updates for software with GitHub repositories
  - Maps installed software to known GitHub repositories for real-time update checking
  - Compares version numbers to determine if updates are available
  - For software without Chocolatey packages or GitHub repositories, uses a simulation approach for demonstration

## Troubleshooting

- **Program Won't Start**:
  - Ensure Python is correctly installed and added to your PATH
  - Try running the script directly from the command line to see any error messages

- **Missing Software**:
  - Some software might not be detected if installed in non-standard locations
  - Applications installed for the current user only might not be detected when running as administrator

- **False Positives**:
  - The update detection system may occasionally report false positives
  - Always verify with the software vendor's website before updating

- **Performance Issues**:
  - If scanning is slow, try closing other applications to free up system resources
  - Consider excluding certain directories if they contain many applications you don't need to track

- **PowerShell Execution Policy Issues**:
  - The scanner uses `-ExecutionPolicy Bypass` for PowerShell commands to ensure compatibility
  - If you encounter PowerShell-related errors, ensure your system allows script execution
  - You can manually set the execution policy: `Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process`

## FAQ

**Q: Does this program automatically update my software?**  
A: No, it only detects available updates. You must manually update each application.

**Q: Is an internet connection required?**  
A: Yes, to check for the latest versions of software and drivers.

**Q: Will this work with portable applications?**  
A: The scanner primarily detects installed applications. Portable apps may not be detected unless they're in standard locations.

**Q: How often should I run the scanner?**  
A: We recommend running it weekly to ensure your system stays up-to-date.

**Q: Does this replace Windows Update?**  
A: No, this complements Windows Update by checking for updates to third-party software that Windows Update doesn't cover.

## Future Enhancements

- Expand Chocolatey package mapping for more software applications
- Expand GitHub repository mapping for more software applications
- Implement real-time driver update checking APIs to replace simulated checks
- Add support for additional version control platforms (GitLab, Bitbucket, etc.)
- Add automatic update functionality where possible
- Improve detection of non-standard installations
- Add scheduling capabilities to run scans automatically
- Implement a silent mode for background operation
- Add export options in various formats (CSV, HTML, PDF)

## Contributing

Contributions are welcome! If you'd like to contribute to this project:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please ensure your code follows the project's coding standards and includes appropriate tests.



*Last updated: March 2025*
