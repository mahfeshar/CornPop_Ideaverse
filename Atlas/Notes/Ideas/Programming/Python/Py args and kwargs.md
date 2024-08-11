---
up:
  - "[[Py function]]"
related: 
created: 2024-04-28
tags: []
---
`*args` = allows you to pass multiple non-key arguments 
`**kwargs` = allows you to pass multiple keyword-arguments 
`*` unpacking operator from [[Packing and Unpacking]]


What’s `*args` and `**kwargs`?
- `*args` is a Tuple that contains all arguments
- `*kwargs` is a dictionary that contains all arguments by key/value

So, to make it clear, `*args` is the list of anonymous arguments, no name, just an order. `**kwargs` is the dictionary with all named arguments.

>[!info]
> Of course you can mix both, but the order should be first all anonymous arguments, and after named arguments.
### `*args`
- _[[Arbitrary Arguments]]_ are often shortened to `*args` in Python documentations.
- If you do not know how many arguments that will be passed into your function, add a `*` before the parameter name in the function definition.
- This way the function will receive a [[Py tuple]] of arguments, and can access the items accordingly:
```python
def add(*nums):
	total = 0
	for num in nums:
		total += num
	return total

print(add(1, 2, 3)) # 6

def dispaly_name(*args):
	for arg in args:
		print(arg, end=" ")

display_name("Dr.", "Spongebob", "Harold", "Squarepants", "III")
```
### `**kwargs`
- _Arbitrary Kword Arguments_ are often shortened to `**kwargs` in Python documentations.
- If you do not know how many keyword arguments that will be passed into your function, add two asterisk: `**` before the parameter name in the function definition.
- This way the function will receive a [[Py dictionary]] of arguments, and can access the items accordingly:
```python
def print_address(**kwargs):
	for value in kwargs.values():
		print(value, end=" ")

print_address(street="123 Fake St.", 
			  pobox="P.O Box 777", 
			  city="Detroit", 
			  state="MI", 
			  zip="54321")
```
### Exercise
```python
def shipping_label(*args, **kwargs):
	for arg in args:
		print(arg, end=" ")
	print()
	if "apt" in kwargs:
		print(f"{kwargs.get('street')} {kwargs.get('apt')}")
	elif "pobox" in kwargs:
		print(f"{kwargs.get('street')}")
		print(f"{kwargs.get('pobox')}")
	else:
		print(f"{kwargs.get('street')}")
	print(f"{kwargs.get('city')}, {kwargs.get('state')} {kwargs.get('zip')}")

shipping_label("Dr.", "Spongebob", "Squarepants",
			   street="123 Fake St.",
			   pobox="PO box #1001",
			   city="Detroit",
			   state="MI",
			   zip="54321")
```

```python
def my_fct(*args, **kwargs):
    print("{} - {}".format(args, kwargs))

my_fct() # () - {}
my_fct("Best") # ('Best',) - {}
my_fct("Best", 89) # ('Best', 89) - {}
my_fct(name="Best") # () - {'name': 'Best'}
my_fct(name="Best", number=89) # () - {'name': 'Best', 'number': 89}
my_fct("School", 12, name="Best", number=89) # ('School', 12) - {'name': 'Best', 'number': 89}
```
>[!tip]
>You can't use `**kwargs` before default arguments or `*args`

