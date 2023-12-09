import tkinter as tk
from tkinter import ttk
import sqlite3
 
# Funktionen zum Anzeigen und Hinzufügen von Mitarbeitern
def show_employees():
    c.execute("SELECT * FROM employees")
    rows = c.fetchall()
    for row in rows:
        result_text.insert(tk.END, f"{row}\n")
 
def add_employee():
    id = employee_id_entry.get()
    name = employee_name_entry.get()
    lastname = employee_lastname_entry.get()
    email = employee_email_entry.get()
    hours = employee_hours_entry.get()
   
    c.execute("INSERT INTO employees VALUES (?, ?, ?, ?, ?)", (id, name, lastname, email, hours))
    conn.commit()
    result_text.insert(tk.END, "Employee added successfully\n")
 
# Funktionen zum Anzeigen und Hinzufügen von Projekten
def show_projects():
    c.execute("SELECT * FROM projects")
    rows = c.fetchall()
    for row in rows:
        result_text.insert(tk.END, f"{row}\n")
 
def add_project():
    id = project_id_entry.get()
    name = project_name_entry.get()
    startdate = project_startdate_entry.get()
    enddate = project_enddate_entry.get()
   
    c.execute("INSERT INTO projects VALUES (?, ?, ?, ?)", (id, name, startdate, enddate))
    conn.commit()
    result_text.insert(tk.END, "Project added successfully\n")
 
# Erstellen des Hauptfensters
root = tk.Tk()
root.title('Mitarbeiter- und Projektverwaltung')
root.geometry("800x600")
 
# Tabs für Mitarbeiter und Projekte
tab_control = ttk.Notebook(root)
 
employee_tab = ttk.Frame(tab_control)
project_tab = ttk.Frame(tab_control)
 
tab_control.add(employee_tab, text='Employees')
tab_control.add(project_tab, text='Projects')
 
tab_control.pack(expand=1, fill="both")
 
# Labels und Entry-Widgets für Mitarbeiter
employee_id_label = tk.Label(employee_tab, text="Employee ID:")
employee_id_label.grid(column=0, row=0, padx=10, pady=10)
employee_id_entry = tk.Entry(employee_tab)
employee_id_entry.grid(column=1, row=0, padx=10, pady=10)
 
employee_name_label = tk.Label(employee_tab, text="Name:")
employee_name_label.grid(column=0, row=1, padx=10, pady=10)
employee_name_entry = tk.Entry(employee_tab)
employee_name_entry.grid(column=1, row=1, padx=10, pady=10)
 
employee_lastname_label = tk.Label(employee_tab, text="Lastname:")
employee_lastname_label.grid(column=0, row=2, padx=10, pady=10)
employee_lastname_entry = tk.Entry(employee_tab)
employee_lastname_entry.grid(column=1, row=2, padx=10, pady=10)
 
employee_email_label = tk.Label(employee_tab, text="Email:")
employee_email_label.grid(column=0, row=3, padx=10, pady=10)
employee_email_entry = tk.Entry(employee_tab)
employee_email_entry.grid(column=1, row=3, padx=10, pady=10)
 
employee_hours_label = tk.Label(employee_tab, text="Hours:")
employee_hours_label.grid(column=0, row=4, padx=10, pady=10)
employee_hours_entry = tk.Entry(employee_tab)
employee_hours_entry.grid(column=1, row=4, padx=10, pady=10)
 
show_employees_button = tk.Button(employee_tab, text="Show Employees", command=show_employees)
show_employees_button.grid(column=0, row=5, columnspan=2, pady=10)
 
add_employee_button = tk.Button(employee_tab, text="Add Employee", command=add_employee)
add_employee_button.grid(column=0, row=6, columnspan=2, pady=10)
 
# Labels und Entry-Widgets für Projekte
project_id_label = tk.Label(project_tab, text="Project ID:")
project_id_label.grid(column=0, row=0, padx=10, pady=10)
project_id_entry = tk.Entry(project_tab)
project_id_entry.grid(column=1, row=0, padx=10, pady=10)
 
project_name_label = tk.Label(project_tab, text="Name:")
project_name_label.grid(column=0, row=1, padx=10, pady=10)
project_name_entry = tk.Entry(project_tab)
project_name_entry.grid(column=1, row=1, padx=10, pady=10)
 
project_startdate_label = tk.Label(project_tab, text="Start Date:")
project_startdate_label.grid(column=0, row=2, padx=10, pady=10)
project_startdate_entry = tk.Entry(project_tab)
project_startdate_entry.grid(column=1, row=2, padx=10, pady=10)
 
project_enddate_label = tk.Label(project_tab, text="End Date:")
project_enddate_label.grid(column=0, row=3, padx=10, pady=10)
project_enddate_entry = tk.Entry(project_tab)
project_enddate_entry.grid(column=1, row=3, padx=10, pady=10)
 
show_projects_button = tk.Button(project_tab, text="Show Projects", command=show_projects)
show_projects_button.grid(column=0, row=4, columnspan=2, pady=10)
 
add_project_button = tk.Button(project_tab, text="Add Project", command=add_project)
add_project_button.grid(column=0, row=5, columnspan=2, pady=10)
 
# Textfeld für Ergebnisse
result_text = tk.Text(root, height=10, width=50)
result_text.pack(padx=10, pady=10)
 
# Datenbankverbindung
conn = sqlite3.connect('database.db')
c = conn.cursor()
 
# Start des Tkinter Hauptloops
root.mainloop()
