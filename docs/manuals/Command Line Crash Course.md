# Command Line Crash Course #

**Table of Content**

[TOC]

## The Setup

You will be instructed to do three things:

- Do some things in your shell (command line, Terminal, PowerShell).
- Learn about what you just did.
- Do more on your own.

For this first exercise you'll be expected to get your Terminal open.

### Mac OS X

- Hold down the `command` key and hit the spacebar.
- In the top right the blue 'search bar' will pop up.
- Type: `terminal`
- Click on the terminal application that looks kind of like a black box.
- This will open Terminal.
- You can now go to your dock and CTRL-click to pull up the menu, then select `Options->Keep` In dock.

### Linux

Look through the menu for your window manager for anything named 'shell or 'terminal'.

### Windows

On Windows we're going to use PowerShell. People used to work with a program called `cmd.exe`, but it's not nearly as usable as PowerShell. If you have Windows 7 or later, do this:

- Click Start.
- In "Search programs and files" type: `powershell`
- Hit Enter. 

### Linux/Mac OSX

List of commands:

- `pwd`; print working directory.
- `hostname`; my computer's network name.
- `mkdir`; make directory.
- `cd`; change directory.
- `ls`; list directory.
- `rmdir`; remove directory.
- `pushd`; push directory.
- `popd`; pop directory.
- `cp`; copy a file or directory.
- `mv`; move a file or directory.
- `less`; page through a file. :q to quit.
- `cat`; print the whole file.
- `xargs`; execute arguments.
- `find`; find files.
- `grep`; find things inside files.
- `man`; read a manual page.
- `apropos`; find what man page is appropriate.
- `env`; look at your environment.
- `echo`; print some arguments.
- `export`; export/set a new environment variable.
- `exit`; exit the shell.
- `sudo`; become super user root.

### Windows

List of commands:

- `pwd`; print working directory.
- `hostname`; my computer's network name.
- `mkdir`; make directory.
- `cd`; change directory.
- `ls`; list directory.
- `rmdir`; remove directory.
- `pushd`; push directory.
- `popd`; pop directory.
- `cp`; copy a file or directory.
- `robocopy`; robust copy.
- `mv`; move a file or directory.
- `more`; page through a file.
- `type`; print the whole file.
- `forfiles`; run a command on lots of files.
- `dir -r`; find files.
- `select-string`; find things inside files.
- `help`; read a manual page.
- `helpctr`; find what man page is appropriate.
- `echo`; print some arguments.
- `set`; export/set a new environment variable.
- `exit`; exit the shell.
- `runas`; become super user root.

## Paths, Folders, Directories (pwd)

You do not type in the `$` (Unix) or `>` (Windows). That's just me showing you my session so you can see what I got.

You type in the stuff after `$ or >`, then hit Enter. So if I have `$ pwd` you type just `pwd` and hit Enter.

You can then see what I have for output followed by another `$` or `>` prompt. That content is the output and you should see the same output.

Let's do a simple first command so you can get the hang of this:

### Linux/OSX

```bash
$ pwd 
/Users/zedshaw
$
```

### Windows

```bash
PS C:\> pwd

C:\Users\zed

PS C:\>
```

## View a File (less, more)

To do this exercise you're going to do some work using the commands you know so far. You'll also need a text editor that can make plain text (.txt) files. Here's what you do:

- Open your text editor and type some stuff into a new file. On OS X this could be TextWrangler. On Windows this might be Notepad++. On Linux this could be gedit. Any editor will work.
- Save that file to your desktop and name it `test.txt`.
- In your shell use the commands you know to copy this file to your `temp` directory that you've been working with.

Once you've done that, complete this exercise:

### Linux/OSX

```bash
$ less test.txt
[displays file here]
$
```

That's it. To get out of `less` just type `:q` (as in quit).

### Windows

```bash
> more test.txt
[displays file here]
> 
```

## Stream a File (cat)

You're going to do some more setup for this one so you get used to making files in one program and then accessing them from the command line. With the same text editor from the last exercise, create another file named `test2.txt` but this time save it directly to your `temp` directory:

### Linux/OSX

```bash
$ less test2.txt
[displays file here]
$ cat test2.txt
I am a fun guy.
Dont you know why?
Because I make poems,
that make babies cry.
$ cat test.txt
Hi there this is cool.
$
```

### Windows

```bash
> more test2.txt
[displays file here]
> cat test2.txt
I am a fun guy.
Dont you know why?
Because I make poems,
that make babies cry.
> cat test.txt
Hi there this is cool.
> 
```

### Edit a file (cat, nano, pico, vim)

- Unix: Try `cat test.txt test2.txt` to concatenate the files on screen.
- Windows: Try `cat test.txt,test2.txt`.
- `cat test.txt` will print on screen.
- `cat file1.txt > file2.txt` to copy.
- `cat file1.txt >> file2.txt` to append.
- Also `nano test.txt`, `pico test.txt`, and `vim test.txt`.

## Exiting Your Terminal (exit)

### Linux/OSX

```bash
$ exit
```

### Windows

```shell
> exit
```

### Unix Bash References

- [Reference Manual](http://www.gnu.org/software/bash/manual/bashref.html)

### PowerShell References

- [Owner's Manual](http://te
- chnet.microsoft.com/en-us/library/ee221100.aspx)
- [Master PowerShell](http://powershell.com/cs/blogs/ebook/default.aspx)