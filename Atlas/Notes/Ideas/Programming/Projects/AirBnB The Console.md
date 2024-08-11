---
up:
  - "[[AirBnB clone]]"
related: 
created: 2024-05-15
tags:
  - note/develop🍃
---

### `basemodel`
- I created a `basemodel` class
- I checked first if we added [[Py args and kwargs#`**kwargs`|kwargs]]
	- If there is dictionary added as `kwargs` (from another object by method`to_dict`)
		- change string to datetime object by [[Py datetime#Datetime class Methods|strptime]] That's convert string to datetime object. (`updated_at`, `created_at`)
		- don't add `__class__` else add attributes to self by [[Py setattr]]
	- else (It's new)
		- Add id to it and time
		- add new instance(object) to storage 

- I made `save` method to update date and save it to storage by save storage

- `__str__` should print: `[<class name>] (<self.id>) <self.__dict__>`
	- I used for class name `type(self).__name__` or `self.__class__.__name__`

- I made `to_dict` to return dictionary representation of the `basemodel`
	- Dictionary that contain: (`__dict__`, `__class__`)
	- We should change type of `created_at` and `updated_at` from datetime to string
	- We will use for that [[Py datetime#Datetime class Methods|isoformat]]

- 
Later:
- We added a storage new function to make a new storage

### `FileStorage`
- We will serialize instances and deserialize it to JSON file [[Py json]]
- The `new` method that add new object to `__objects`
	- `Class_name.Class_id` = `object`
- I made `save` method save it to file
	- I saved `objects` at storage in new dictionary and made [[Py json#write to file|dump]]
- I made `reload` method that reads dictionary from file and save it to objects
	- Delete `__class__` key
	- Because of I have a lot of classes (`BaseModel`, User, State ..)
		- I made dictionary for it to pick the class with name (classes)
	- I read from JSON file by [[Py json#read from file|load]] and saved it to dictionary
	- I want to save this dictionary to objects so:
		- I retrieve at the dictionary for `json` load and use the key for it as key object
		- The value is also dictionary So will make new object with `__init__` at `BaseModel` and I will pass for it [[Py args and kwargs#`**kwargs`|kwargs]]
		- And I used dictionary that I made (classes) to know class that I will use to `init` and to know the class name, we will see the value dictionary's key (`__class`)
- At `_init__.py` at package models, I created a unique `FileStorage` instance for the application
	- It will reload all objects from `file.json` by using `reload()` method
- We used this storage to save objects at `BaseModel.save` 

### The console
- I used [[Py cmd]] to make it
	- I used prompt attribute to change prompt
	- I made 2 methods `do_quit` and `do_EOF` 
	- I used `emptyline` and override it to make  if I hit Enter with empty line not repeating the last command
	- I created `helo_` for every command
#### Console 0.1
I created some commands:
- Before I created the command, I noticed that all commands raise same errors, So I made [[Py Static methods]] called `command_check`
	- It takes line of arguments
	- I made [[Py partition]] for the line with `" "`
	- It will return [[Py tuple]] with 3 values (`class_name`,  `command_id` with attribute)
	- So we should partition it again 
	- And then make some checks
	- Then we make a key that is `BaseName.id` and check if it exist or not

- `create`: 