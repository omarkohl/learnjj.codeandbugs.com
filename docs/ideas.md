---
sidebar_position: 98
---
# Ideas

Ideas for things to include in this tutorial.

* I noticed that a past change includes files I did not want e.g. the .idea
  directory. How can I remove them from the history? The change contains other
  changes to the blog/ directory that I want to keep.
  `jj split blogs/ zo` will split into a first change with the blog and a second
  change with the rest. In both cases it will open the editor to edit the
  description.
* Keep track of some development-local things e.g. the .idea/ directory but
  don't push it. `jj rebase -r kz -d "root()"`
