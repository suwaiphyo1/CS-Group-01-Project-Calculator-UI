# CS-Group-01-Project-Calculator-UI
import tkinter as tk
import math

def exit_ui():
    root.destroy()

def on_click(operation):
    try:
        num1 = float(entry_num1.get())
        num2 = float(entry_num2.get()) if operation in ('+', '-', '*', '/') else None

        if operation == '+': # if addition, we will add the first number to the sec
           result.set(num1 + num2) # and assign the resulting value to 
        elif operation == '-':
             result.set(num1 - num2)
        elif operation == '*':
             result.set(num1 * num2)
        elif operation == '/':
             result.set("Error!" if num2 == 0 else num1 / num2)
        elif operation == '^2':
             result.set(num1 ** 2)
        elif operation == 'sqrt':
             result.set("Error!" if num1 < 0 else math.sqrt(num1))

    except ValueError:
           result.set("Invalid Input")

def clear_entries():
    entry_num1.delete(0, tk.END)
    entry_num2.delete(0, tk.END)
    result.set("")
    
# GUI Setup
root = tk.Tk() # creating the object for the UI window
root.title("Calculator") # setting the window name (title)

# Labels and Entries
tk.Label(root, text="Enter Number 1:").grid(row=0, column=0)
entry_num1 = tk.Entry(root)
entry_num1.grid(row=0, column=1)

tk.Label(root, text="Enter Number 2:").grid(row=1, column=0)
entry_num2 = tk.Entry(root)
entry_num2.grid(row=1, column=1)

result = tk.StringVar()
tk.Label(root, text="Result:").grid(row=2, column=0)
tk.Entry(root, textvariable=result, state='readonly').grid(row=2, column=1)

# using lambda expressions for the basic operations
# defining the buttons for the operations
tk.Button(root, text="+", command=lambda: on_click('+')).grid(row=3, column=0)
tk.Button(root, text="-", command=lambda: on_click('-')).grid(row=3, column=1)
tk.Button(root, text="*", command=lambda: on_click('*')).grid(row=4, column=0)
tk.Button(root, text="/", command=lambda: on_click('/')).grid(row=4, column=1)
tk.Button(root, text="x^2", command=lambda: on_click('^2')).grid(row=5, column=0)
tk.Button(root, text="√x", command=lambda: on_click('sqrt')).grid(row=5, column=1)
tk.Button(root, text="Clear", command=clear_entries).grid(row=6, column=0, columnspan=2)
tk.Button(root, text="Exit", command=lambda: exit_ui()).grid(row=7, column=0, columnspan=2)

root.mainloop() # running the application main loop to run 
