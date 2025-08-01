---
sidebar_position: 1
title: Introduction
slug: /
description: Learn the fantastic Git-compatible version control system
---

# Ju Jutsu Tutorial - Introduction
Let's discover **Ju Jutsu**!

[Ju Jutsu](https://jj-vcs.github.io/jj/latest/) is a VCS (version control
system) like **Git or Mercurial** that is fully compatible with Git. You can
use it inside a Git repository with the option of going back to Git at any
time. You can in fact mix and match Git and Ju Jutsu commands, depending on
which suit you more _right now_.

## What will you get out of this tutorial?

A hands-on introduction to Ju Jutsu where you will be trying all the commands
on your own PC. It will show case real workflows, including resolving
non-trivial conflicts and interacting with GitHub (e.g. to create pull
requests).

You will walk away with a solid understanding of Ju Jutsu concepts and get a
taste for the situations in which it might be helpful to you.

## Prerequisites

This tutorial makes certain assumptions. If those assumptions don't hold you
may struggle with the tutorial.

* You know **how to use Git**: While in theory Ju Jutsu is a great first VCS
  for new developers, such developers would require a different tutorial. Also
  in practice Ju Jutsu currently relies on Git for remote collaboration, so
  knowing Git is basically unavoidable.
* You are comfortable using **(interactive) rebase, squash and cherry-pick**:
  In reality this is not a hard requirement but if you are not comfortable
  using those Git tools then you probably use a very linear Git workflow and
  you might feel that the workflows presented here are solving problems that
  you don't have. I think Ju Jutsu is still great for such a simple, linear
  workflow but it would probably require a different tutorial to make that case
  well.
* You are ok using a **CLI (command line interface)**: Since Ju Jutsu is quite
  new there are few graphical tools or IDE support. This tutorial will be using
  the CLI.


## Differences from Git

As a _friendly warning_ here are some differences between Git and Ju Jutsu that
may confuse you at first. I believe all the choices in Ju Jutsu are in fact
better and all differences plus better workflows (or if you insist on the Git
way of doing things: _workarounds_) will be addressed in due course during the
tutorial. I claim there is nothing you can do in Git that you can't do equally
well or better in Ju Jutsu.

* The fundamental unit of change is called **change** not **commit**, even
  though there are commits too.
* Everything is **always committed**, automatically after you modify anything.
* There is **no index** (staging area).
* Ju Jutsu uses **bookmarks** as the equivalent of **branches** but you rarely
  need them. Ju Jutsu is a _branchless_ VCS. You will almost always be in what
  Git calls _detached HEAD state_. There is **no way of checking out** a
  bookmark and making it move automatically as you keep adding changes.

Here is a more [detailed
comparison](https://jj-vcs.github.io/jj/latest/git-comparison/).
