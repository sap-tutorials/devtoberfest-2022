---
auto_validation: true
time: 20
author_name: DJ Adams
author_profile: https://github.com/qmacro
tags: [ tutorial>beginner, topic>cloud ]
primary_tag: topic>cloud
parser: v2
---

# 🟡 Devtoberfest 2024 - Fun Friday Week 3 - Bugtoberfest Bash
<!-- description --> This is the Bash Bug Hunt!

## You will learn
- How to have fun hunting for bugs in code.

## Prerequisites
- Basic to intermediate knowledge of Bash.


## Intro
As a part of Devtoberfest 2024 Fun Friday events, we have a bug hunt written in multiple languages for you to complete! The questions will range from easy to spot to a little more difficult, requiring some knowledge of the individual languages to complete. Each question will have 1 to 10 bugs and no bug should require running the code for the bug to appear.

There may be occasions where, for example, a misspelled variable may occur multiple times. Count this as one bug as a whole, not one bug for each of the occurrences of the misspelling.

If you're curious to learn more about good Bash scripting habits, be sure to check out these resources:

* [progrium/bashstyle](https://gist.github.com/outro56/4a2403ae8fefdeb832a5)
* [Bash pitfalls](https://mywiki.wooledge.org/BashPitfalls)
* [Shellcheck](https://mywiki.wooledge.org/BashPitfalls)
* [Improving my shell scripting](https://qmacro.org/blog/posts/2020/10/05/improving-my-shell-scripting/)

Remember to have fun and enjoy the bug hunt. Happy hunting!

This tutorial is part of Devtoberfest 2024, a celebration of and for Developers. For more information, see the [Devtoberfest Group](https://groups.community.sap.com/t5/devtoberfest/gh-p/Devtoberfest).

![Devtoberfest](promo-image-kasimir-square.png)

&nbsp;

For specifics on the Devtoberfest contest and the grand prize, see this [Devtoberfest 2024 Contest blog](https://community.sap.com/t5/devtoberfest-blog-posts/devtoberfest-2024-contest/ba-p/13781593)

&nbsp;

### Question 1 (Easy)

Find the bugs in the following code.

```bash
#!/usr/bin/env bash

read -p 'Enter your name: '
$answer = $REPLY
echo 'Thank you. You entered $answer.'
```

### Question 2 (Medium)

Find the bugs in the following code. Assume that the `pass` tool referenced in this script exists (it's the [standard Unix password manager](https://www.passwordstore.org/)).

```bash
#!/usr/bin/env bash

set -e
set pipefail

main {

  local account="${1:?No account specified}"

  # Cause script to abend if no account data stored
  pass "btp/$account" > dev/null

  cf login
    -a "$(pass "btp/$account/cfapiendpoint")" \
    -u "$(pass "btp/$account/user")" \
    -p "$(pass "btp/$account/password")"

  echo <<EOF
Thank you.
Logged in successfully.
EOF

}

main "$@"
```

### Question 3 (Hard)

In this (somewhat contrived but simple) script the bugs are less syntactical, and more subtle, and exhibit pitfalls described in the Bash Pitfalls resource referenced in the introduction to this tutorial.

The `shellcheck` tool will point out a number of pitfalls in this script, at various levels:

- Informational ("it's best not to do this")
- Warning ("this is not a good idea at all")
- Error ("this is broken")

Note that you should count _all_ types of levels, not just those at the Error level. This is mainly because in Bash, even Informational (arguably "best practice") are more important to be heeded than in other languages.

Good luck!

```bash
#!/usr/bin/env bash

read -p 'Enter a color: ' color

if [ $color == 'black' ]; then
    echo "Black is not a color, it is the absence of color"
fi

if [ $color =~ ^(red|green|blue)$ ]; then
    echo "You chose a primary color"
fi

cd colors
touch "$color.txt"
```

> Bonus info: [the open square bracket is an executable](https://qmacro.org/blog/posts/2020/08/21/the-open-square-bracket-is-an-executable/)

