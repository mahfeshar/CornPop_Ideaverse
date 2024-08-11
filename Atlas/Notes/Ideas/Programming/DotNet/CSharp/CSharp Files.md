---
up:
  - "[[CSharp MOC]]"
related: 
created: 2024-07-07
---
- هنستخدم namespace اسمها `System.IO`
```cs
using System.IO;  // include the System.IO namespace

File.SomeFileMethod();  // use the file class with methods
```

| Method           | Description                                                                                           |
| ---------------- | ----------------------------------------------------------------------------------------------------- |
| `AppendText()`   | Appends text at the end of an existing file                                                           |
| `Copy()`         | Copies a file                                                                                         |
| `Create()`       | Creates or overwrites a file                                                                          |
| `Delete()`       | Deletes a file                                                                                        |
| `Exists()`       | Tests whether the file exists                                                                         |
| `ReadAllText()`  | Reads the contents of a file                                                                          |
| `Replace()`      | Replaces the contents of a file with the contents of another file                                     |
| `WriteAllText()` | Creates a new file and writes the contents to it. If the file already exists, it will be overwritten. |

## Write To a File and Read It

```cs
using System.IO;  // include the System.IO namespace

string writeText = "Hello World!";  
// Create a text string
File.WriteAllText("filename.txt", writeText);  
// Create a file and write the content of writeText to it

string readText = File.ReadAllText("filename.txt");  
// Read the contents of the file
Console.WriteLine(readText);  // Output the content
```