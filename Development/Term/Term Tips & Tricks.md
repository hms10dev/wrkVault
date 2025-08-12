

# ZSH

## The Most Common zsh files:

* ~/.zshrc: 
	* This is the most commonly used zsh file. It is run every time a new shell is opened and is used to set up your shell environment. You can use this file to configure aliases, customize your prompt, set environment variables, and more.
- ~/.zsh_profile or ~/.zprofile: 
	- This file is run once at login, before ~/.zshrc. It is often used to set environment variables that should be available to all shells, such as the PATH variable.
- ~/.zshenv: 
	- This file is read by every shell that is opened and is used to set environment variables that should be available to all processes, not just shells.
- /etc/zshenv: 
	- This file is similar to ~/.zshenv, but is read by all users on the system. It is often used to set system-wide environment variables.
- /etc/zshrc: 
	- This file is similar to ~/.zshrc, but is read by all users on the system. It is often used to set system-wide aliases or shell options.

> [!info] Note :
It's worth noting that there is no hard and fast rule for which file to use for a given configuration. Some people prefer to keep all of their settings in **~/.zshrc**, while others use **~/.zsh_profile** for everything. In general, it's a good idea to use the most specific file that makes sense for a given configuration. For example, if you have an environment variable that should be available to all shells, use **~/.zshenv or /etc/zshenv.**



### How to find the ~/.zshrc file:

The ~/.zshrc file is located in your home directory. You can access it by opening a new Terminal window and running the following command:

```
open ~/.zshrc
```

This will open the ~/.zshrc file in your default text editor, if the file already exists. If the file does not exist, the command will create a new file in your home directory.Alternatively, you can navigate to your home directory by running cd ~, and then run ls -a to list all files, including hidden files. The ~/.zshrc file should be listed among them. You can open it in a text editor by running nano ~/.zshrc or vim ~/.zshrc, depending on your preferred editor.

