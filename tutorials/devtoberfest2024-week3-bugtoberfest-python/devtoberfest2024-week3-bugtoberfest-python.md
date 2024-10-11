---
auto_validation: true
time: 1
author_name: Vitaliy Rudnytskiy
author_profile: https://github.com/Sygyzmundovych
tags: [ tutorial>beginner, topic>cloud, topic>Python ]
primary_tag: topic>cloud
parser: v2
---

# 🟡 Devtoberfest 2024 - Fun Friday Week 3 - Bugtoberfest Python
<!-- description --> This is the Python Bug Hunt!

## You will learn
- How to have fun hunting for bugs in code.

## Prerequisites
- Basic to intermediate knowledge of Python 3.8 or later.


## Intro
As a part of Devtoberfest 2024 Fun Friday events, we have a bug hunt written in multiple languages for you to complete! The questions will range from easy to spot to a little more difficult, requiring some knowledge of the individual languages to complete. Each question will have 1 to 10 bugs and no bug should require running the code for the bug to appear.

Remember to have fun and enjoy the bug hunt. Happy hunting!

This tutorial is part of the Devtoberfest 2024, a celebration of and for Developers. For more information, see the [Devtoberfest Group](https://groups.community.sap.com/t5/devtoberfest/gh-p/Devtoberfest).

![Devtoberfest](promo-image-kasimir-square.png)

&nbsp;

For specifics on the Devtoberfest contest and the grand prize, see this [Devtoberfest 2024 Contest blog](https://community.sap.com/t5/devtoberfest-blog-posts/devtoberfest-2024-contest/ba-p/13781593)

&nbsp;

### Question 1 (Easy)

Find the number of bugs in the following code using Python 3.8 or later.

```python
def hello_world();
print "Hello, World!"

hello_world()
```

### Question 2 (Medium)

Find the bugs in the following code using Python 3.8 or later.

```python
from typing import Final

#Store integers 1, 2 and 3 in variables `ONE`, `TWO`, `THREE`
ONE, TWO, THREE = range(1, 3)
ZERO : Final = 0

def check_number (x : int) -> str:
    if x <= ONE:
        result='smaller than or equal to 1'
    elif x = TWO:
        result='equal to 2'
    then:
        result='equal to or greater than 3'

    returns result

a=input("Input the integer number: ")

print(f"{a} is {check_number(a)}")
```

### Question 3 (Hard)

Find the bugs in the following code using Python 3.8 or later.

```python
from dataclass import dataclass

class PointInTime:
    year : int
    month: int
    day  : int

point = PointInTime(1974, 12, 23)
print(point)  # Output should be: PointInTime(year=1974, month=12, day=23)
```
