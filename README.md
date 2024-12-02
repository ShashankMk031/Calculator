﻿# Calculator
from tkinter import *
root = Tk()
root.title("Mobile Calculator")
expression = ""

def click(item):
    global expression
    expression += str(item)  # Append the clicked button's text to the expression
    equation.set(expression)  # Update the display with the current expression

def evaluate():
    global expression
    try:
        total = str(eval(expression))  # Evaluate the expression
        equation.set(total)            # Display the result
        expression = total             # Update expression to result for further calculations
    except Exception:
        equation.set("Error")          # Display error if evaluation fails
        expression = ""                # Reset expression on error

def clear():
    global expression
    expression = ""  # Reset the expression
    equation.set("") # Clear the display
    
equation = StringVar()
expression_field = Entry(root, textvariable=equation, width=20, font=('Arial', 16))
expression_field.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

number_buttons = [
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2),
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2),
    ('0', 4, 0)
]

for (text, row, col) in number_buttons:
    Button(root, text=text, padx=40, pady=20, font=('Arial', 14),
           command=lambda t=text: click(t)).grid(row=row, column=col)

operation_buttons = [
    ('+', 1, 3), ('-', 2, 3), ('*', 3, 3), ('/', 4, 3),
    ('=', 4, 2), ('Clear', 4, 1)
]

for (text, row, col) in operation_buttons:
    if text == '=':
        Button(root, text=text, padx=40, pady=20, font=('Arial', 14), command=evaluate).grid(row=row, column=col)
    elif text == 'Clear':
        Button(root, text=text, padx=29, pady=20, font=('Arial', 14), command=clear).grid(row=row, column=col)
    else:
        Button(root, text=text, padx=39, pady=20, font=('Arial', 14), command=lambda t=text: click(t)).grid(row=row, column=col)

root.mainloop()
