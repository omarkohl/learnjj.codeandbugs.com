---
sidebar_position: 1
description: Installation and configuration of jj.
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Setup

## Installation

Start by installing `jj`, following the [installation
instructions](https://martinvonz.github.io/jj/latest/install-and-setup/).

Verify the installation was successful:

```bash title="Run"
jj version
```

```bash title="Expected output (similar)"
jj 0.24.0-32d2a85539254e9d96f9819072fa5c6ac70dd1e4
```

```bash title="Overview of commands"
jj -h
```


## Config

### Basics

Set some _global_ (for your user) configuration. Adapt as needed.

```bash title="Set your preferred text editor"
# Note if you have an EDITOR env variable you can skip this
jj config set --user ui.editor vim

## To copy the setting from Git use the following instead:
#jj config set --user ui.editor "`git config --get core.editor`"
```

```bash title="Set email and name"
jj config set --user user.email ME@EXAMPLE.COM
jj config set --user user.name "MY NAME"

## To copy the settings from Git use the following instead:
#jj config set --user user.email "`git config --get user.email`"
#jj config set --user user.name "`git config --get user.name`"
```

Make `jj` default to `jj log`, which is very convenient. Otherwise you'll have
to type `jj log` instead of `jj` every time you want to see the history, which
is frequently.

```bash
jj config set --user ui.default-command log
```

:::tip Repository-specific configuration

If you are inside a repository, you can set configuration that only applies to
that repository. Use `--repo` instead of `--user`.

:::


### (Optional) Make "log" more verbose

```bash title="If you are curious, see the default value"
jj config get revsets.log
```

```bash title="Change the value"
jj config set --user revsets.log '"present(@) | ancestors(immutable_heads().., 7) | present(trunk())"'
```


### (Optional) Manually edit the config file

```bash title="See location of config file"
jj config path --user
```

```bash title="Open the config file in an editor"
jj config edit --user
```


## Clone Repository

```bash title="Clone the repository"
jj git clone --colocate https://github.com/omarkohl/jj-tutorial
cd jj-tutorial
```

:::tip Colocate

`--colocate` allows you to use both Git commands and Ju Jutsu commands in the
same repository. If you don't use that option then Ju Jutsu will still keep an
internal Git repository inside the `.jj/` directory but you will not be able to
execute any `git ...` commands yourself.

:::


```bash title="See the log (history)"
jj
```

![Log output](./log.webp)


## (Optional) Try it in another Git repository

If you have any local Git repository I encourage you to try using `jj` in it too:

```bash
cd path/to/my/repo
jj git init --colocate
```

Now you can use `jj` with all the things you learn in this tutorial.

If you ever want to get rid of `jj` in this repository:

```bash
cd path/to/my/repo
rm -rf .jj/
```

That's it, as if `jj` had never been there! Any commits you created, rebased
etc. via `jj` will of course be there since `jj` synchronizes the `jj` data
with Git. It will just look as if everything had been done with Git.


## (Optional) Shell completion

If you use bash, you can add the following to your `~/.bashrc`:

```bash
source <(jj util completion bash)
```

See [more
examples](https://martinvonz.github.io/jj/latest/install-and-setup/#command-line-completion)
for other shells.


## (Optional) Live 'jj log'

A convenient way of permanently seeing the current state of your log is to run
this command in a separate terminal window and have it open next to your work.

```bash
cd path/to/repo
watch --color jj --ignore-working-copy log --color=always
```

See an explanation and alternatives
[here](https://martinvonz.github.io/jj/latest/FAQ/#can-i-monitor-how-jj-log-evolves).


## Takeaways

Key points. As QA because of [active
recall](https://en.wikipedia.org/wiki/Testing_effect). Try to come up with the
answer yourself before looking 😉

<Tabs>
  <TabItem value="questions" label="Questions" default>
    1. What is the relationship between Ju Jutsu and Git?
    2. If you forget about a particular command, how do you refresh your memory?
  </TabItem>
  <TabItem value="answers" label="Answers">
    1. Ju Jutsu stores everything inside a `.jj/` directory, including an
       internal Git repository.  Additionally, if your repository is
       _colocated_ then the top level will **also** be a Git repository.  Both
       Ju Jutsu and Git commands can then be used. Ju Jutsu makes sure to
       synchronize data bidirectionally. If you ever want to stop using Ju
       Jutsu in a repository you can just delete the `.jj/` directory.
    2. Use `jj -h`. To get more information for a particular command e.g.
       `config` use `jj config -h` or for even more information either `jj
        config --help` or `jj help config`.
  </TabItem>
</Tabs>
