---
sidebar_position: 4
description: Continue developing, committing and changing things.
---

# Adding Changes 2

This builds on the [previous section](./adding_changes.md).

## What will we do

* Implement storing tasks in a file
* Make the file configurable with `--file/-f`
* Cleanup
* Documentation

We will keep practicing with the commands from the previous section and add the
following:

* `abandon`
* `commit`
* `edit`

## Storing tasks

We will store all tasks in a text file `.todocli.json` in the current
directory.

We will try a slightly different workflow for this, starting with a new, empty
change:

```bash
jj new
```

Now we describe what we **want** to do:

```bash
jj desc -m "feat: store tasks in .todocli.json file"
```

Note that the above change is empty even though it already has a description!
Then we create another empty change on top of the previous one:

```bash
jj new
```

TODO Screenshot

:::tip jj commit

`jj describe -m "MESSAGE"` followed by `jj new` can also be replaced by
`jj commit -m "MESSAGE"`. It's completely equivalent. `commit` allows you to
describe the current change and then create a new change in one step.

:::

:::info Git index

Do you miss the Git index (staging area)?

This new empty change is where we can work freely and then squash any relevant
modifications into the previous change. This workflow is comparable to using the
index (staging area) in Git, where the previous change plays precisely the role
of _index_ (albeit already with a description documenting what we are trying to
do).

:::

Make the following two modifications to `todocli/cli.py`:

```python title="todocli/cli.py"
import json
```

```python title="todocli/cli.py"
def list_cmd():
    try:
        with open(".todocli.json", "r") as f:
            tasks = json.load(f)
    except FileNotFoundError:
        tasks = []
    for i, task in enumerate(tasks, 1):
        print(f"{i}. {task['title']}")
        print(f"   {task['description']}")
    else:
        print("No tasks.")
```

Then squash this into the change where we are implementing storing tasks in a
file:

```bash
jj squash
```

Check the result:

```bash
jj show
jj show @-
```

Now we think we should store the file name in a constant so let's implement
that:

```python title="todocli/cli.py"
STORAGE_FILE = ".todocli.json"


# ...

def list_cmd():
    try:
        with open(STORAGE_FILE, "r") as f:
            tasks = json.load(f)
# ...
```

And again we can squash this into the previous change:

```bash
jj squash
```

If we execute the result:

```bash
poetry run todocli list
```

We see there is some obsolete output we no longer want:

```text
No tasks.
Hello, World!
```

Let's clean that up:

```bash
jj commit -m "fix: remove obsolete output"
```

Remove the line:

```python title="todocli/cli.py"
    print("Hello, World!")
```

Then squash this into the previous change:

```bash
jj squash
```

Let's look at the result:

```bash
jj
```

TODO screenshot

Removing the obsolete output is unrelated to storing tasks in a file so we can
move it further back into history:

```bash
jj rebase -r @- -B qo
```

Again, check the output:

```bash
jj
```

TODO screenshot

## Adding new tasks

Now we want to add the ability to add tasks. Make sure you are starting with an
empty change (e.g. use `jj new`). Then:

```bash
jj commit -m "feat: add the 'add' command"
```

Well, on second though, let's make the storage file configurable first.


## Make storage file configurable

```bash
jj commit -m "feat: make storage file configurable"
```

Let's look at the current status:

```bash
jj
```

TODO screenshot

We could keep the (empty) change for adding the 'add' command but instead let's
try out `abandon`:

```bash
jj abandon CHANGE_ID
```

OK, let's continue working on making the storage file configurable by passing a
`--file/-f` option to the `list` command. Thinking about it, we realize that
other future commands will also require this option se we might as well make it
global. The argument handling is getting a little complicated so let's use a
library for that:

```bash
jj commit -m "refactor: use argparse for argument handling"
```

Make the following changes to `todocli/cli.py`:

Delete the `help()` function

```python title="todocli/cli.py"
import argparse
```

```python title="todocli/cli.py"
def cli():
    parser = argparse.ArgumentParser()
    parser.add_argument("-v", "--version", action="store_true", help="Show the version and exit.")
    subparsers = parser.add_subparsers(dest="command", help="Available commands")
    subparsers.add_parser("list", help="List all tasks.")
    subparsers.add_parser("version", help="Show the version and exit.")
    subparsers.add_parser("help", help="Show this help message and exit.")
    args = parser.parse_args()

    if args.version or args.command == "version":
        version()
    elif args.command == "help" or not args.command:
        parser.print_help()
    elif args.command == "list":
        list_cmd()
```

Then squash this into the previous change:

```bash
jj squash
```

Let's re-order the changes so that the switch to argparse happens first.

Look the status and figure out yourself how to achieve the desired end result:

TODO screenshot


Add the `--file/-f` option to the `list` command:


```python title="todocli/cli.py"
def list_cmd(storage_file):
    try:
        with open(storage_file, "r") as f:
            tasks = json.load(f)
```

```python title="todocli/cli.py"
    parser.add_argument("-v", "--version", action="store_true", help="Show the version and exit.")
    parser.add_argument("-f", "--file", default=STORAGE_FILE, help=f"Specify the storage file. Default is: {STORAGE_FILE}")
    subparsers = parser.add_subparsers(dest="command", help="Available commands")
```

```python title="todocli/cli.py"
    list_cmd(args.file)
```

Then squash this into the previous change:

```bash
jj squash
```


## Next steps

TODO

* show how to use 'edit' to add documentation for the lowest change
* go back to the top change, add more documentation for the --file and then
  squash it with --into

