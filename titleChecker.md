import os
import csv
import tkinter as tk
from tkinter import filedialog
from tkinter import messagebox
from PIL import Image, ImageTk

root = tk.Tk()
root.title("Image Renamer")

# Define variables for input fields
title_var = tk.StringVar()
vendor_var = tk.StringVar()
product_type_var = tk.StringVar()
option_name_var = tk.StringVar()
option_value_var = tk.StringVar()

# Define dictionary of image extensions and corresponding thumbnail sizes
image_ext_dict = {".jpg": (200, 200), ".jpeg": (200, 200), ".png": (150, 150)}

# Define function to rename file
def rename_file(old_name, new_name):
    try:
        os.rename(old_name, new_name)
    except:
        print(f"Could not rename file {old_name}")

# Define function to update preview panel with selected image
def update_preview():
    # Get selected image path from listbox
    try:
        image_path = image_paths_listbox.get(image_paths_listbox.curselection())
    except:
        error_label.config(text="Please select an image file.")
        return
    
    # Display image in preview panel
    try:
        img = Image.open(image_path)
        img.thumbnail((500, 500))
        img_tk = ImageTk.PhotoImage(img)
        preview_panel.config(image=img_tk)
        preview_panel.image = img_tk
        error_label.config(text="")
    except:
        error_label.config(text="Could not display image.")

# Define function to rename selected image
def rename_image():
    # Get input values
    title = title_var.get()
    vendor = vendor_var.get()
    product_type = product_type_var.get()
    option_name = option_name_var.get()
    option_value = option_value_var.get()
    
    # Get selected image path from listbox
    try:
        image_path = image_paths_listbox.get(image_paths_listbox.curselection())
    except:
        error_label.config(text="Please select an image file.")
        return
    
    # Determine file extension and create new filename
    file_ext = os.path.splitext(image_path)[1]
    new_name = f"{vendor}--{product_type}--{title}--{option_name}-{option_value}{file_ext}"
    
    # Rename file and update listbox and completed renaming listbox
    try:
        rename_file(image_path, os.path.join(image_folder, new_name))
        completed_renaming_listbox.insert(tk.END, new_name)
        image_paths_listbox.delete(image_paths_listbox.curselection())
        error_label.config(text="")
    except:
        error_label.config(text="Could not rename file.")
    
    # Update CSV file
    image_dict = {
        'Handle': '',
        'Title': title_var.get(),
        'Body (HTML)': '',
        'Vendor': vendor_var.get(),
        'Product Category': '',
        'Type': product_type_var.get(),
        'Tags': '',
        'Published': 'TRUE',
        'Option1 Name': option_name_var.get(),
        'Option1 Value': option_value_var.get(),
        'Option2 Name': '',
        'Option2 Value': '',
        'Option3 Name': '',
        'Option3 Value': '',
        'Variant SKU': '',
        'Variant Grams': '',
        'Variant Inventory Tracker': '',
        'Variant Inventory Qty': '',
        'Variant Inventory Policy': '',
        'Variant Fulfillment Service': '',
        'Variant Price': '',
        'Variant Compare At Price': '',
        'Variant Requires Shipping': '',
        'Variant Taxable': '',
        'Variant Barcode': '',
        'Image Src': '',
        'Image Position': '',
        'Image


import os
import csv
import tkinter as tk
from tkinter import filedialog
from PIL import Image, ImageTk

root = tk.Tk()
root.title("Image Renaming Application")

# Define variables
title_var = tk.StringVar()
vendor_var = tk.StringVar()
product_type_var = tk.StringVar()
option_name_var = tk.StringVar()
option_value_var = tk.StringVar()

# Define dropdown options
vendor_options = ['Vendor 1', 'Vendor 2', 'Vendor 3', 'Vendor 4']
product_type_options = ['Type 1', 'Type 2', 'Type 3', 'Type 4']
option_name_options = ['Option 1', 'Option 2', 'Option 3', 'Option 4']

# Define image preview panel
preview_panel = tk.Label(root, width=200, height=200)
preview_panel.grid(row=0, column=0, rowspan=10)

# Define input labels and fields
title_label = tk.Label(root, text="Title:")
title_entry = tk.Entry(root, textvariable=title_var, width=100)
title_label.grid(row=0, column=1, padx=5, pady=5)
title_entry.grid(row=0, column=2, padx=5, pady=5)

vendor_label = tk.Label(root, text="Vendor:")
vendor_dropdown = tk.OptionMenu(root, vendor_var, *vendor_options)
vendor_label.grid(row=1, column=1, padx=5, pady=5)
vendor_dropdown.grid(row=1, column=2, padx=5, pady=5)

product_type_label = tk.Label(root, text="Product Type:")
product_type_dropdown = tk.OptionMenu(root, product_type_var, *product_type_options)
product_type_label.grid(row=2, column=1, padx=5, pady=5)
product_type_dropdown.grid(row=2, column=2, padx=5, pady=5)

option_name_label = tk.Label(root, text="Option Name:")
option_name_dropdown = tk.OptionMenu(root, option_name_var, *option_name_options)
option_name_label.grid(row=3, column=1, padx=5, pady=5)
option_name_dropdown.grid(row=3, column=2, padx=5, pady=5)

option_value_label = tk.Label(root, text="Option Value:")
option_value_entry = tk.Entry(root, textvariable=option_value_var, width=50)
option_value_label.grid(row=4, column=1, padx=5, pady=5)
option_value_entry.grid(row=4, column=2, padx=5, pady=5)

# Define listbox to display image paths
image_paths_listbox = tk.Listbox(root, width=50, height=10)
image_paths_listbox.grid(row=5, column=3, padx=5, pady=5)

# Define label for error messages
error_label = tk.Label(root, fg='red')
error_label.grid(row=6, column=3, padx=5, pady=5)

# Define button to select image folder
def select_folder():
    # Open file dialog to select folder
    global image_folder
    image_folder = filedialog.askdirectory()
    
    # Get list of image files in folder
    image_files = [f for f in os.listdir(image_folder) if f.endswith('.jpg') or f.endswith('.jpeg') or f.endswith('.png')]
    
    # Display image file names in listbox
    image_paths_listbox.delete(0, tk.END)
    for f in image_files:
        image_paths_listbox.insert(tk.END, f)

select_folder_button = tk.Button(root

import os
import csv
import tkinter as tk
from tkinter import filedialog
from PIL import Image, ImageTk


# Define function to rename file
def rename_file(old_name, new_name):
    try:
        os.rename(old_name, new_name)
    except:
        print(f"Could not rename file {old_name}")


# Define function to update the preview panel
def update_preview():
    title = title_var.get()
    vendor = vendor_var.get()
    product_type = product_type_var.get()
    option_name = option_name_var.get()
    option_value = option_value_var.get()

    # Create file name
    file_name = f"{vendor}--{product_type}--{title}--{option_name}-{option_value}"
    file_name_preview.config(text=file_name)


# Define function to select folder
def select_folder():
    # Open file dialog to select folder
    folder_path = filedialog.askdirectory()

    # Get list of image files in folder
    image_files = os.listdir(folder_path)
    image_files = [file for file in image_files if file.endswith(('jpg', 'jpeg', 'png'))]

    # Update listbox with image file names
    image_paths_listbox.delete(0, tk.END)
    for file_name in image_files:
        image_paths_listbox.insert(tk.END, file_name)


# Define function to select image
def select_image():
    # Get selected image file name
    file_name = image_paths_listbox.get(image_paths_listbox.curselection())

    # Create file path
    file_path = os.path.join(image_folder, file_name)

    # Display image in preview panel
    img = Image.open(file_path)
    img.thumbnail((200, 200))
    img_tk = ImageTk.PhotoImage(img)
    image_panel.configure(image=img_tk)
    image_panel.image = img_tk

    # Update option values from file name
    parts = file_name.split('--')
    vendor_var.set(parts[0])
    product_type_var.set(parts[1])
    title_var.set(parts[2].split('.')[0])
    option_parts = parts[3].split('-')
    option_name_var.set(option_parts[0])
    option_value_var.set(option_parts[1])


# Define function to rename selected image
def rename_image():
    # Get input values
    title = title_var.get()
    vendor = vendor_var.get()
    product_type = product_type_var.get()
    option_name = option_name_var.get()
    option_value = option_value_var.get()

    # Create file name
    file_name = f"{vendor}--{product_type}--{title}--{option_name}-{option_value}"

    # Get selected image file name
    file_name_selected = image_paths_listbox.get(image_paths_listbox.curselection())

    # Create file paths
    old_path = os.path.join(image_folder, file_name_selected)
    new_path = os.path.join(image_folder, file_name)

    # Rename file
    rename_file(old_path, new_path)

    # Update completed renaming listbox
    completed_renaming_listbox.insert(tk.END, file_name_selected)

    # Remove selected image file name from image paths listbox
    image_paths_listbox.delete(image_paths_listbox.curselection())

    # Update preview panel
    update_preview()

    # Update CSV data
    row = [
        '',
        title_var.get(),
        '',
        vendor_var.get(),
        '',
        product_type_var.get(),
        '',
        'TRUE',
        option_name_var.get(),
        option_value_var.get(),
        '',
        '',
        '',
        '',
        '',
        '',
        '',
        '',
        '',
        '',
        '',
        '',

