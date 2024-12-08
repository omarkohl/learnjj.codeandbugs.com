# learnjj.codeandbugs.com

[Ju Jutsu (jj)](https://martinvonz.github.io/jj/latest/) tutorial source, built
using [Docusaurus](https://docusaurus.io/). **jj** is a VCS (version control
system), like Git or Mercurial.

Visit https://learnjj.codeandbugs.com to get started.


# Developer Documentation

Documentation for people who want to contribute to the tutorial. If you only
want to learn jj the following is probably uninteresting to you.

## Installation

```
$ yarn
```

## Local Development

```
$ yarn start
```

This command starts a local development server and opens up a browser window.
Most changes are reflected live without having to restart the server.

## Build

```
$ yarn build
```

This command generates static content into the `build` directory and can be
served using any static contents hosting service.


## Screenshots

For taking screenshots on Ubuntu 22.04:

* Open a new terminal (default size)
* Execute `export PS1="$ "` and `PROMPT_COMMAND='echo -ne "\033]0;omar@ubuntu\007"'`
* Take screenshots of that window with the Print key
