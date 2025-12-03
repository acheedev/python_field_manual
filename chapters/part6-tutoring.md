[← Part 5 – Quality Layer](part5-quality-layer.md) · [Home](../README.md) · [Next → Part 7 – Script Cookbook](part7-script-cookbook.md)
---

# Part 6 – Tutoring Toolkit

## Core Teaching Rules

- Never talk more than ~2 minutes without letting the student type.
- Use age-appropriate metaphors.
- End every lesson by asking them to teach the concept back.

## Debugging Lessons

- Read the error message slowly.
- Use `print()` to inspect values.
- Use breakpoints in VS Code.

## Curriculum: Beginner → Intermediate → Advanced

Sketch a progression:

- Level 1: print, input, numbers, strings, lists, if, for, basic functions.
- Level 2: files, JSON/CSV, simple projects, functions, modules.
- Level 3: APIs, classes, virtualenvs, tests, small CLI tools.

## Teaching Projects

### Example first lesson

```python
# hello.py
print("Hello world!")

name = input("Your name: ")
print("Hello", name)

for i in range(5):
    print(i)

if name.lower() == "john":
    print("Awesome name!")
else:
    print("Nice to meet you.")
```

Then end with a small challenge like:  
“Ask for their favorite food and print a custom message about it.”
