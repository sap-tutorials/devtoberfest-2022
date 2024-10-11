---
auto_validation: true
time: 1
author_name: DJ Adams
author_profile: https://github.com/qmacro
tags: [ tutorial>beginner, topic>cloud ]
primary_tag: topic>cloud
parser: v2
---

# 🟡 Devtoberfest 2024 - Fun Friday Week 3 - Bugtoberfest jq
<!-- description --> This is the jq Bug Hunt!

## You will learn
- How to have fun hunting for bugs in code.

## Prerequisites
- Basic to intermediate knowledge of jq.


## Intro
As a part of Devtoberfest 2024 Fun Friday events, we have a bug hunt written in multiple languages for you to complete! The questions will range from easy to spot to a little more difficult, requiring some knowledge of the individual languages to complete. This particular bug hunt, focuses on the [jq language](https://jqlang.github.io/jq/).

Each of the questions will be based on some small jq scripts (also known as filters) that work on the same data set.

That data set is product data and exists as a single JSON file [products.json](https://github.com/qmacro/teched-jq-talk/blob/main/products.json). You may recognize the products as being from the classic Northwind data model, and the file was [put together](https://github.com/qmacro/teched-jq-talk/tree/main?tab=readme-ov-file#appendix) from multiple JSON files used in [the material for a talk on jq](https://github.com/qmacro/teched-jq-talk) that you may find helpful, or at least interesting.

While working through the questions, it's best to also look at [the data set contents](https://github.com/qmacro/teched-jq-talk/blob/main/products.json).

Remember to have fun and enjoy the bug hunt. Happy hunting!

This tutorial is part of the Devtoberfest 2024, a celebration of and for Developers. For more information, see the [Devtoberfest Group](https://groups.community.sap.com/t5/devtoberfest/gh-p/Devtoberfest).

![Devtoberfest](promo-image-kasimir-square.png)

&nbsp;

For specifics on the Devtoberfest contest and the grand prize, see this [Devtoberfest 2024 Contest blog](https://community.sap.com/t5/devtoberfest-blog-posts/devtoberfest-2024-contest/ba-p/13781593)

&nbsp;

### Question 1 (Easy)

We want a simple list of products and the categories they're in. The output should look like this:

```text
Chai is in the Beverages category
Chang is in the Beverages category
Aniseed Syrup is in the Condiments category
Chef Anton's Cajun Seasoning is in the Condiments category
...
```

The invocation of the jq script (including bugs) to produce this looks like this:

```shell
jq --raw \
  '.()|"(.ProductName) is in the \(Category.CategoryName) category" \
  products.json
```

and on its own, with extra whitespace, the (buggy) jq filter looks like this:

```jq
.()
| "(.ProductName) is in the \(Category.CategoryName) category"
```

<!--

Bugs (3 total)

- the array iterator is [] not () (https://jqlang.github.io/jq/manual/#array-object-value-iterator)
- the string interpolation construct is \( ... ) so there's a backslash missing in the first instance (https://jqlang.github.io/jq/manual/#string-interpolation)
- in the second instance of an expression being inserted into the string, the identity filter . is missing - it should be .Category.CategoryName (https://jqlang.github.io/jq/manual/#identity)

The correct filter should be:

.[]|"\(.ProductName) is in the \(.Category.CategoryName) category"

-->

### Question 2 (Medium)

We want to know how many products are still being sold, i.e. not discontinued. The answer should be a simple numeric value, like this (8 of the 77 total products in this data set are discontinued, so the value here is correct):

```text
69
```

The invocation of the jq script (including bugs) to produce this looks like this:

```shell
jq --raw \
  'select(.Discontinued)|length' \
  products.json
```

and on its own, with extra whitespace, the (buggy) jq filter looks like this:

```jq
select(.Discontinued)
| length
```

<!--

Bugs (2 total)

- the outermost element is an array, so we must use map to iterate over and call select (https://jqlang.github.io/jq/manual/#map-map_values)
- we're after a count of the products that are not discontinued, so we need to negate the boolean expression inside the select (https://jqlang.github.io/jq/manual/#select)

The correct filter should be:

map(select(.Discontinued|not))|length

-->

### Question 3 (Hard)

We want a summary of categories with the total number of units of stock for each of those categories. The output should look like this:

```json
{
  "Beverages": 559,
  "Condiments": 507,
  "Confections": 386,
  "Dairy Products": 393,
  "Grains/Cereals": 308,
  "Meat/Poultry": 165,
  "Produce": 100,
  "Seafood": 701
}
```

The invocation of the jq script (including bugs) to produce this looks like this:

```shell
jq --raw \
  'group(.Category.CategoryID)|map({first|Category.CategoryName:map(.UnitsInStock)|+})|sum' \
  products.json
```

and on its own, with extra whitespace, the (buggy) jq filter looks like this:

```jq
group(.Category.CategoryID)
| map({
    first|Category.CategoryName:
    map(.UnitsInStock)
    | +
  })
| sum
```

<!--

Bugs (4 total)

- the group function, which takes a path expression, is group_by, not group (https://jqlang.github.io/jq/manual/#group_by)
- while first, which is just syntactic sugar for .[0] (https://github.com/jqlang/jq/blob/master/src/builtin.jq#L177) can be followed by a pipe, it can also be followed directly by the identity filter, which is missing here (should be first.Category.CategoryName, or first|.Category.CategoryName but not first|Category.CategoryName) (https://jqlang.github.io/jq/manual/#first-last-nth-1)
- to use an expression as a key in a property literal, you need to wrap it in parentheses, i.e. {(first.Category.CategoryName): ... } not {first.Category.CategoryName: ...}
- while + is valid in jq (it's an operator), it's not valid in the position it is here; the add filter is needed to add values in an array (https://jqlang.github.io/jq/manual/#add)
- sum is not a valid filter in jq, it's add

The correct filter should be:

group_by(.Category.CategoryID)
| map({
    (first.Category.CategoryName):
    map(.UnitsInStock)
    | add
  })
| add

-->

## Reading material

For reading around jq, we have some pointers for you. In general:

- [jq posts on qmacro.org](https://qmacro.org/tags/jq/)
- [Material for the SAP TechEd talk "Handle jq like a boss"](https://github.com/qmacro/teched-jq-talk)

Directly related to this bug hunt, here are some links to specific components of the jq language that you may find useful:

- [the array / object value iterator](https://jqlang.github.io/jq/manual/#array-object-value-iterator)
- [string interpolation](https://jqlang.github.io/jq/manual/#string-interpolation)
- [the identity filter](https://jqlang.github.io/jq/manual/#identity)
- [map](https://jqlang.github.io/jq/manual/#map-map_values)
- [select](https://jqlang.github.io/jq/manual/#select)
- [group_by](https://jqlang.github.io/jq/manual/#group_by)
- [first](https://jqlang.github.io/jq/manual/#first-last-nth-1) ([just syntactic sugar for .[0]](https://github.com/jqlang/jq/blob/master/src/builtin.jq#L177))
- [the addition operator](https://jqlang.github.io/jq/manual/#addition)
- [add](https://jqlang.github.io/jq/manual/#add)
