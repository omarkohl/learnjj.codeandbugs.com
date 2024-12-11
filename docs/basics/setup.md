---
sidebar_position: 1
description: Installation and configuration of jj.
---
# Setup

## Installation

Follow the [installation instructions](https://martinvonz.github.io/jj/latest/install-and-setup/).

```bash title="Run"
jj version
```

```bash title="Expected output (similar)"
jj 0.24.0-32d2a85539254e9d96f9819072fa5c6ac70dd1e4
```


## Config

Set some _global_ (for your user) configuration. Adapt as needed.

```bash title="Set your preferred text editor"
jj config set --user ui.editor vim
```

```bash title="Set email and name"
jj config set --user user.email ME@EXAMPLE.COM
jj config set --user user.name "MY NAME"
```

Make `jj` default to `jj log`, which is very convenient:

```bash
jj config set --user ui.default-command log
```

:::tip Repository-specific configuration

If you are inside a repository, you can set configuration that only applies to
that repository. Use `--repo` instead of `--user`.

:::


### (Optional) Make "log" more verbose

```bash title="Get the default value"
jj config get revsets.log
```

```bash title="Change the value"
jj config set --user revsets.log "present(@) | ancestors(immutable_heads().., 7) | present(trunk())"
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

```bash title="See the log (history)"
jj
```

![Log output](./log.webp)
