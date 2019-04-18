# Example: Diary Logging Program

Python Lecture 4

---- 

1. Ask for user input.
2. Determine today's date.
3. Write file from user input.
4. Display the last 3 lines of records.

---- 

We need the `datetime` module to get the current date.

```python
import datetime
```

---- 

We can get current date via `datetime`

```python
datetime.date.today()
```

---- 

Our target is to generate `YYYY-MM-DD`.

```python
str(datetime.date.today())
```

---- 

The string _representation_ of the date object is already what we need. It generates `YYYY-MM-DD`

---- 

# Where controls the string representation?

```python
str(datetime.date.today())
```

---- 

# `__repr__` method defines the string representation

```python
dir(datetime.date.today())
```

---- 

# Dunder Method

- `__repr__` is called special method or “dunder method”.
- **Double Underscore** method.

---- 

# List of Dunder Methods

![](https://makclass.com/system/class_notes/1354/original/36a0f5ad9da14c9e2c8138a76f3757c6c516d7d1/5C969AD7-023F-4839-B77E-0DB6ED3DBF6F.png?1544611351)

---- 

![](https://makclass.com/system/class_notes/1355/original/9c7bc7d37a9cc9c1c258a271ae81fd481ae651f7/46B314C3-BB6E-4533-BD80-78753F7240B9.png?1544611383)

---- 

# What if `__repr__` returns a different format sometimes in future?

---- 

In alternative, we can use the `isoformat` method:

```python
datetime.date.today().isoformat()
```

---- 

```python
def today():
    return datetime.date.today().isoformat()
```

---- 

We will use the file path in two places, read and write. So we better put them into a method.

```python
def diary_file_path():
    return 'diary.txt'
```

---- 

Furthermore, if we want to store the `diary.txt` file alongside the `.py` file, we can use the `__file__` method.

```python
def diary_file_path():
    script_dir = os.path.dirname(__file__)
    return os.path.join(script_dir, 'diary.txt')
```

---- 

The write file method opens the `diary.txt` file and append the given content to it.

```python
def write_file(content):
    with open(diary_file_path(), "a") as file_obj:
        file_obj.write(content + "\n")
```

---- 

The `read_last_entries()` read the file again and shows the last entries via `lines[-3:]` slicing.

```python
def read_last_entries():
    with open(diary_file_path(), "r") as file_obj:
        lines = file_obj.readlines()
        print("".join(lines[-3:]).rstrip())
```


---- 

Finally, we ask for input and 

```python
def ask_for_input():
    content = input("What do you want to say to Mr. Diary? ")
    if len(content) > 0:
        write_file(today() + ": " + content)
    read_last_entries()
```

---- 

# Further Challenges

---- 

1) For the `read_last_entries()`, assume now we want to dynamically set the number of lines we want to read. How to change the `read_last_entries` method?

---- 

2) What if we want to separate the diary files by date?

For example, we want to have a `diary-2019-04-15.txt` file for entries from 2019-04-15 and `diary-2019-04-16.txt` file for entries from 2019-04-16. How to do it?

---- 

# Writing .docx

---- 

# Installing Python-docx

We can install the `python-docx` module.

```bash
pip install python-docx
```

---- 

# How to choose which module to use?

1. Update frequency. (Last committed date)
2. How many people are using it. (Stars, blog posts)
3. Issues count, closed vs open ratio.
4. Documentation readability. (Do you understand what it does)

---- 

# Writing to DOCX

The write file method becomes:

```python
def write_file(content):
    if os.path.isfile(diary_file_path()):
        doc = docx.Document(diary_file_path())
    else:
        doc = docx.Document()
    doc.add_paragraph(content)
    doc.save(diary_file_path())
```

---- 

# Reading DOCX

```python
def read_last_entries():
    doc = docx.Document(diary_file_path())
    print("\n".join( map(lambda p: p.text, doc.paragraphs[-3:] )))
```

---- 

[Further examples on MakClass](https://makclass.com/classrooms/38/class_notes/1837)
