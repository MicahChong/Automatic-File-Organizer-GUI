import os
import shutil
import tkinter as tk
from tkinter import messagebox

# Directory and File Types
directorydesk = ""FOLDER DIRECTORY HERE" # Change these to your folder directory
directoryload = "FOLDER DIRECTORY HERE"
file_categories = {
    'Images': ['.jpg', '.jpeg', '.png', '.gif', '.bmp', '.tiff'],
    'Documents': ['.pdf', '.doc', '.docx', '.txt', '.xls', '.xlsx', '.ppt', '.pptx'],
    'Audio': ['.mp3', '.wav', '.aac', '.flac', '.ogg'],
    'Video': ['.mp4', '.mkv', '.avi', '.mov', '.wmv'],
    'Archives': ['.zip', '.rar', '.7z', '.tar', '.gz'],
    'Code': ['.py', '.html', '.css', '.js', '.cpp', '.java', '.php'],
    'Executables': ['.exe', '.bat', '.sh', '.app'],
    'Others': []
}

# Organize Function
def pineapple(directory):
    for filename in os.listdir(directory):
        filepath = os.path.join(directory, filename)
        if os.path.isdir(filepath):
            continue
        _, file_extension = os.path.splitext(filename)
        # Check which category the file belongs to
        folder_name = 'Others'  # Default to 'Others' if no match is found
        for category, extensions in file_categories.items():
            if file_extension.lower() in extensions:
                folder_name = category
                break
        # Create the folder if it doesn't exist
        folder_path = os.path.join(directory, folder_name)
        if not os.path.exists(folder_path):
            os.makedirs(folder_path)

        # Move the file to the appropriate folder
        shutil.move(filepath, os.path.join(folder_path, filename))

    messagebox.showinfo("Success", f'Files in {directory} have been organized.')

# Function Command for Desktop Button
def deskcleanbutton():
    pineapple(directorydesk)

# Function Command for Download Folder Button
def downloadcleanbutton():
    pineapple(directoryload)

# Create the main window
root = tk.Tk()
root.title("File Automatic Sorter")
root.geometry("350x100")

# Creation of Desktop Button
deskbutton = tk.Button(root, text="Desktop", command=deskcleanbutton)
deskbutton.pack(pady=10)

# Creation of Download Folder Button
downloadbutton = tk.Button(root, text="Download Folder", command=downloadcleanbutton)
downloadbutton.pack(pady=10)

# Window
root.mainloop()
