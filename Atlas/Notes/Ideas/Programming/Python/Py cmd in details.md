- The `cmd` module contains one public class, `Cmd`
- It designed to be used as a base class for command processors such as interactive shells and other command interpreters.
## Processing Command
- The interpreter uses a loop to read all lines from its input, parse them, and then dispatch the command to an appropriate command handler.
- Input lines are parsed into two parts. The command, and any other text on the line.
- If the user enters a command `foo bar`, and your class includes a method named `do_foo()`, it is called with "bar" as the only argument.

```python
from cmd import Cmd

class HelloWorld(Cmd):
	"""Simple commadn processor example."""
	def do_greet(self, line):
		print("hello")
	def do_EOF(self, line):
		return True

if __name__ == '__main__':
	HelloWorld().cmdloop()
```
## Example
```python
from cmd import Cmd

class MyPrompt(Cmd):

    def do_hello(self, args):
        """Says hello. If you provide a name, it will greet you with it."""
        if len(args) == 0:
            name = 'stranger'
        else:
            name = args
        print("Hello, %s" % name)

    def do_quit(self, args):
        """Quits the program."""
        print("Quitting.")
        raise SystemExit


if __name__ == '__main__':
	prompt = MyPrompt() 
	# Make object from the class
	prompt.prompt = '> '
	prompt.cmdloop('First Line in CMD ...')
```
## Prompt
- We use `cmdloop` to make prompt appear always and we can add message appear when `cmd` start
- The prompt by default is (`Cmd`) but we can change it by changing the `prompt` attribute
```python
if __name__ == '__main__':
	prompt = MyPrompt() 
	# Make object from the class
	prompt.prompt = '> '
	prompt.cmdloop('First Line in CMD ...')

First Line in CMD ...
> 
```
## help
- The help command is built into Cmd.
- With no arguments, it shows the list of commands available.
- If you include a command you want help on, the output is more verbose and restricted to details of that command, when available.
```python
> help

Documented commands (type help <topic>):
========================================
hello  help  quit

# If the command not documented it will appear at Undocumented commands:

> help hello
Says hello. If you provide a name, it will greet you with it.
```

>[!fail]
> If your class does not include a specific command processor for a command, the method `default()` is called with the entire input line as an argument. The built-in implementation of `default()` reports an error.
## Live help
- To make help more formatted and make a help handler for the command we make `help_command()` method
```python
import cmd

class HelloWorld(cmd.Cmd):
    """Simple command processor example."""
    
    def do_greet(self, person):
        if person:
            print "hi,", person
        else:
            print 'hi'
    
    def help_greet(self):
        print '\n'.join([ 'greet [person]',
                           'Greet the named person',
                           ])
    
    def do_EOF(self, line):
        return True

if __name__ == '__main__':
    HelloWorld().cmdloop()
```
## EOF
- The end-of-file marker is dispatched to `do_EOF()`.
- If a command handler returns a true value, the program will exit cleanly. So to give a clean way to exit your interpreter, make sure to implement `do_EOF()` and have it return `True`. or use __`exit()`__
- Since `do_EOF()` returns True, typing Ctrl-D will drop us out of the interpreter.
- If we made EOF it will not print newline so we should add print before

`(Cmd) ^D$`
Notice that no newline is printed, so the results are a little messy.

```python
def do_EOF(self, line):
	print()
	exit()

def do_quit(self, args):
    """Quits the program."""
    print("Quitting.")
    raise SystemExit # return True or exit()

> quit
Quitting.
```
## Empty Line
- An empty line + `ENTER` shouldn’t execute anything

## Auto-Completion
- `Cmd` includes support for command completion based on the names of the commands with processor methods.
- The user triggers completion by hitting the tab key at an input prompt. 
- When multiple completions are possible, pressing tab twice prints a list of the options.
```python
$ python cmd_do_help.py
(Cmd) <tab><tab>
EOF    greet  help
(Cmd) h<tab>
(Cmd) help
```
- After we know the command, we can handle the argument completion by methods `complete_command`
- This allows you to assemble a list of possible completions using your own criteria (query a database, look at at a file or directory on the filesystem, etc.)

```python
import cmd

class HelloWorld(cmd.Cmd):
    """Simple command processor example."""
    
    FRIENDS = [ 'Alice', 'Adam', 'Barbara', 'Bob' ]
    
    def do_greet(self, person):
        "Greet the person"
        if person and person in self.FRIENDS:
            greeting = 'hi, %s!' % person
        elif person:
            greeting = "hello, " + person
        else:
            greeting = 'hello'
        print greeting
    
    def complete_greet(self, text, line, begidx, endidx):
        if not text:
            completions = self.FRIENDS[:]
        else:
            completions = [ f
                            for f in self.FRIENDS
                            if f.startswith(text)
                            ]
        return completions
    
    def do_EOF(self, line):
        return True

if __name__ == '__main__':
    HelloWorld().cmdloop()

$ python cmd_arg_completion.py
(Cmd) greet <tab><tab>
Adam     Alice    Barbara  Bob
(Cmd) greet A<tab><tab>
Adam   Alice
(Cmd) greet Ad<tab>
(Cmd) greet Adam
hi, Adam!
```
## Configuring `Cmd` Through Attributes

- In addition to the methods described above, there are several attributes for controlling command interpreters.

- `prompt` can be set to a string to be printed each time the user is asked for a new command.
- `intro` is the “welcome” message printed at the start of the program. `cmdloop()` takes an argument for this value, or you can set it on the class directly.
- When printing help, the `doc_header`, `misc_header`, `undoc_header`, and ruler attributes are used to format the output.

This example class shows a command processor to let the user control the prompt for the interactive session.
```python
import cmd

class HelloWorld(cmd.Cmd):
    """Simple command processor example."""

    prompt = 'prompt: '
    intro = "Simple command processor example."

    doc_header = 'doc_header'
    misc_header = 'misc_header'
    undoc_header = 'undoc_header'
    
    ruler = '-'
    
    def do_prompt(self, line):
        "Change the interactive prompt"
        self.prompt = line + ': '

    def do_EOF(self, line):
        return True

if __name__ == '__main__':
    HelloWorld().cmdloop()

$ python cmd_attributes.py
Simple command processor example.
prompt: prompt hello
hello: help

doc_header
----------
prompt

undoc_header
------------
EOF  help

hello
```

## Overriding Base Class Methods
- `Cmd` includes several methods that can be overridden as hooks for taking actions or altering the base class behaviour.
- This example is not exhaustive, but contains many of the methods commonly useful.
```python
import cmd

class Illustrate(cmd.Cmd):
    "Illustrate the base class method use."
    
    def cmdloop(self, intro=None):
        print 'cmdloop(%s)' % intro
        return cmd.Cmd.cmdloop(self, intro)
    
    def preloop(self):
        print 'preloop()'
    
    def postloop(self):
        print 'postloop()'
        
    def parseline(self, line):
        print 'parseline(%s) =>' % line,
        ret = cmd.Cmd.parseline(self, line)
        print ret
        return ret
    
    def onecmd(self, s):
        print 'onecmd(%s)' % s
        return cmd.Cmd.onecmd(self, s)

    def emptyline(self):
        print 'emptyline()'
        return cmd.Cmd.emptyline(self)
    
    def default(self, line):
        print 'default(%s)' % line
        return cmd.Cmd.default(self, line)
    
    def precmd(self, line):
        print 'precmd(%s)' % line
        return cmd.Cmd.precmd(self, line)
    
    def postcmd(self, stop, line):
        print 'postcmd(%s, %s)' % (stop, line)
        return cmd.Cmd.postcmd(self, stop, line)
    
    def do_greet(self, line):
        print 'hello,', line

    def do_EOF(self, line):
        "Exit"
        return True

if __name__ == '__main__':
    Illustrate().cmdloop('Illustrating the methods of cmd.Cmd')
```
- `cmdloop()` is the main processing loop of the interpreter. You can override it, but it is usually not necessary, since the `preloop()` and `postloop()` hooks are available.
- Each iteration through `cmdloop()` calls `onecmd()` to dispatch the command to its processor. The actual input line is parsed with `parseline()` to create a tuple containing the command, and the remaining portion of the line.
- If the line is empty, `emptyline()` is called. The default implementation runs the previous command again. If the line contains a command, first `precmd()` is called then the processor is looked up and invoked.
- If none is found, `default()` is called instead. Finally `postcmd()` is called.
```python
$ python cmd_illustrate_methods.py
cmdloop(Illustrating the methods of cmd.Cmd)
preloop()
Illustrating the methods of cmd.Cmd
(Cmd) greet Bob
precmd(greet Bob)
onecmd(greet Bob)
parseline(greet Bob) => ('greet', 'Bob', 'greet Bob')
hello, Bob
postcmd(None, greet Bob)
(Cmd) ^Dprecmd(EOF)
onecmd(EOF)
parseline(EOF) => ('EOF', '', 'EOF')
postcmd(True, EOF)
postloop()
```
## `Cmd` Attributes
- There are several attributes for controlling command interpreters.
- `prompt` can be set to a string to be printed each time the user is asked for a new command.
- `intro` is the “welcome” message printed at the start of the program.
  `cmdloop()` takes an argument for this value, or you can set it on the class directly.
- When printing help, the `doc_header`, `misc_header`, `undoc_header`, and `ruler` attributes are used to format the output.
```python
import cmd

class HelloWorld(cmd.Cmd):
    """Simple command processor example."""

    prompt = 'prompt: '
    intro = "Simple command processor example."

    doc_header = 'doc_header'
    misc_header = 'misc_header'
    undoc_header = 'undoc_header'
    
    ruler = '-'
    
    def do_prompt(self, line):
        "Change the interactive prompt"
        self.prompt = line + ': '

    def do_EOF(self, line):
        return True

if __name__ == '__main__':
    HelloWorld().cmdloop()


$ python cmd_attributes.py
Simple command processor example.
prompt: prompt hello
hello: help

doc_header
----------
prompt

undoc_header
------------
EOF  help

hello:
```
## Shelling out
- `Cmd` includes 2 special command prefixes.
- A question mark (?) is equivalent to the built-in help command, and can be used in the same way.
- An exclamation point (!) maps to `do_shell()`, and is intended for shelling out to run other commands, as in this example.

```python
import cmd
import os

class ShellEnabled(cmd.Cmd):
    
    last_output = ''

    
    def do_echo(self, line):
        "Print the input, replacing '$out' with the output of the last shell command"
        # Obviously not robust
        print line.replace('$out', self.last_output)
    
    def do_EOF(self, line):
        return True
    
if __name__ == '__main__':
    ShellEnabled().cmdloop()
```

```palintext
$ python cmd_do_shell.py
(Cmd) ?

Documented commands (type help ):
========================================
echo  shell

Undocumented commands:
======================
EOF  help

(Cmd) ? shell
Run a shell command
(Cmd) ? echo
Print the input, replacing '$out' with the output of the last shell command
(Cmd) shell pwd
running shell command: pwd
/Users/dhellmann/Documents/PyMOTW/in_progress/cmd

(Cmd) ! pwd
running shell command: pwd
/Users/dhellmann/Documents/PyMOTW/in_progress/cmd

(Cmd) echo $out
/Users/dhellmann/Documents/PyMOTW/in_progress/cmd

(Cmd)
```

## Alternative Inputs
- While the default mode for `Cmd()` is to interact with the user through the `readline` library, it is also possible to pass a series of commands in to standard input using standard Unix shell redirection.
- We need to use it at non-interactive mode
```shell
$ echo help | python cmd_do_help.py
(Cmd)
Documented commands (type help ):
========================================
greet

Undocumented commands:
======================
EOF  help

(Cmd)
```

>[!fail]
>We should have `do_EOF` in our program to end the loop after start it.


## Notes
>[!Note]
> Commands should have `arg`. Ex: `def do_quit(self, arg):`


## Resources
[cmd — Support for line-oriented command interpreters — Python 3.12.3 documentation](https://docs.python.org/3/library/cmd.html)
[cmd – Create line-oriented command processors - Python Module of the Week](https://pymotw.com/2/cmd/)
[cmd — Support for line-oriented command interpreters](https://docs.python.org/3.8/library/cmd.html)
[CmdModule - Python Wiki](https://wiki.python.org/moin/CmdModule)
[Give your Python program a shell with the cmd module (Example)](https://coderwall.com/p/w78iva/give-your-python-program-a-shell-with-the-cmd-module)