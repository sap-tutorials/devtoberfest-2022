---
auto_validation: true
time: 20
author_name: Michelle Moudy
author_profile: https://github.com/MMoudy49
tags: [ tutorial>beginner, topic>cloud ]
primary_tag: topic>cloud
parser: v2
---

# 🟡 Devtoberfest 2024 - Fun Friday Week 3 - Bugtoberfest JavaScript
This is the JavaScript Bug Hunt!

## You will learn
- How to have fun hunting for bugs in code.

## Prerequisites
- Basic to intermediate knowledge of JavaScript.


## Intro
As a part of Devtoberfest 2024 Fun Friday events, we have a bug hunt written in multiple languages for you to complete! The questions will range from easy to spot to more difficult, requiring some knowledge of the individual languages to complete.

Each question will have 1 to 10 bugs and no bug should require running the code for the bug to appear. You're looking for unique errors, even if they are of the same type. Best practices do not count as bugs as the code will run regardless of how well the code is written.

For example, a misspelled variable may be referenced multiple times. Each misspelling should be counted as a separate bugs. The code below has three bugs, one for each misspelling regardless of the repeat in misspelling.

<pre lang="JavaScript">
  const test = 1;

  console.log(taste);
  console.log(tent);
  console.log(tent);
</pre>

However, if the bug is a syntax error, such as using the wrong separating character in an instantiation of an array, that should only be counted once unless it is done multiple times.

For example, there are two bugs in the code below. Of the three arrays in the code below, only one uses the correct separating character. There might be an inclination to count each incorrect separating character but instead you should assume there is just one bug per array instead of three.

<pre lang="JavaScript">
  const arrNoBug = ["", "", "", ""];
  const arrBug1 = ["". "". "". ""];
  const arrBug2 = [
    "";
    "";
    "";
    ""
  ];
</pre>


**A few helpful tips for counting errors:**
- if the error occurs on more than one line, there's a case to count it more than once. Ex. A variable is referenced with the same misspelling on two separate lines, that would be two bugs.
- If the error has to do with blocks of code, think about the types of errors in the block. Ex. a while loop may have a bug in the way the loop is created (using `[]` for the code block instead of `{}`) and has an incorrect condition for the loop (`while (1+1)`). These would be two bugs, even though the `()` surrounding the executed code occurs on two separate lines.
- Best practices should not be counted as bugs. If there is a better way to write the code, that is fine but should not be counted as a bug. For example, using a variable to store a return value in `if else` statements, then returning after, when no code outside of those `if else` statements needs to be run. The `if else` block could have the return statements within each of the `if else` blocks to reduce the need of the extra variable. This **would not be counted as a bug**.

[To learn more about JavaScript or for help on the bug hunts, the Mozilla web docs are a wonderful resource.](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

Remember to have fun and enjoy the bug hunt. Happy hunting!

This tutorial is part of the Devtoberfest 2024, a celebration of and for Developers. For more information, see the [Devtoberfest Group](https://groups.community.sap.com/t5/devtoberfest/gh-p/Devtoberfest).

![Devtoberfest](promo-image-kasimir-square.png)

&nbsp;

For specifics on the Devtoberfest contest and the grand prize, see this [Devtoberfest 2024 Contest blog](https://community.sap.com/t5/devtoberfest-blog-posts/devtoberfest-2024-contest/ba-p/13781593)

&nbsp;

### Question 1 (Easy)

**Find the bugs in the following code:**

```JavaScript
const bugFunc = (areThereBugs) -> {
  if (areThereBags) {
    console.log('Quick! Call an exterminator!);
  } else {
    console.log('Are you sure there aren't any bugs?');
  } else {
    console.log('No bugs here! Thank god.');
  }
}
```

**Hints**:

  - [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
  - [if else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
  - [Strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

### Question 2 (Medium)

**Find the bugs in the following code:**

```JavaScript
for (let i = 0: i < 5: i++) {
  console.log(looped {i} times);
}
```

**Hints**:

  - [Loops and iterations](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
  - [Strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

### Question 3 (Hard)

For the last JavaScript bug hunt, "bug" identification is the name of the game. What most people call bugs or insects are actually several different classifications of the phylum arthropods.

The goal of the function in this bug hunt is to take in an object of an unidentified "bug" and determine if it is a part of the class Insecta or Arachnids, and if Insecta, further identify if it is a true bug in the order Hemiptera. To make things simple, **the function should return one of the three values, "Arachnid", "Insect", or "True Bug".**

Please note that some of this data might not technically be correct, entomology wise. For example, there are some arachnids with less than 8 legs. This does not count as a bug. To simplify things, **the objects below are going to be used as the source of truth for arthropod classification**. They should be used to determine if the function `isArachnidInsectOrBug` will return the correct output.

**Arachnid**
```JSON
{
    antennae: false,
    wingPairs: false,
    bodySegments: 2,
    legs: 8
}
```

**Insect**
```JSON
{
    antennae: true,
    wingPairs: [0, 2],
    mouthType: [
      "sponging",
      "siphoning",
      "chewing",
      "piercing/sucking flexible",
      "piercing/sucking rigid"
    ],
    bodySegments: 3,
    legs: 6
}
```

**True Bug**
```JSON
{
    antennae: true,
    wingPairs: [0, 2],
    mouthType: "piercing/sucking rigid",
    bodySegments: 3,
    legs: 6
}
```

**Hint**: _Keep these classification objects in mind when looking at the functions in the bug hunt._

Below are examples of potential input to the function `IsArachnidInsectOrBug`. In order to determine what is what, they need to match the values in the classification objects above. Keep in mind that all true bugs are insects but not all insects are true bugs and arachnids are neither. No coding bugs will be about the data itself being wrong.

**Assume only one value in the classification object parameters with arrays will be chosen for the input object**. For example, in Insect, `wingPairs` would equal either `0` or `2`, not `[0]` or `[0, 2]`. You can see this in input example 2.

Example of what could be sent into the function and expected output:

**Arthropod Input Example 1**
```JSON
{
    antennae: false,
    wingPairs : false,
    bodySegments: 2,
    legs: 8

}
```
*Expected Output: "Arachnid"*

**Arthropod Input Example 2**
```JSON
{
    antennae: false,
    wingPairs : false,
    mouthType: "piercing/sucking flexible",
    bodySegments: 3,
    legs: 6

}
```
*Expected Output: "Insect"*

Remember, **best practices is not a justification for a bug**. If the code will run and output the expected result, it does not count as a bug. Also keep in mind that the point is to count the bugs, not how to fix the bugs. One fix might take care of several bugs but should not be counted as only one bug.

These are complex bugs so look carefully.

**Find the bugs in the following code:**
```JavaScript
function isArachnidInsectOrBug (arthropod) {
    let bugType = isInsectOrBug(arthropod);

    if (!bugType) {
        return isArachnid(arthropod);
    }
}

function isInsectOrBug(arthropod) {
    let bugType = "";
    switch (arthropod.mouthType) {
        case "sponging":
        case "siphoning":
        case "chewing":
        case "piercing/sucking flexible": {
            bugType = "Insect";
        }
        case "piercing/sucking rigid": {
            bugType = "True Bug";
        }
    }
}

function isArachnid ({antennae, wingPairs, bodySegments, legs}) {
    if (!antennae || !wingPairs || bodySegments === 2 || legs === 8) {
        return true;
    }
}
```

**Hints**:

  - [if else](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)
  - [Expressions and Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_operators)
  - [Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer)
  - [Object Destructuring in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#object_destructuring)
  - [Switch statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)