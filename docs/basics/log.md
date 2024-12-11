---
sidebar_position: 2
description: Analyze the history of the repository.
---

# Log

## Introduction

The `jj log` command shows the history of the repository. If you configured `jj`
as recommended in the last section, you can simply run `jj` to get the log
output.

```bash
jj
```

![Log output](./log.webp)

A few things to note about the above screenshot:

* Starting at the top left, `@` is the working copy, which includes all
  "uncommitted" modifications to the working directory. "uncommitted" is in
  quotes because in jj, changes are always committed. It is only uncommitted in
  the usual Git sense.
* Next to it, you have `smmzpnrn`, the change ID. Every change has such an ID
  that never changes even as you modify, rebase etc. the change. Highlighted is
  the shortest unique prefix that identifies the change, `s` in this case.
  Whenever a change ID is required you can just use this prefix.
* After the email address and commit date you have the commit ID as in Git. It
  is in fact exactly the same commit ID as in Git. It will change every time you
  modify the change. In this case `cacb68cb`, again with the shortest unique
  prefix `c` highlighted.
* The next change `w` has a bookmark `main` attached to it. Bookmarks are
  the jj equivalent of branches. Also attached to it is the `git_head()` revset
  function which identifies the HEAD of the Git repository. You'll notice that
  the `@` change is not included in `git_head()`, meaning it will not appear
  when for instance you execute `git log`. Ju Jutsu maintains a separate
  internal Git history inside the `.jj` directory.

:::tip Change vs. Commit

A change is a commit as it evolves over time. You can consider them to be
equivalent only that the change ID will remain unchanged as you modify its
content, rebase it etc. Note that change IDs are currently NOT shared via
push/pull so they may differ between repositories.

This sounds more complicated than it is. You'll see!

:::


## Examples

Try them!

```bash title="Show all the history"
jj -r ::
```

```bash title="Show the ancestors of 'main' but limit to 3"
jj -r ..main -n 3
```

```bash title="Show all children of the change 'kt'"
jj -r kt+
```

```bash title="Show all changes that are ancestors of 'main' and were commited on 2024-12-05"
jj -r 'committer_date(after:"2024-12-05") & committer_date(before:"2024-12-06") & ::main'
```

Check the [Revset language](https://martinvonz.github.io/jj/latest/revsets/) for
more options.


## Other Commands

Try them out!

Some more useful commands and options:

```bash title="Display log with file names"
jj -s
```

```bash title="Summarize the current change"
jj show
```

```bash title="Summarize the latest change on 'main', only file names"
jj show -s main
```

