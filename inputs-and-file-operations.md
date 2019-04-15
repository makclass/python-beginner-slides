# Taking inputs, Joining List, File Operations

Python Lecture 3

---- 

# Agenda

- Taking inputs
- Converting type
- While loop
- Joining list from string
- Splitting string into list
- File operations (Read, Append, Write)

---- 

# Taking Inputs

---- 

```python
name = input("What is your name? ")
print("Hello " + name)
```

---- 

The inputs are always string. We need to convert inputs into our data type.


---- 

# Convert type

- int(x)
- float(x)
- str(x)
- bool(x)
- list(x)


---- 

^ An example of taking input and convert it into integer.

```python
age = input("What is your age? ")

if int(age) >= 18:
    print("You can drink.")
else:
    print("Please don't drink.")

print("Good bye.")
```

---- 

# While-loop

---- 

# While loop

```python
x = 0
while x < 10:
    print(x)
    x += 1
```

---- 

# Comparing to for-loop

```python
for x in range(10):
    print(x)
```


---- 

# Take inputs until quit

```python
guests = []

while True:
    value = input("Please input a guest name, or 'q' to quit: ")
    if value == "q":
        break
    guests.append(value)

print(guests)
```

---- 

# Using while-loop

- When we don’t know where the loop end.
- Beware of infinite loop.

---- 

# Join and Split

---- 

# Join string together

We can join the list into string for better readable text.

```python
"glue".join(list)
```

---- 

```python
", ".join(guests)
```

---- 

# Join list together into string
```python
sample_list = ["Peter", "Tom", "Viena", "John"]
result = "The students are: {}".format( ", ".join(sample_list) )
print( result )
```

---- 

# Split string into list

```python
sample_string = "Peter, Tom, Viena, John"
result_list = sample_string.split(', ')
print( result_list )
```

---- 

# Split multiple lines

```python
sample_string = """This is a sample paragraph with multiple lines.
So that we can split the string by line endings.
Good for getting list from a plain text file with mutliple lines."""
result_list = sample_string.splitlines()
print(result_list)
```


---- 

# File Operations

---- 

# Reading Plain Text File with `readlines`

```python
with open("guests.txt", "r") as file_obj:
    result = file_obj.readlines()

print(result)
```

---- 

# Reading Plain Text File with `read` and `splitlines`

```python
with open("guests.txt", "r") as file_obj:
    result = file_obj.read().splitlines()

print(result)
```

---- 

# Appending to Existing File

```python
with open("guests2.txt", "a") as file_obj:
    file_obj.write("New Name Here\n")
```


---- 

# Writing to File

```python
with open("guests2.txt", "w") as file_obj:
    file_obj.write("New Name Here\n")
```


---- 

# Writing a list into file

```python
list = ["Susan", "Chris", "Anthony", "Joana"]
with open("guests2.txt", "a") as file_obj:        
    file_obj.writelines(list)
```

---- 

# Writing a list into file with line endings

```python
list = ["Susan", "Chris", "Anthony", "Joana"]
with open("guests3.txt", "a") as file_obj:        
    file_obj.write( "\n".join(list) )
```

---- 

# Guests Example: Write Result to File

```python
guests = []

while True:
    value = input("Please input a guest name, or 'q' to quit: ")
    if value == "q":
        break
    if len(value) > 0:
        guests.append(value)

with open(f"{list_name}.txt", "a") as file_obj:
    file_obj.write("\n".join(items))
    file_obj.write("\n")

print("List saved to guests.txt.")
```

---- 

# Guests Example: What if we let user choose where to save the list?

```python
list_name = input("Please enter a list name: ")
```

---- 

# Guests Example: Save to the given list name

```python
with open(f"{list_name}.txt", "a") as file_obj:
    file_obj.write("\n".join(items))
    file_obj.write("\n")

print(f"List saved to {list_name}.txt.")
```

---- 

# Further more: Divide logic into functions

```python
def ask_for_list_name():
    '''Ask the user for list name to save.'''
    list_name = input("Please enter a list name: ")
    return list_name

def get_list_items_input(list_name):
    '''Ask user to input a collection of list items until type 'q'.'''
    items = []
    while True:
        value = input(f"Please input an item for {list_name}, or 'q' to quit: ")
        if value == "q":
            break
        if len(value) > 0:
            items.append(value)
    return items

def save_list(list_name, items):
    '''Save the given items into list_name.txt.'''
    with open(f"{list_name}.txt", "a") as file_obj:
        file_obj.write("\n".join(items))
        file_obj.write("\n")

# Main Program Flow
list_name = ask_for_list_name()
items = get_list_items_input(list_name)
save_list(list_name, items)
print(f"List saved to {list_name}.txt.")
```

