import tkinter as tk  # Импортируем библиотеку для графического интерфейса

def button_click(symbol):
    entry.insert(tk.END, symbol)  # Вставляем символ в поле ввода

def clear_entry():
    entry.delete(0, tk.END)  # Удаляем всё из поля ввода

def calculate():
    try:
        result = eval(entry.get())  # Вычисляем выражение из поля
        entry.delete(0, tk.END)     # Очищаем поле
        entry.insert(tk.END, str(result))  # Вставляем результат
    except Exception:
        entry.delete(0, tk.END)
        entry.insert(tk.END, "Ошибка")

# Создаём главное окно
window = tk.Tk()
window.title("Калькулятор")  # Заголовок окна

# Создаём поле ввода
entry = tk.Entry(window, font=("Arial", 24), justify="right")
entry.grid(row=0, column=0, columnspan=4, sticky="nsew")  # Расположение

# Кнопки калькулятора
buttons = [
    "7", "8", "9", "/",
    "4", "5", "6", "*",
    "1", "2", "3", "-",
    "0", "C", "=", "+"
]

# Создаём и размещаем кнопки
row = 1
col = 0
for char in buttons:
    if char == "=":
        btn = tk.Button(window, text=char, font=("Arial", 18), command=calculate)
    elif char == "C":
        btn = tk.Button(window, text=char, font=("Arial", 18), command=clear_entry)
    else:
        btn = tk.Button(window, text=char, font=("Arial", 18),
                        command=lambda ch=char: button_click(ch))
    
    btn.grid(row=row, column=col, sticky="nsew")

    col += 1
    if col > 3:
        col = 0
        row += 1

# Расширяемость колонок и строк
for i in range(4):
    window.grid_columnconfigure(i, weight=1)
for i in range(5):
    window.grid_rowconfigure(i, weight=1)

window.mainloop()  # Запускаем приложение
