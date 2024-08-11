---
up:
  - "[[Python MOC]]"
related: 
created: 2024-07-29
Link: https://docs.python.org/3/tutorial/stdlib.html#command-line-arguments
---
## argv
These arguments are stored in the [[Py sys]] module’s _argv_ attribute as a list.
```python
import sys
print(sys.argv)
```
Here is the output from running `python demo.py one two three` at the command line:
```python
['demo.py', 'one', 'two', 'three']
```
The number of elements of `argv` can be retrieved by using: `len(argv)`
## argparse
The [`argparse`](https://docs.python.org/3/library/argparse.html#module-argparse "argparse: Command-line option and argument parsing library.") module provides a more sophisticated متطور mechanism to process command line arguments. 
The following script extracts one or more filenames and an optional number of lines to be displayed:
```python
import argparse

parser = argparse.ArgumentParser(
								 prog='top',
								 description='Show top lines from each file'
)
parser.add_argument('filenames', nargs='+')
parser.add_argument('-l', '--lines', type=int, default=10)
args = parser.parse_args()
print(args)
```
When run at the command line with `python top.py --lines=5 alpha.txt beta.txt`, the script sets `args.lines` to `5` and `args.filenames` to `['alpha.txt', 'beta.txt']`.

## Examples
Write a program that prints the result of the addition of all arguments
```python
import sys
sumi = 0
for i in sys.argv:
	if i != sys.argv[0]:
		sumi += int(i)
print(sumi)
```