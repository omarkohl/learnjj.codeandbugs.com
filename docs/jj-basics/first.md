# Setup

## Installation

Follow the [installation instructions](https://martinvonz.github.io/jj/latest/install-and-setup/).

Verify you can run:

```bash
jj version
```

Expected result (similar to):

```bash
jj 0.23.0-5de285f5eb727b613434979cd9d83c30cabaffae
```


## Config

Set some _global_ (for your user) configuration. Adapt as needed.

```bash
jj config set --user ui.editor vim
jj config set --user user.email omarkohl@posteo.net
jj config set --user user.name "Omar Kohl"
```

Optional: Change the default "log" output to be a little more verbose.

```bash
# See the default value first
jj config get revsets.log

# Change the value
jj config set --user revsets.log "present(@) | ancestors(immutable_heads().., 7) | present(trunk())"
```

Optional: You can also edit the config file directly.

```bash
# Find the file ...
jj config path --user

# ... or directly open a text editor:
jj config edit --user
```


## Clone Repository

Clone the tutorial repository:

```bash
jj git clone --colocate https://github.com/omarkohl/jj-tutorial
cd jj-tutorial
```

Execute:

```bash
jj log
```

Expected result (similar to):

```bash
TODO
```
