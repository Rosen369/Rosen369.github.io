---
layout: post
title: Commit-msg git hook
desc: a commit-msg local git hook for check commit message
categories: [tools]
tags: [git]
---

```shell
#!/bin/sh
#
# feat：new features
# fix：fix bug
# docs：documentation
# style： format code style
# refactor：refactor
# test：add unit test code
# chore：chores

commit_message=$1

array=("feat" "fix" "docs" "style" "refactor" "test" "chore")

while read line; do
    echo $line
    if [[ ! " ${array[@]} " =~ " ${line%%:*} " ]]; then
        echo "Commit Message don't conform to specification,Please check it."
        exit 1
    elif [ -z "${line#*:}" ]; then
        echo "${line%%:*}： is empty,Please check it."
        exit 1
    fi
done <${commit_message}
```
