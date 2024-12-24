# Calculator Code Documentation

This documentation provides a detailed explanation of the Python code for a graphical calculator application built using the `tkinter` library. Each section corresponds to a part of the code, explaining its functionality and design.

## Code Explanation

 1. Importing Required Librarpython
import tkinter as tk

- The `tkinter` library is imported to create the graphical user interface (GUI) for the calculator.

### 2. **Defining Styles and Colors**
```python
LARGE_FONT_STYLE = ("Arial", 40, "bold")
SMALL_FONT_STYLE = ("Arial", 16)
DIGITS_FONT_STYLE = ("Arial", 24, "bold")
DEFAULT_FONT_STYLE = ("Arial", 20)

OFF_WHITE = "#F8FAFF"
WHITE = "#FFFFFF"
LIGHT_BLUE = "#CCEDFF"
LIGHT_GRAY = "#F5F5F5"
LABEL_COLOR = "#25265E"
```
- Font styles and sizes are defined for different elements.
- Colors for buttons, labels, and backgrounds are set using hexadecimal color codes.

### 3. **Creating the Calculator Class**
```python
class Calculator:
    def __init__(self):
        self.window = tk.Tk()
        self.window.geometry("375x667")
        self.window.resizable(0, 0)
        self.window.title("Calculator")
```
- The `Calculator` class encapsulates all the logic and UI components of the calculator.
- A `Tk` instance is created as the main application window with a fixed size and title.

### 4. **Display Components**
#### a. **Display Frame**
```python
self.display_frame = self.create_display_frame()
```
- The display frame is a container for showing the current and total expressions.

#### b. **Display Labels**
```python
self.total_label, self.label = self.create_display_labels()
```
- Two labels are created:
  - `total_label`: Displays the cumulative expression.
  - `label`: Displays the current input or result.

### 5. **Digit and Operator Buttons**
#### a. **Digits**
```python
self.digits = {
    7: (1, 1), 8: (1, 2), 9: (1, 3),
    4: (2, 1), 5: (2, 2), 6: (2, 3),
    1: (3, 1), 2: (3, 2), 3: (3, 3),
    0: (4, 2), '.': (4, 1)
}
```
- A dictionary maps each digit to a grid position on the button frame.

#### b. **Operators**
```python
self.operations = {"/": "\u00F7", "*": "\u00D7", "-": "-", "+": "+"}
```
- Operators are mapped to their respective symbols for display.

### 6. **Creating Frames and Buttons**
#### a. **Buttons Frame**
```python
self.buttons_frame = self.create_buttons_frame()
```
- A frame to hold all buttons is created and configured for grid layout.

#### b. **Digit Buttons**
```python
self.create_digit_buttons()
```
- Buttons for digits (0-9 and `.`) are created with commands to update the current expression.

#### c. **Operator Buttons**
```python
self.create_operator_buttons()
```
- Buttons for operations (`+`, `-`, `*`, `/`) are created with commands to append operators.

#### d. **Special Buttons**
```python
self.create_special_buttons()
```
- Special buttons (`C`, `=`, `x²`, `√`) are added with specific functionality:
  - **Clear (`C`)**: Resets the expressions.
  - **Equals (`=`)**: Evaluates the total expression.
  - **Square (`x²`)**: Squares the current value.
  - **Square Root (`√`)**: Computes the square root of the current value.

### 7. **Binding Keyboard Input**
```python
self.bind_keys()
```
- Key bindings are added to allow user interaction via keyboard.

### 8. **Evaluation Logic**
```python
def evaluate(self):
    self.total_expression += self.current_expression
    self.update_total_label()
    try:
        self.current_expression = str(eval(self.total_expression))
        self.total_expression = ""
    except Exception as e:
        self.current_expression = "Error"
    finally:
        self.update_label()
```
- The `evaluate` method computes the result of the total expression using Python's `eval` function and handles exceptions for invalid inputs.

### 9. **Update Methods**
```python
def update_total_label(self):
    expression = self.total_expression
    for operator, symbol in self.operations.items():
        expression = expression.replace(operator, f' {symbol} ')
    self.total_label.config(text=expression)

def update_label(self):
    self.label.config(text=self.current_expression[:11])
```
- The `update_total_label` and `update_label` methods refresh the display to show the latest expressions.

### 10. **Run the Application**
```python
def run(self):
    self.window.mainloop()
```
- The `run` method starts the main event loop to display the GUI and handle user interactions.

### 11. **Entry Point**
```python
if __name__ == "__main__":
    calc = Calculator()
    calc.run()
```
- The `Calculator` object is instantiated, and the application is launched.

