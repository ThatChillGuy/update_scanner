import os
import tkinter as tk
from tkinter import ttk, messagebox
import requests
import winreg
import wmi

# GitHub API to check for updates
GITHUB_REPOS = {
    "VLC media player": "videolan/vlc",
    "Notepad++": "notepad-plus-plus/notepad-plus-plus"
}

def get_installed_software():
    software = []
    reg_path = r"SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall"
    try:
        with winreg.OpenKey(winreg.HKEY_LOCAL_MACHINE, reg_path) as key:
            for i in range(0, winreg.QueryInfoKey(key)[0]):
                subkey_name = winreg.EnumKey(key, i)
                with winreg.OpenKey(key, subkey_name) as subkey:
                    try:
                        name = winreg.QueryValueEx(subkey, "DisplayName")[0]
                        version = winreg.QueryValueEx(subkey, "DisplayVersion")[0]
                        software.append({"name": name, "version": version})
                    except FileNotFoundError:
                        continue
    except Exception as e:
        messagebox.showerror("Error", f"Error fetching software: {e}")
    return software

def check_github_updates(software):
    results = []
    for app in software:
        repo = GITHUB_REPOS.get(app["name"])
        if repo:
            try:
                response = requests.get(f"https://api.github.com/repos/{repo}/releases/latest")
                latest_version = response.json().get("tag_name", "Unknown")
                if latest_version != app["version"]:
                    results.append({"name": app["name"], "status": "Update Available"})
                else:
                    results.append({"name": app["name"], "status": "Up to Date"})
            except Exception:
                results.append({"name": app["name"], "status": "Error Checking"})
    return results

def display_results():
    software = get_installed_software()
    results = check_github_updates(software)
    for result in results:
        tree.insert("", "end", values=(result["name"], result["status"]))

def save_report():
    with open("update_report.txt", "w") as file:
        for child in tree.get_children():
            file.write(f"{tree.item(child, 'values')}\n")
    messagebox.showinfo("Success", "Report saved successfully.")

# GUI Setup
root = tk.Tk()
root.title("Windows Update Scanner")

frame = ttk.Frame(root)
frame.pack(padx=20, pady=20, fill="both", expand=True)

tree = ttk.Treeview(frame, columns=("Software", "Status"), show="headings")
tree.heading("Software", text="Software")
tree.heading("Status", text="Status")
tree.pack(fill="both", expand=True)

btn_frame = ttk.Frame(root)
btn_frame.pack(pady=10)

scan_btn = ttk.Button(btn_frame, text="Scan for Updates", command=display_results)
scan_btn.grid(row=0, column=0, padx=5)

save_btn = ttk.Button(btn_frame, text="Save Report", command=save_report)
save_btn.grid(row=0, column=1, padx=5)

root.mainloop()
