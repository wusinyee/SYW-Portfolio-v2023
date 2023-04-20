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
The function first checks if the input list has 9 elements. If not, it raises a ValueError exception. If the input list has 9 elements, it converts the list to a 3x3 numpy array using the 'np.array()' function and 'reshape()'. Then it calculates the mean, variance, standard deviation, max, min, and sum along the rows, columns, and elements of the array using numpy functions. Finally, it creates a dictionary containing the calculated statistics in lists, and returns the dictionary.

Demonstration of the use of 'calculate()' function:
```python
print(calculate([0,1,2,3,4,5,6,7,8]))
```
The ouput:
```python
{
  'mean': [[3.0, 4.0, 5.0], [1.0, 4.0, 7.0], 4.0],
  'variance': [[6.0, 6.0, 6.0], [0.6666666666666666, 0.6666666666666666, 0.6666666666666666], 6.666666666666667],
  'standard deviation': [[2.449489742783178, 2.449489742783178, 2.449489742783178], [0.816496580927726, 0.816496580927726, 0.816496580927726], 2.581988897471611],
  'max': [[6, 7, 8], [2, 5, 8], 8],
  'min': [[0, 1, 2], [0, 3, 6], 0],
  'sum': [[9, 12, 15], [3, 12, 21], 36]
}
```
## Testing
Imported the tests from test_module.py to main.py for your convenience. The tests will run automatically whenever you hit the "run" button.
