# Setup

## Installation

Follow the [installation instructions](https://martinvonz.github.io/jj/latest/install-and-setup/).

```bash title="Run"
jj version
```

```bash title="Expected output (similar)"
jj 0.23.0-5de285f5eb727b613434979cd9d83c30cabaffae
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

### (Optional) Default "log" output

Make it a little more verbose.

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

```bash title="Expected output (similar)"
@  nysytqzy omarkohl@posteo.net 2024-12-04 21:26:47 fc266a06
│  (empty) (no description set)
○  tnvsnpur omarkohl@posteo.net 2024-12-04 21:26:47 git_head() 7682755e
│  improve code blocks
○  twmqrppx omarkohl@posteo.net 2024-12-04 20:49:19 986b03cf
│  add content to main tutorial page
○  mvwtstvr omarkohl@posteo.net 2024-12-04 20:18:48 73ef312b
│  update button on main page
○  vwtumtnt omarkohl@posteo.net 2024-12-04 20:14:07 03616c82
│  add commands for global jj configuration
○  qutqwkol omarkohl@posteo.net 2024-12-04 20:14:07 5ed0d123
│  update the global configuration
○  qooyoykq omarkohl@posteo.net 2024-12-04 20:14:07 7b0d58b3
│  add some basic jj setup instructions
○  upslplnp omarkohl@posteo.net 2024-12-04 20:11:46 daf3d9d5
│  dev: don't start the browser automatically
○  uuvksslk omarkohl@posteo.net 2024-12-04 20:11:46 51376100
│  Initial commit
◆  zzzzzzzz root() 00000000
```
