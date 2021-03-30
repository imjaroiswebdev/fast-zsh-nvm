# Fast-ZSH-NVM


## Overview

A ZSH plugin to initialize [NVM](https://github.com/nvm-sh/nvm) quickly when a new terminal opens.

If `AUTO_LOAD_NVMRC_FILES` is set to `true`, this plugin also runs `nvm use` automatically whenever you enter a directory that contains an `.nvmrc` file (which NVM reads to discover what version of node to use in that location).


### Why?

Other NVM-loading scripts I've seen (including the default technique provided in NVM itself) have been [widely](https://github.com/nvm-sh/nvm/issues/539) [reported](https://github.com/nvm-sh/nvm/issues/1242) [to](https://github.com/nvm-sh/nvm/issues/1721) [be](https://github.com/nvm-sh/nvm/issues/1774) [slow](https://broken-by.me/lazy-load-nvm/).

Thanks to some feedback from [NVM's main author](https://github.com/nvm-sh/nvm/issues/1242#issuecomment-249253858) and [another helpful developer](https://github.com/nvm-sh/nvm/issues/539#issuecomment-403661578), there are a couple ways to speed this process up (the `--no-use` option and asynchronous loading). I just compiled both into an easy-to-install package.


## Integration with plugin managers

`fast-zsh-nvm` requires the `mafredri/zsh-async` package, so be sure to install both in your plugin manager of choice.

### [antibody](https://github.com/getantibody/antibody)

Update your `.zshrc` file with the following two lines (order matters):

```sh
antibody bundle mafredri/zsh-async
antibody bundle allanjamesvestal/fast-zsh-nvm
```

### [antigen](https://github.com/zsh-users/antigen)

Update your `.zshrc` file with the following two lines (order matters). Do not use the `antigen theme` function.

```sh
antibody bundle mafredri/zsh-async
antibody bundle allanjamesvestal/fast-zsh-nvm
```

### [zgen](https://github.com/tarjoilija/zgen)

```
zgen load mafredri/zsh-async
zgen load allanjamesvestal/fast-zsh-nvm
```

### [zplug](https://github.com/zplug/zplug)

Update your `.zshrc` file with the following two lines:

```sh
zplug "mafredri/zsh-async", from:github
zplug "allanjamesvestal/fast-zsh-nvm", from:github
```


## Configuration

`fast-zsh-nvm` has three configuration options. Each can be triggered by setting the corresponding environment variable to `true`.

`AUTO_LOAD_NVMRC_FILES` listens every time you change directories. If the new directory has an `.nvmrc` file, this option will automatically switch to the correct node verson for that folder.

`LOAD_NVMRC_ON_INIT` extends the plugin to also run that auto-loading behavior just after the terminal session starts. This is disabled by default, as it adds significantly to the initial load time if your starting directory contains a `.nvmrc` file.

`NVM_SCRIPTS_DIR` in case that `nvm` isn't located at `NVM_DIR` then is possible to use this variable to set the right location for *nvm*'s scripts. This is the case when installing nvm through `brew` which installs it i.e.: `/usr/local/opt/nvm/nvm.sh`.


## Addtional Advice

In order for this to work you may need to get rid of these lines that might already exists in your `.zshrc` configuration file.

```sh
  [ -s "/usr/local/opt/nvm/nvm.sh" ] && . "/usr/local/opt/nvm/nvm.sh"  # This loads nvm
  [ -s "/usr/local/opt/nvm/etc/bash_completion.d/nvm" ] && . "/usr/local/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
```
