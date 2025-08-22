# Command Line Basics

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/A386XmKi6M8?si=bZ-bNqFeJjgQGbOp" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

In this Episode, we will cover the most common Linux command-line commands.

Linux has two main ways of identifying a user’s access level. A <kbd>$</kbd> is for the normal user and a <kbd>#</kbd> sign is usually for the root or privileged user

| Command | What it Does | Why would you use it |
| --- | --- | --- |
| Echo | Displays the text you type out |     |
| PWD (print working directory) | Prints the directory you are in |     |
| LS (list directories) | List the sub-directories attached to the directory you are in |     |
| Touch | Create new empty files |     |
| File | Tells you the file type |     |
| Cat | Displays file Content | Good for small files |
| Nano | Text editor |     |
| Less | Navigate through a file by pages | To navigate through big files |
| History | History of the commands that you previously entered | To recall a command you may need again |
| Cp (copy) | Copies a file to a new location | Keeps the original file and gives a copy of the file |
| Mv (move) | Used for moving files and also renaming them | Moves the original file to the specific location |
| Mkdir (Make Directory) | It will create a directory if it doesn’t already exist. | Directories are good for organizing files and applications |
| Rm (remove) | Used to delete files and directories. |     |
| Find | Helps us search for files | You may forgotten where you stored a config file but know the name |
| Help (other tool name) | Used to see the instructions on how to use a command line tool |     |
| Man (other tool name) | Displays a manual for that tool |     |
| Whatis (other tool name) | Provides a brief description of command line program |     |
| Alias/Unalias (name) | Assigns a name to commands | Sometimes typing commands can get really repetitive, or if you need to type a long command many times, it’s best to have an alias you can use for that. To create an alias for a command you simply specify an alias name and set it to the command. |
| Exit | Logout command |     |

## Checkout this series here   
Check out videos in this playlist [here](https://www.youtube.com/playlist?list=PLAvgoEDVC5qGxD1JIioyofs2IL7XKUnkT)

## Updating Linux

Before you do anything, it is always best to ensure your Linux Environment is up to date and pulling the latest repos:

```
sudo apt update && sudo apt upgrade -y
```

## Echo

**Description:** Prints text or variables to the terminal. Useful for displaying messages or variable values.

```
echo "Hello, world!"
```

## PWD (print working directory)

**Description:** Shows the full absolute path of your current directory.

```
pwd
```

## LS (list directories)

**Description:** Lists files and directories in the current location. Add options for details or hidden files.

```
ls -l
```

## Touch

**Description:** Creates a new, empty file or updates the timestamp of an existing file.

```
touch example.txt
```

## File

**Description:** Shows the type of a file (text, directory, binary, etc.).

```
file example.txt
```

## Cat

**Description:** Concatenates and displays the content of files in the terminal.

```
cat example.txt
```

## Nano

Nano can be used as a text editor, which is usually found in most Linux distributions.

```
nano example.txt
```

## Less

**Description:** Opens a file interactively so you can scroll through it, useful for long files.

```
less example.txt
```

## History

**Description:** Displays a list of previously entered commands.

```
history
```

## Cp (copy)

**Description:** Copies files or directories to a new location.

```
cp example.txt backup.txt
```

## Mv (move)

**Description:** Moves or renames files and directories.

```
mv backup.txt archive.txt
```

## Mkdir (Make Directory)

**Description:** Creates a new directory (folder).

```
mkdir myfolder
```

## Rm (remove file)

**Description:** Deletes files or directories. Use with caution!

```
rm example.txt
```

## Rmdir (remove directory)

```
rmdir testdir
```

## Find

**Description:** Searches for files and directories matching criteria (name, type, etc.).

```
find . -name "example.txt"
```

## Help (other tool name)

**Description:** Shows brief help for a command, listing options and usage.

```
ls --help
```

## Man (other tool name)

**Description:** Displays the full manual (documentation) for a command.

```
man ls
```

## Whatis (other tool name)

**Description:** Gives a one-line description of a command.

```
whatis ls
```

## Alias/Unalias (name)

**Description:** Creates or removes shortcuts for commands (aliases).

```
alias ll='ls -l'
```

To get rid of an alias type:

```
unalias ll
```

## Exit

**Description:** Closes the current terminal session or shell.

```
exit
```

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)