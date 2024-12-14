#Final-Project
'''
Author: Rashan Wells
Date: 11/22/2024
Program: taskMate.py
'''

import tkinter as tk
from tkinter import Toplevel, messagebox
import json
import os
#Initialize
TASK_FILE = "tasks.json"

#Loading tasks from files
def loadTasks():
    if os.path.exists(TASK_FILE):
        try:
            with open(TASK_FILE, "r") as file:
                tasks = json.load(file)
                return tasks
        except Exception as e:
            messagebox.showerror("Error", f"Failed to load tasks: {e}")
    return []

#Saving tasks to files
def saveTasks(tasks):
    try:
        with open(TASK_FILE, "w") as file:
            json.dump(tasks, file)
    except Exception as e:
        messagebox.showerror("Error", f"Failed to save tasks: {e}")

#Adding tasks
def addTask(taskListBox, taskEntry):
    task = taskEntry.get().strip()
    if task:
        taskListBox.insert(tk.END, task)
        taskEntry.delete(0, tk.END)
        saveTasks(list(taskListBox.get(0, tk.END)))
    else:
        messagebox.showwarning("Input Error", "Task cannot be empty.")

#Deleting tasks
def deleteTask(taskListBox):
    try:
        selectedTask = taskListBox.curselection()[0]
        taskListBox.delete(selectedTask)
        saveTasks(list(taskListBox.get(0, tk.END)))
    except IndexError:
        messagebox.showwarning("Selection Error", "No task selected.")

#Marking tasks completed
def markCompletedTask(taskListBox):
    try:
        selectedTask = taskListBox.curselection()[0]
        task = taskListBox.get(selectedTask)
        if not task.startswith("!"):
            taskListBox.delete(selectedTask)
            taskListBox.insert(tk.END, f"!{task}")
            saveTasks(list(taskListBox.get(0, tk.END)))
        else:
            messagebox.showinfo("Info", "Task is already completed.")
    except IndexError:
        messagebox.showwarning("Selection Error", "No task selected.")

#Unmarking completed tasks incase of user error
def unmarkCompletedTask(taskListBox):
    try:
        selectedTask = taskListBox.curselection()[0]
        task = taskListBox.get(selectedTask)
        if task.startswith("!"):
            taskListBox.delete(selectedTask)
            taskListBox.insert(tk.END, task[2:])
            saveTasks(list(taskListBox.get(0, tk.END)))
        else:
            messagebox.showinfo("Info", "Task is not marked as completed.")
    except IndexError:
        messagebox.showwarning("Selection Error", "No task selected.")

#Opening the about window 
def openAboutWindow():
    aboutWindow = Toplevel()
    aboutWindow.title("About TaskMate")
    aboutWindow.geometry("300x200")
    
    aboutLabel = tk.Label(aboutWindow,text="TaskMate",font=("Arial", 16))
    aboutLabel.pack(pady=10)
    
    infoLabel = tk.Label(aboutWindow,text="A simple tool designed to help you manage your everyday tasks efficiently.",wraplength=250,justify="center")
    infoLabel.pack(pady=10)
    
    closeButton = tk.Button(aboutWindow,text="Close",command=aboutWindow.destroy)
    closeButton.pack(pady=10)

#Creating the main app window with buttons 
def mainWindow():
    app = tk.Tk()
    app.title("TaskMate")
    app.geometry("500x600")
    
    headerLabel = tk.Label(app, text="TaskMate", font=("Arial", 18), pady=10)
    headerLabel.pack()
    
    taskEntry = tk.Entry(app, width=40, font=("Arial", 14))
    taskEntry.pack(pady=10)
    
    buttonFrame = tk.Frame(app)
    buttonFrame.pack(pady=10)
    
    addButton = tk.Button(buttonFrame,text="Add Task",width=15,command=lambda: addTask(taskListBox, taskEntry))
    addButton.grid(row=0, column=0, padx=5)
    
    completeButton = tk.Button(buttonFrame,text="Mark Completed",width=15,command=lambda: markCompletedTask(taskListBox))
    completeButton.grid(row=0, column=1, padx=5)
    
    unmarkButton = tk.Button(buttonFrame, text="Unmark Completed", width=15, command=lambda: unmarkCompletedTask(taskListBox))
    unmarkButton.grid(row=1, column=0, padx=5, pady=5)
    
    deleteButton = tk.Button(buttonFrame, text="Delete Task", width=15, command=lambda: deleteTask(taskListBox))
    deleteButton.grid(row=1, column=1, padx=5, pady=5)
    
    taskListBox = tk.Listbox(app, width=50, height=15, font=("Arial", 12))
    taskListBox.pack(pady=10)
    
    footerFrame = tk.Frame(app)
    footerFrame.pack(pady=10)
    
    aboutButton = tk.Button(footerFrame, text="About", command=openAboutWindow)
    aboutButton.pack(side="left", padx=20)
    
    exitButton = tk.Button(footerFrame, text="Exit", command=app.quit)
    exitButton.pack(side="right", padx=20)
    
    tasks = loadTasks()
    for task in tasks:
        taskListBox.insert(tk.END, task)
    
    app.mainloop()

if __name__ == "__main__":
    mainWindow()


