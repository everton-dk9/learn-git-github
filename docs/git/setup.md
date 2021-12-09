# Git installation and setup

Set the following global configurations if it's your first time usage:

Set user name:
```
git config --global user.name "My Name"
```
Set user email:
```
git config --global user.email "myemail@example.com"
```
Set default editor (vim is the default editor, I use VScode):
```
git config --global core.editor "code --wait"
```

Unset the editor:
```
git config --global --unset core.editor
```

There is a file called .gitconfig that store some configurations settings, we can
modify this or use commands:
```
:~/.gitconfig
```

To list all the configuration settings in .gitconfig file type:
```
git config --list
```