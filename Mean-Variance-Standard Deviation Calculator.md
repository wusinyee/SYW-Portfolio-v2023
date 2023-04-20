## Mean-Variance-Standard Deviation Calculator (Data Analysis with Python Project)

Project Propoasl: TBC

Using the 'calculate()' function:
```python
import numpy as np

def calculate(lst):
    if len(lst) != 9:
        raise ValueError("List must contain nine numbers.")

    arr = np.array(lst).reshape(3, 3)

    calculations = {
        'mean': [list(np.mean(arr, axis=0)), list(np.mean(arr, axis=1)), np.mean(arr)],
        'variance': [list(np.var(arr, axis=0)), list(np.var(arr, axis=1)), np.var(arr)],
        'standard deviation': [list(np.std(arr, axis=0)), list(np.std(arr, axis=1)), np.std(arr)],
        'max': [list(np.max(arr, axis=0)), list(np.max(arr, axis=1)), np.max(arr)],
        'min': [list(np.min(arr, axis=0)), list(np.min(arr, axis=1)), np.min(arr)],
        'sum': [list(np.sum(arr, axis=0)), list(np.sum(arr, axis=1)), np.sum(arr)]
    }

    return calculations

```
The 'calculate' function takes a list of nine numbers and returns a dictionary containing various statistical calculations of those numbers.
The function checks whether the input list has exactly 9 numbers. If not, it raises an error message. Next, the function converts the list into a 3x3 array and uses various NumPy functions to calculate different statistics, such as mean, variance, standard deviation, maximum, minimum, and sum of the numbers. The function then returns a dictionary with the name of these statistical calculations as the keys and the calculated values as the corresponding values. 

## Testing
Imported the tests from test_module.py to main.py for your convenience. The tests will run automatically whenever you hit the "run" button.
