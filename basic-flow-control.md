# Basic Python syntax

----

In these slides, we will demonstrates some basic Python code snippets.

----

```python
# Defining variables

a = 1
```

----

```python
b = 2
c = a + b

print(c)
print(b - a)
```

----

```python
# Strings

name = "Python"
```

----

```python
# Concat string together
print("Hello " + name)
```

----

```python
# Format string
print("Hello {}".format(name))
```

----

```python
# F-String
print(f"Hello {name}")
```

----

```python
# Strings with 2+ variables

temperture = 28
weather = "sunny"
```

----

```python
# Concat strings together
print("It is " + weather + " today, " + str(temperture) + " Celsius degrees.")
```

----

```python
# Format string
print("It is {} today, {} Celsius degrees".format(weather, temperture))
```

----

```python
# F-String
print(f"It is {weather} today, {temperture} Celsius degrees")
```

----

```python
# F-String
print(f"What if I need to type {{}}? Make it double brackets: {{{{}}}}")
```

----

# Flow Control

----

^ Basic If statement

```python
score = 61

if score >= 60:
    print("Pass")
else:
    print("Fail")
```

----
^ Define function to re-use logic

```python
def is_student_pass(score):
    if score >= 60:
        return "Pass"
    else:
        return "Fail"
        
print(is_student_pass(59))
print(is_student_pass(62))
```

----

^ For-loop

```python
print("0-9")
for i in range(10):
    print(i)
```

----

```python
print("1-10")
for i in range(1,11):
    print(i)
```

----

```python
print("1,3,5,7,9")
for i in range(1,10,2):
    print(i)
```

----

```python
print("2,4,6,8,10")
for i in range(2,11,2):
    print(i)    
```

----

^ Looping List

```python
list = ["Apple", "Banana", "Cherry"]
for item in list:
    print(item)
```

----

^ Looping list of student scores

```python
list = [80, 59, 62, 70, 99, 40, 51]
for score in list:
    print("{}: {}".format(score, is_student_pass(score)) )
```
