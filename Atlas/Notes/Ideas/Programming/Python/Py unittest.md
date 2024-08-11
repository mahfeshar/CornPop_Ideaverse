---
up:
  - "[[Py Testing]]"
related: 
created: 2024-04-28
tags:
  - "#note/boat🚤"
  - "#note/develop🍃"
---

## Step by step
1. Make a file for testing the module
   We have two common convention for naming the test module:
	1. `/test_circles.py`
		All test modules will be grouped together.
	2. `/circles_test.py`
		each module appears next to its test class in  your file system
	![[Pasted image 20240217194116.png]]
2. We should import the module for `unittest` and the module that we want to test
   ```python
   import unittest
   import calc
   ```
3. Make a [[Py class]] for what we want to test and this class will [[Py Inheritance|inherent]] from `unittest.TestCase` class to have an access to testing capabilities in this class
   ```python
   class TestCalc(unittest.TestCase):
   ```
4. Make a function for every function that you want to test and use in it assert methods to test it
   You can name it with `test_funcName` 
   >[!error]
   >This is important because he only run this `test_function`
   
   ```python
   def test_add(self):
	   result = calc.add(10, 5)
	   self.assertEqual(result, 15)
	```
5. You can run your test module file from commend line 
   `python test_calc.py` but this will not give us any output so we run it with `unittest`
   `python -m unittest test_calc.py` you will get output now.
   To run it with your editor or with first commend we should use [[Py __name__ and __main__]]
   So add at the end of your test module this code:
   ```python
   if __name__ == '__main__':
	   unittest.main() # This will run all tests
	```
## Assert methods
| **Method**                                                                                                         | **Checks That**      |
| ------------------------------------------------------------------------------------------------------------------ | -------------------- |
| [assertEqual(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertEqual)                 | a == b               |
| assertNotEqual(a, b)                                                                                               | a != b               |
| assertTrue(x)                                                                                                      | bool(x) is True      |
| assertFalse(x)                                                                                                     | bool(x) is False     |
| [assertIs(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIs)                       | a is b               |
| [assertIsNot(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNot)                 | a is not b           |
| [assertIsNone(x)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsNone)                  | x is None            |
| assertIsNotNone(x)                                                                                                 | x is not None        |
| [assertIn(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIn)                       | a in b               |
| assertNotIn(a, b)                                                                                                  | a not in b           |
| [assertIsInstance(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertIsInstance)       | isinstance(a, b)     |
| [assertNotIsInstance(a, b)](https://docs.python.org/3/library/unittest.html#unittest.TestCase.assertNotIsInstance) | not isinstance(a, b) |
### Using help
```Shell
# Open python interactive mode
>>> import unittest
>>> help(unittest.TestCase.assertSetEqual)
```
## Errors
To Test errors we have to methods to do that:
1. We will use `assertRaises(ErrorType, function, values_pass_to_function)`
   ```python
   self.assertRaises(ValueError, calc.divide, 10, 0)
   ```
2. We use same method but with `with` and it's a preferred one 
   ```python
   with self.asserRaises(ValueError):
	   calc.divide(10, 0)
	```
## setUp and tearDown Classes
We can make a classes at the start of the code and use them to just don't repeat them a lot.
1. We can make them as [[Py Instance methods]] and it will be good if you will change data every test.
```python
def setUp(self):
	print('setUp')
	self.emp_1 = Employee('Corey', 'Schafer', 50000)
	self.emp_2 = Employee('Sue', 'Smith', 60000)

def tearDown(self):
	print('tearDown\n')
```
2. We can use them as [[Py Class methods]]
```python
@classmethod
def setUpClass(cls):
    print('setupClass')

@classmethod
def tearDownClass(cls):
    print('teardownClass')
```
## Example
### Ex 1
#### Code ex 1
```python
def add(x, y):
    """Add Function"""
    return x + y


def subtract(x, y):
    """Subtract Function"""
    return x - y


def multiply(x, y):
    """Multiply Function"""
    return x * y


def divide(x, y):
    """Divide Function"""
    if y == 0:
        raise ValueError('Can not divide by zero!')
    return x / y
```
#### Testing ex 1
```python
import unittest
import calc


class TestCalc(unittest.TestCase):

    def test_add(self):
        self.assertEqual(calc.add(10, 5), 15)
        self.assertEqual(calc.add(-1, 1), 0)
        self.assertEqual(calc.add(-1, -1), -2)

    def test_subtract(self):
        self.assertEqual(calc.subtract(10, 5), 5)
        self.assertEqual(calc.subtract(-1, 1), -2)
        self.assertEqual(calc.subtract(-1, -1), 0)

    def test_multiply(self):
        self.assertEqual(calc.multiply(10, 5), 50)
        self.assertEqual(calc.multiply(-1, 1), -1)
        self.assertEqual(calc.multiply(-1, -1), 1)

    def test_divide(self):
        self.assertEqual(calc.divide(10, 5), 2)
        self.assertEqual(calc.divide(-1, 1), -1)
        self.assertEqual(calc.divide(-1, -1), 1)
        self.assertEqual(calc.divide(5, 2), 2.5)

        with self.assertRaises(ValueError):
            calc.divide(10, 0)


if __name__ == '__main__':
    unittest.main()
```
### Ex 2
#### Code ex 2
```python
import requests


class Employee:
    """A sample Employee class"""

    raise_amt = 1.05

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    @property
    def email(self):
        return '{}.{}@email.com'.format(self.first, self.last)

    @property
    def fullname(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amt)

    def monthly_schedule(self, month):
        response = requests.get(f'http://company.com/{self.last}/{month}')
        if response.ok:
            return response.text
        else:
            return 'Bad Response!'
```
#### Testing ex 2
```python
import unittest
from unittest.mock import patch
from employee import Employee


class TestEmployee(unittest.TestCase):

    @classmethod
    def setUpClass(cls):
        print('setupClass')

    @classmethod
    def tearDownClass(cls):
        print('teardownClass')

    def setUp(self):
        print('setUp')
        self.emp_1 = Employee('Corey', 'Schafer', 50000)
        self.emp_2 = Employee('Sue', 'Smith', 60000)

    def tearDown(self):
        print('tearDown\n')

    def test_email(self):
        print('test_email')
        self.assertEqual(self.emp_1.email, 'Corey.Schafer@email.com')
        self.assertEqual(self.emp_2.email, 'Sue.Smith@email.com')

        self.emp_1.first = 'John'
        self.emp_2.first = 'Jane'

        self.assertEqual(self.emp_1.email, 'John.Schafer@email.com')
        self.assertEqual(self.emp_2.email, 'Jane.Smith@email.com')

    def test_fullname(self):
        print('test_fullname')
        self.assertEqual(self.emp_1.fullname, 'Corey Schafer')
        self.assertEqual(self.emp_2.fullname, 'Sue Smith')

        self.emp_1.first = 'John'
        self.emp_2.first = 'Jane'

        self.assertEqual(self.emp_1.fullname, 'John Schafer')
        self.assertEqual(self.emp_2.fullname, 'Jane Smith')

    def test_apply_raise(self):
        print('test_apply_raise')
        self.emp_1.apply_raise()
        self.emp_2.apply_raise()

        self.assertEqual(self.emp_1.pay, 52500)
        self.assertEqual(self.emp_2.pay, 63000)

    def test_monthly_schedule(self):
        with patch('employee.requests.get') as mocked_get:
            mocked_get.return_value.ok = True
            mocked_get.return_value.text = 'Success'

            schedule = self.emp_1.monthly_schedule('May')
            mocked_get.assert_called_with('http://company.com/Schafer/May')
            self.assertEqual(schedule, 'Success')

            mocked_get.return_value.ok = False

            schedule = self.emp_2.monthly_schedule('June')
            mocked_get.assert_called_with('http://company.com/Smith/June')
            self.assertEqual(schedule, 'Bad Response!')


if __name__ == '__main__':
    unittest.main()
```
## Materials
[Getting Started With Testing in Python – Real Python](https://realpython.com/python-testing/)
[unittest — Unit testing framework — Python 3.8.19 documentation](https://docs.python.org/3.8/library/unittest.html#module-unittest)