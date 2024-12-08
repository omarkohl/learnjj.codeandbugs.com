---
description:
  "Version private files in a public repository without sharing them."
---

# Private files in public repo 

## Scenario

You are working in a project, collaborating with other people but there are
some files within that project that you don't want to share, but still want to
version.

Concrete example in our application would be you are using a specific IDE,
namely PyCharm, which stores the configuration in a `.idea/` directory.


## Commit private files

First:

* Make sure you start with an empty change e.g. execute `jj new`
* Start PyCharm. If you don't use PyCharm just create a `.idea/` directory with
  some (empty) file inside for this tutorial.

```bash title="Describe your change"
jj desc -m "local: keep track of .idea (PyCharm config)"
```

```bash title="Current state"
jj
```

The new change is just on the top of our history, as expected. We would like to
move the to the _side_ so that we can work on the code without worrying about
that change.

```bash title="Move the change out of the way"
jj new @- @
```

```bash title="Current state"
jj
```

```bash title="Rebase the change onto the root"
# CHANGE_ID is the id of the ".idea" change (mwzllxkn in my case)
jj rebase --revisions CHANGE_ID --destination "root()"
```

```bash title="Current state"
jj
```

Hmm, that's not exactly what we wanted. We lost our merge change. We could of
course just create it again but let's instead learn to undo operations.

```bash title="Look at the operation history"
jj op log
```

```bash title="Restore a past state of the repository"
# OPERATION_ID is the id of the operation before the rebase (d042 in my case)
jj op restore OPERATION_ID 
```

:::tip jj undo

`jj undo` allows you to undo some operation, by default the last one.
Unfortunately in my opinion this does not work as well as `jj op restore`
because sometimes a command like `jj log` appears in the operation log so you
would be undoing _that_ operation, which is not harmful but also doesn't help.

You could use `jj op log` to identify the operation you want to undo and then
call `jj undo IDENTIFIER` to do so.

:::


```bash title="Perform the rebase we want"
# CHANGE_ID is the id of the ".idea" change (mwzllxkn in my case)
jj rebase --source CHANGE_ID --destination "root()"
```

```bash title="Current state"
jj
```

The difference between the two rebase commands was that one used the
`-r/--revisions` options and the other `-s/--source`. The second option rebases
the entire descendant tree, which is what we wanted. There is a third option
`-b/--branch`. Check the help to find out what it does.

```bash
jj rebase --help
```


## Continue developing

Now of course we have this merge change in our history that we do not want to
share with other developers. How do we continue working then?

```bash
jj new
```

* Add a new feature to the app e.g. TODO
* Modify an IDE setting (or manually add a file to the `.idea/` folder)

```bash
jj split .idea
```

An editor will open. Describe the changes you made e.g. "local: fix IDE
settings".

```bash title="Look at the result"
jj
jj st
jj diff
```

```bash
jj desc -m "feat: add todocli entry point"
jj new
```

Implement another feature.


```bash
jj desc -m "feat: add "--version" flag"
jj new
```

Now put everything into its right place. Look at the current status:

```bash
jj
```

```bash
# rebase IDE change after previous local IDE change
jj rebase -r so -A m
```

```bash
# rebase my two features on top of where I want them
jj rebase -r r -r w -A l
```

```bash
jj
```
