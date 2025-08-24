# Assignment-6
# Module 10 & 11: CALCULATOR USING TKINTER

import tkinter as tk
from tkinter import messagebox

# Function to update expression
def press(num):
    global expression
    expression += str(num)
    equation.set(expression)

# Function to evaluate expression
def equalpress():
    try:
        global expression
        total = str(eval(expression))   # eval() evaluates the string expression
        equation.set(total)
        expression = total
    except Exception as e:
        messagebox.showerror("Error", "Invalid Input")
        equation.set("")
        expression = ""

# Function to clear the expression
def clear():
    global expression
    expression = ""
    equation.set("")

# main GUI window
root = tk.Tk()
root.title("Calculator")
root.geometry("350x400")
root.configure(bg="#282C34")

expression = ""
equation = tk.StringVar()

# Entry field
entry_field = tk.Entry(root, textvariable=equation, font=('Arial', 20), bd=10, insertwidth=2, width=14,
                       borderwidth=4, relief="ridge", justify="right")
entry_field.grid(row=0, column=0, columnspan=4, pady=10)

# Buttons
buttons = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
    ('0', 4, 0), ('.', 4, 1), ('=', 4, 2), ('+', 4, 3)
]

for (text, row, col) in buttons:
    if text == "=":
        tk.Button(root, text=text, padx=20, pady=20, bg="lightgreen", fg="black",
                  font=('Arial', 14), command=equalpress).grid(row=row, column=col, sticky="nsew")
    else:
        tk.Button(root, text=text, padx=20, pady=20, bg="lightgray", fg="black",
                  font=('Arial', 14), command=lambda t=text: press(t)).grid(row=row, column=col, sticky="nsew")

# Clear button
tk.Button(root, text="C", padx=20, pady=20, bg="tomato", fg="black", font=('Arial', 14),
          command=clear).grid(row=5, column=0, columnspan=4, sticky="nsew")

# Adjust grid
for i in range(6):
    root.rowconfigure(i, weight=1)
for j in range(4):
    root.columnconfigure(j, weight=1)

root.mainloop()
