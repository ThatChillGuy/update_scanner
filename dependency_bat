@echo off
echo ===================================================
echo Installing dependencies for Update Scanner...
echo ===================================================

:: Check if Python is installed
python --version > nul 2>&1
if %errorlevel% neq 0 (
    echo Error: Python is not installed or not in PATH.
    echo Please install Python from https://www.python.org/downloads/
    echo Make sure to check "Add Python to PATH" during installation.
    pause
    exit /b 1
)

echo Python is installed. Installing required packages...

:: Install required packages
echo Installing requests package...
python -m pip install requests

echo Installing packaging package...
python -m pip install packaging

echo ===================================================
echo Dependencies installation completed!
echo ===================================================
echo The following packages were installed:
echo - requests (for HTTP requests)
echo - packaging (for version comparison)
echo.
echo You can now run the Update Scanner using run_update_scanner.bat
echo ===================================================
pause
