---

**Foreword**

Commands and code snippets. From Codecademy.

---

# Navigation

- Bash means 'Bourne again shell'.
- There exists other bash programs : ksh, tcsh, zsh, etc.
- Common terminals: Ubuntu gnome, KDE konsole, eterm, txvt, kvt, nxterm, eterm.
- A CLI has its advantages over a GUI.

**Terminal**

- `bash`; open another 'bash' in the same bash window.
- `exit`; close one instance of 'bash'.
- `export`; export variable to the next bash.
	- `export MESSAGE="Hi"`.
	- Variables are associated with one bash. 
	- One change in one bash does not affect the other bash.
- `man <cmd>`; call the manual, help about a command.
	- `man cp`; open the manual about command `cp` (or any other command).
- `cp --help`; command `cp` arguments (or any other command).
- `command cp`; get info on command `cp` (or any other command).
- `type cp`; find where command `cp` is located and what kind of command (an `alias` or `else`) (or any other command).
- `which cp`; locate command `cp` (or any other command).
- `which make`; check out where `make` is. 
- `pwd`; print working directory.
- `dir`; list of directory.
- `up`/`down` arrow; resume a past command.
- `tab`; autocomplete.

**Change dir**

- `cd/aaa`; change to directory `aaa`.
- `cd ~`, `cd ~user`; go back home to `user` directory.
- `cd ..`; go up one level.
- `cd ../..`; go up two levels.
- `cd ../../..`; go up three levels.
- `cd temp`; go to directory `temp`.
- `cd stuff`; if we are in dir `temp`, switch to directory `stuff`.
- `cd temp/stuff`; switch directly to directory `stuff`.
- `cd 'en co re'`; switch to directory `en co re`.

**Make dir**

- `mkdir aaa`; make directory `aaa`.
- `mkdir -p aaa/bbb`; make directory `aaa` with sub-directory `bbb`.
- `mkdir 'en co re'`; make directory `en co re`.

**Remove dir**

- `rmdir aaa`; remove directory `aaa`.
- `rmdir 'en co re'`; remove directory `en co re`.
- `rmdir aaa/bbb`; remove both directory and sub-directory (if both empty).
- `rmdir -p aaa/bbb`; remove all *(you cannot remove a directory if it is non-empty (filled with sub-directories and files))*.
	- `rmdir -p aaa/*`; remove all.

**Switch dir**

- `pushd`; save current location; then, change location (another directory).
- `popd`; return to pushd. *(for example, you are in `aaa`, type `pushd`, go to `bbb`, type `pushb`, go to `ccc`, type `popd`, return to `bbb`, type `popd`, return to `aaa`)*.

**Make file**

- `touch iamcoo.txt`; create an empty text file.
- `touch temp/ismvoo.txt`; create an empty text file in the `temp` directory.

**Edit file**

- `less test.txt`; open the file and display its content.
- Within `less` :
	- `q`; quit.
	- arrows, `pgUp`, `pgDn`; move.
	- `h`; help.
- For other files extensions like `tar` and GNU archive, use `tvf`.

# Manipulation

**List file & dir**

- `ls`; list of directories and files.
- `ls /bin/bash`; list of a remote directory and files.
- `ls -a`; list all.
- `ls -t`; list in alphanumeric order, when they were last modified.
- `ls -l`; list in long format.
- `ls -la`; list all in long format.
- `ls -alt`; list all in long format and ordered.
- `ls /aaa /bbb`; list both directories.
- `ls -r`; list in reverse.
- `ls ../paint/`; list an upper directory.

**Copy file & dir**

- `cp aaa.txt bbb.txt`; copy `aaa.txt` file, paste it or create a copy named `bbb.txt`.
- `cp aaa.txt dir/`; copy `aaa.txt` into directory `dir`.
- `cp aaa.txt bbb.txt dir/`; copy `aaa.txt` and `bbb.txt `into directory `dir`.
- `cp \*.txt dir/`; copy all `.txt` files into directory `dir`.
- `cp aaa.txt dir/dir2`; copy `aaa.txt` into sub-directory `dir2`.
- `cp -r aaa bbb`; copy `dir1`, create a copy names `dir2` with the exact same content.
- `cp -i`; interactive, to prompt the user.
- `cp f\* ../paint/`; copy all files beginning with `f` to an upper directory.

**Wildcards**

- `\*`; wildcard for any string.
- `?`; wildcard for any character.
- `\*.txt`; all files finishing with `.txt`.
- `r\*`; all files beginning with `r`.
- `??a.txt`; all files beginning with two characters + `a.txt`.
- `backup[[:digit:]]`; all file beginning with `backup` + any digit.
- `[abc]\*`; all files beginning with either `a`, `b` or `c`
- `[[:upper:]]\*`; all files beginning with an upper case.
- `\*[![:lower:]]`; all file not finishing with a lower case.

**Move file & dir**

- `mv aaa.txt bbb.txt`; move file or cut `aaa.txt` and paste `bbb.txt`.
- `mv aaa.txt dir/`; move file `aaa.txt` into directory `dir`.
- `mv aaa.txt bbb.txt dir/`; move files `aaa.txt` and `bbb.txt` into directory `dir`.
- `mv \*.txt dir/`; move all `.txt` files into directory `dir`.
- `mv aaa.txt dir/dir2`; move file `aaa.txt` into sub-directory `dir2`.
- `mv -i`; interactive, prompt the user.

**Remove file & dir**

- `rm aaa.txt`; remove file `aaa.txt`.
- `rm test1.txt test2.txt`; remove both files.
- `rm aaa/\*`; remove all files in the directory `aaa`.
- `rm -r aaa`; remove directory `aaa`, must be empty.
- `rm -rf aaa`; remove directory `aaa` and its files.
- `rm -i`; interactive, prompt the user.

# Redirection

- Let's begin by taking a closer look at input and output. In the terminal, after the shell prompt, type :

```bash
$ echo 'Hello'
```

- The `echo` command accepts the string 'Hello' as standard input, and echoes the string `'Hello'` back to the terminal as standard output. 
	- standard input, abbreviated as `stdin`, is information inputted into the terminal through the keyboard or input device.
	- standard output, abbreviated as `stdout`, is the information outputted after a process is run.
	- standard error, abbreviated as `stderr`, is an error message outputted by a failed process.
- Redirection (`>`) reroutes standard input, standard output, and standard error to or from a different location. Type :

```bash
$ echo 'Hello' > hello.txt
```

- Type :

```bash
$ cat hello.txt
```

- The `>` command redirects the standard output to a file. The standard output `'Hello'` is redirected by `>` to the file `hello.txt`, and entered as the standard input.
- The cat command outputs the contents of a file to the terminal. When you type `cat hello.txt`, the contents of `hello.txt` are displayed.

- Type :

```bash
$ ls -l
```

- This is the filesystem we'll work with. Create a file. Type :

```bash
$ touch ocean.txt
```

- Fill the file with values (ocean names). Type :

```bash
$ cat oceans.txt > continents.txt
```

- Use `cat` to view the contents of `continents.txt`. Notice that we only see oceans as output:

```bash
$ cat continents.txt
```

- `>` takes the standard output of the command on the left, and redirects it to the file on the right. Here the standard output of cat `oceans.txt` is redirected to `continents.txt`. Note that `>` OVERWRITES all original content in `continents.txt`. When you view the output data by typing cat on `continents.txt`, you will see only the contents of `oceans.txt`. Type :

```bash
$ cat glaciers.txt >> rivers.txt
```

- Use `cat` to view the contents of `rivers.txt`:

```bash
$ cat rivers.txt
```

- Notice that we see both rivers and glaciers as output. Type:

```bash
$ cat glaciers.txt >> rivers.txt
```

- `>>` takes the standard output of the command on the left and APPENDS it to the file on the right. You can view the output data of the file with cat and the filename. Here, the output data of `rivers.txt` will contain the original contents of `rivers.txt` with the content of `glaciers.txt` appended to it. 

- Type :

```bash
$ touch lakes.txt
```

- Fill the files with values (lake names). Type :

```bash
$ cat < lakes.txt
```

- `<` takes the standard input from the file on the right and inputs it into the program on the left. Here, `lakes.txt` is the standard input for the `cat` command. The standard output appears in the terminal. Let's try some more redirection commands. Type :

```bash
$ touch volcanoes.txt
```

- Fill the files with values (volcano names). Type :

```bash
$ cat volcanoes.txt | wc
```

- You get the count for: lines, words, bytes. Type :

```bash
$ cat volcanoes.txt | wc | cat > islands.txt
```

- Use `cat` to output the contents in `islands.txt`. The next command should now equals `$ cat volcanoes.txt | wc`.

```bash
$ cat volcanoes.txt | wc
```

- `|` is a 'pipe' or 'pipeline' The `|` takes the standard output of the command on the left, and PIPES it as standard input to the command on the right. You can think of this as 'command to command' redirection. Here, again, the output of cat `volcanoes.txt` is the standard input of `wc`. In turn, the `wc` command outputs the number of lines, words, and characters in `volcanoes.txt`, respectively:

```bash
$ cat volcanoes.txt | wc | cat > islands.txt
$ less islands.txt
```

- Multiple `|`s can be chained together. Here the standard output of cat `volcanoes.txt` is 'piped' to the `wc` command. The standard output of `wc` is then 'piped' to cat. Finally, the standard output of cat is redirected to `islands.txt`. You can view the output data of this chain by typing cat `islands.txt`. 
- A few commands are particularly powerful when combined with redirection. Let's try them out. First, use `cat` to output the contents of `lakes.txt`. Then, `sort` it. Type :

```bash
$ cat lakes.txt
$ sort lakes.txt
```

- The lakes in `lakes.txt` are listed in alphabetical order. Type:

```bash
$ cat lakes.txt | sort
```

- `sort` takes the standard input and orders it alphabetically for the standard output. The lakes in `lakes.txt` are listed in alphabetical order.
- Use cat to output the contents of `sorted-lakes.txt`.

```bash
$ cat lakes.txt | sort > sorted-lakes.txt
```

- The command takes the standard output from cat `lakes.txt` and 'pipes' it to sort in ascending order. The standard output of `sort` is redirected to `sorted-lakes.txt`. You can view the output data by typing:

```bash
$ cat sorted-lakes.txt
```

- Type :

```bash
$ touch deserts.txt
```

- Fill the file with values. Type :

```bash
$ cat deserts.txt
$ uniq deserts.txt
```

- You get to see all entries and unique entries.

- Type :

```bash
$ sort deserts.txt | uniq
```

- You get to see  unique entries sorted. Type :

```bash
$ sort deserts.txt | uniq > uniq-deserts.txt
```

- You save the result in `uniq-deserts.txt`.
- Use `cat` to output the contents of `uniq-deserts.txt`.
- `uniq` stands for 'unique' and filters out ADJACENT, duplicate lines in a file. Here `uniq deserts.txt` filters out duplicates of 'Sahara Desert', because the duplicate of 'Sahara Desert' directly follows the previous instance. The 'Kalahari Desert' duplicates are not adjacent, and thus remain.
- Type :

```bash
$ grep Mount mountains.txt
```

- `grep` stands for 'global regular expression print'. It searches files for lines that match a pattern and returns the results. It is also case sensitive. Here, `grep` searches for 'Mount' in `mountains.txt`. Type:

```bash
$ grep -i Mount mountains.txt
```

- `grep -i` enables the command to be case insensitive. Here, `grep` searches for capital or lowercase strings that match 'Mount' in `mountains.txt`. The above commands are a great way to get started with `grep`. If you are familiar with regular expressions, you can use regular expressions to search for patterns in files. `grep` can also be used to search within a directory. Type :

```bash
$ grep -R Arctic /home/ccuser/workspace/geography
```

- ype :

```bash
$ grep -R Arctic /home/ccuser/workspace/geography
```

- `grep -R` searches files in a directory and outputs filenames and lines containing matched results. `-R` stands for 'recursive'. Here `grep -R` searches the `/home/ccuser/workspace/geography` directory for the string 'Arctic' and outputs filenames and lines with matched results. Type:

```bash
$ grep -R Gambino .
```

- `grep -R` searches ALL files recursively and outputs filenames and lines containing matched results.

```bash
$ grep -Rl Arctic /home/ccuser/workspace/geography
```

- `grep -Rl` searches all files in a directory and outputs only filenames with matched results. `-R` stands for 'recursive' and `l` stands for 'files with matches'. Here `grep -Rl` searches the `/home/ccuser/workspace/geography` directory for the string 'Arctic' and outputs filenames with matched results. Use `cat` to display the contents of `forests.txt`. 
- `grep this file.txt`; search for `this` in `file.txt,` print the output on screen.
- `grep this < file.txt`; feed `file.txt` to process `grep` to look for `this`, print on screen
- `grep this file.txt > file_this.txt`; write, overwrite the output in `file_this.txt`.
- `grep this file.txt >> file_this.txt`; write, append the output in `file_this.txt`.
- `grep "is" file.txt`; search pattern `is`, precisely, in words or alone.
- `grep line file.txt`; search pattern `line`.
- `grep -n line file.txt`; show the line number where it finds pattern `line`.
- `grep -i line file.txt`; case insensitive
- `grep -v line file.txt`; inverse or when it does not have the pattern line

- If you search for one "file" in the current directory, type:

```bash
find . _name "file.txt"
```

- `find / _name "file.txt"` searches "file" in multiple directories.
- `find dirA dirB dirC _name "file.txt"` search "file" in one or more directories. Type :

```bash
$ sed 's/snow/rain/' forests.txt
```

- `sed` stands for 'stream editor'. It accepts standard input and modifies it based on an expression, before displaying it as output data. It is similar to 'find and replace'. 
- Let's look at the expression `'s/snow/rain/'`:
	- `s`: stands for 'substitution'. it is always used when using sed for substitution.
	- `snow`: the search string, the text to find.
	- `rain`: the replacement string, the text to add in place.
- In this case, `sed` searches `forests.txt` for the word `'snow'` and replaces it with `'rain'`. Importantly, the above command will only replace the FIRST instance of `'snow'` on a line.

```bash
$ sed 's/snow/rain/g' forests.txt
```

- The above command uses the `g` expression, meaning 'global'. Here `sed` searches `forests.txt` for the word `'snow'` and replaces it with `'rain'`, globally. ALL instances of `'snow'` on a line will be turned to `'rain'`.

- Let's summarize what we've done so far.
- The common redirection commands are:
	- `>`; redirects standard output of a command to a file, overwriting previous content.
	- `>>`; redirects standard output of a command to a file, appending new content to old content.
	- `<`; redirects standard input to a command.
	- `|`; redirects standard output of a command to another command.
- A number of other commands are powerful when combined with redirection commands:
	- `echo 'a'`; display 'a' in the terminal.
	- `touch`; create a file.
	- `cat`; display the content of a file in the terminal.
	- `less`; edit the content of a file in the terminal; prefer `nano`, it's more user-friendly.
	- `sort`; sorts lines in a file in alphabetical order.
	- `uniq`; filters duplicates in a file.
	- `grep`; searches for a text pattern in files and outputs it.
	- `find`; searches for files, not the content.
	- `sed`; searches for a text pattern in files, modifies it, and outputs it.
	- `head`/`tail`; `ls`, but only the top/bottom results.

**Examples**

- `echo 'thisthat'`; show `thisthat`.
- `echo $USER`; show user variable.
- `echo \*`, `d\*`, `s\*`, `[[:upper]]\*`, `/usr/\*/share`; show the content of the current directory according to the specified string (wildcards and characters).
- `echo ~`; show `/home/user`.
- `echo .\*`; show hidden files.
- `echo 2 + 2`; show 2 + 2.
- `echo $((2 + 2))`; show 4.
- `echo $(($((5 \*\* 2)) \* 3))`; show 75.
- `echo Front-{A,B,C}-Back`; show Front-A-Back Front-B-Back Front-C-Back.
- `echo Number-{1...5}`; show Number-1 Number-2 Number-3 Number-4 Number-5.
- `echo {Z...A}`; show Z Y X W…
- `echo a{A{1,2}, B{3,4}}b`; show aS1b aA2b aB3b aB4b.
- `mkdir {2007...2009}-0{1...9} {2007...2009}-{10...12}`; show 2007-01 2007-02 2007-03 2007-04 2007-05 2007-06 2007-07 2007-08 2007-09 2007-10 2007-11 2007-12 2008-01…
- `echo $(ls)`; show, not a list, but a paragraph of files and directories.
- `echo $USER $((2 + 2))`; show user 4.
- `echo $(cal) or echo ' $(cal) '`; show a calendar.
- With `.`, special characters become ordinary characters except for `$`, `\` or `'`; and with `.`, it doesn't suppress commands, variables and aliases as with `.`. Try :
- `echo text ~/\*.txt {a,b} $(echo foo) $((2 + 2))` .
- `echo 'text ~/\*.txt {a,b} $(echo foo) $((2 + 2))'` .
- `echo 'text ~/\*.txt {a,b} $(echo foo) $((2 + 2))'`.
- `print env | less`; show a list of available variables.
- `cat test.txt`; showthe content of file `text.txt`.
- `ls > file.txt`; send command and results into a file, if the file exists, it overwrite it, use `cat file.txt` to edit it.
- `ls >> file.txt`; send command and results into a file, if the file exists, it appends the new content to the existing one, use `cat file.txt` to edit it.
- `cat test.txt > bbb.txt`; write (overwrite) the (existing) content of `test.txt` into `bbb.txt`.
- `cat test.txt >> bbb.txt`; write the content of `test.txt` into `bbb.txt` or append it to `bbb.txt`.
- `wc test.txt`; count lines, words and bytes of `test.txt`.
- `cat test.txt | wc`; show the wc of `test.txt`.
- `cat test.txt | wc > bbb.txt`; write the `wc` of `test.txt` into `bbb.txt`.
- `sort < file.txt`; push the content into command sort.
- `cat < aaa.txt`; open file `aaa.txt` to edit.
- `sort file.txt`; sort the content.
- `cat aaa.txt | sort > sorted_aaa.txt`; in addition, send the results in a new files.
- `uniq file.txt`; extract unique values of the content.
- `ls -l | less`; the list goes into the reader.
- `ls -l | head`; the list shows the 10 top lines only.
- `ls -l | tail`; the list shows the 10 bottom lines only.

# Environment

- Each time we launch the terminal application, it creates a new session. The session immediately loads settings and preferences that make up the command line environment.
- We can configure this environment to support the commands and programs, customize greetings and command aliases, and create variables to share across commands and programs.

- A simple, command line text editor: `nano`. It is more powerful than `less`. Type :

```bash
$ nano hello.txt
```

- In `nano`, at the top of the window, type :

```bash
$ 'Hello, I am nano.'
```

- Using the menu at the bottom of the terminal for reference, type ++ctrl+o++ (the letter, not the number) to save the file. Press ++enter++, when prompted about the filename to write. Then type ++ctrl+x++ to exit `nano`. Finally, type `clear` to clear the terminal window. The command prompt should now be at the top of the window. You just edited a file in the `nano` text editor. Type:

```bash
$ nano hello.txt
```

- `nano` is a command line text editor. It works just like a desktop text editor, except that it is accessible from the command line and only accepts keyboard input. The command `nano hello.txt` opens a new text file named `hello.txt` in the `nano` text editor. 'Hello, I am nano' is a text string entered in `nano` through the cursor.
- The menu of keyboard commands at the bottom of the window allow us to save changes to `hello.txt` and exit `nano`. The `^` stands for the ++ctrl++ key.
	- ++ctrl+o++ saves a file. `o` stands for output.
	- ++ctrl+x++ exits the `nano` program. `x` stands for exit.
	- ++ctrl+g++ opens a help menu.
	- `Clear` clears the terminal window, moving the command prompt to the top of the screen.
- [nano editor](http://www.nano-editor.org/)
- Now that you are familiar with editing text in `nano`, let's create a file to store environment settings. Type :

```bash
$ nano ~/.bash_profile
```

- This opens up a new file in `nano`. In `~/.bash_profile`, at the top of the file, type :

```bash
$ echo 'Welcome, Jane Doe'
```

- You can use your name in place of 'Jane Doe'. Type ++ctrl+o++ to save the file. Press ++enter++ to write the filename. Type ++ctrl+x++ to exit. Finally, type `clear` to clear the terminal window. Type :

```bash
$ source ~/.bash_profile
```

- You should see the greeting you entered. You created a file in `nano` called `~/.bash_profile` and added a greeting.

```bash
$ nano ~/.bash_profile
```

- `~/.bash_profile` is the name of file used to store environment settings. It is commonly called the 'bash profile'. When a session starts, it will load the contents of the bash profile before executing commands.
	- The `~` represents the user's home directory.
	- The `.` indicates a hidden file.
- The name `~/.bash_profile` is important, since this is how the command line recognizes the bash profile.
- The command `nano ~/.bash_profile` opens up `~/.bash_profile` in `nano`. The text echoes 'Welcome, Jane Doe' and creates a greeting in the bash profile, which is saved. It tells the command line to echo the string 'Welcome, Jane Doe' when a terminal session begins. The command source `~/.bash_profile` ACTIVATES the changes in `~/.bash_profile` for the current session.
- Now that we know what bash profile is, let's continue configuring the environment by adding command aliases. Open `~/.bash_profile` in `nano`. In `~/.bash_profile`, beneath the greeting you created, type :

```bash
$ alias pd='pwd'
```

- Save the file. Press ++enter++ to write the filename. Exit `nano`. Clear the terminal window.
- In the command line, use the source command to activate the changes in the current session.

```bash
$ source ~/.bash_profile
```

- Let's try out the alias. Type :

```bash
$ pd
```

- You should see the same output as you would by typing the `pwd` command. What happens when you store this alias in `~/.bash_profile`?

```bash
$ alias pd='pwd'
```

- The alias command allows you to create keyboard shortcuts, or aliases, for commonly used commands. Here alias `pd='pwd'` creates the alias `pd` for the `pwd` command, which is then saved in the bash profile. Each time you enter `pd`, the output will be the same as the pwd command. The command source `~/.bash_profile` makes the alias `pd` available in the current session. Each time we open up the terminal, we can use the `pd` alias.
- Let's practice aliases some more. Open `~/.bash_profile` in `nano`. In the bash profile, beneath the previous alias, add :

```bash
$ alias hy='history'
```

- Save the file. Press ++enter++ to write the filename.
- Add another alias:

```bash
$ alias ll='ls -la'
```

- Save the file.
- Press ++enter++ to write the filename.
- Exit `nano`.
- Clear the terminal window.
- In the command line, use source to activate the changes to the bash profile for the current session.
- Let's try out the aliases. Type:

```bash
$ hy
```

- What happens when you store the following aliases in `~/.bash_profile`?

```bash
$ alias hy='history'
```

- `hy` is set as alias for the history command in the bash profile. The alias is then made available in the current session through source. By typing `hy`, the command line outputs a history of commands that were entered in the current session. Type:

```bash
$ alias ll='ls -la'
```

- `ll` is set as an alias for `ls -la` and made available in the current session through source. By typing `ll`, the command line now outputs all contents and directories in long format, including all hidden files.
- Now that you are familiar with configuring greetings and aliases, let's move on to setting environment variables.
- Open `~/.bash_profile` in `nano`.
- In the bash profile, beneath the aliases, on a new line, type:

```bash
$ export USER='Jane Doe'
```

- Feel free to use your own name. Save the file. Press ++enter++ to write the filename. Exit `nano`. Finally, clear the terminal.
- In the command line, use source to activate the changes in the bash profile for the current session. Type :

```bash
$ echo $USER
```

- This should return the value of the variable that you set. What happens when you store this in `~/.bash_profile`?

```bash
$ export USER='Jane Doe'
```

- Environment variables are variables that can be used across commands and programs and hold information about the environment. The line `USER='Jane Doe'` sets the environment variable `USER` to a name `'Jane Doe'`. Usually the `USER` variable is set to the name of the computer's owner. The line export makes the variable to be available to all child sessions initiated from the session you are in. This is a way to make the variable persist across programs. At the command line, the command echo `$USER` returns the value of the variable. Note that `$` is always used when returning a variable's value. Here, the command echo `$USER` returns the name set for the variable.
- Let's learn a few more environment variables, starting with the variable for the command prompt. Open `~/.bash_profile` in `nano`. On a new line, beneath the last entry, type

```bash
$ export PS1='>> '
```

- Save the file. Press ++enter++ to write the filename. Exit `nano`. Finally, clear the terminal window. In the command line, use source to activate the changes in the bash profile for the current shell session. Let's try out the new command prompt. Type :

```bash
$ echo 'hello'
```

- Type :

```bash
$ ls -alt
```

- Did you notice that the prompt has changed? What happens when this is stored in `~/.bash_profile`?

```bash
$ export PS1='>> '
```

- `PS1` is a variable that defines the makeup and style of the command prompt.
- `echo $PS1` prints the variable.
- `PS1="value"` changes the variable value.
- `PS1='>> '` sets the command prompt variable and exports the variable. It makes the variable available in all sub programs of the current shell. Here we change the default command prompt from `$` to `>>`. After using the source command, the command line displays the new command prompt. Let's learn about two more environment variables. Type :

```bash
$ echo $HOME
```

- This returns the value of the `HOME` variable. What happens when you type this command?

```bash
$ echo $HOME
```

- The `HOME` variable is an environment variable that displays the path of the home directory. Here by typing echo `$HOME`, the terminal displays the path `/home/ccuser` as output. `cd $HOME` goes to the home directory. You can customize the `HOME` variable if needed, but in most cases this is not necessary. In the command line, type :

```bash
$ echo $PATH
```

- Type :

```bash
/bin/pwd
```

- Type :

```bash
/bin/ls
```

- What happens when you type this command?

```bash
$ echo $PATH
/home/ccuser/.gem/ruby/2.0.0/bin:/usr/local/sbin:/usr/local/bin:/usr/bin:/usr/sbin:/sbin:/bin
```

- `PATH` is an environment variable that stores a list of directories separated by a colon. Looking carefully, echo `$PATH` lists the following directories:
	- `/home/ccuser/.gem/ruby/2.0.0/bin`.
	- `/usr/local/sbin`.
	- `/usr/local/bin`.
	- `/usr/bin`.
	- `/usr/sbin`.
	- `/sbin`.
	- `/bin`.
- Each directory contains scripts for the command line to execute. The `PATH` variable simply lists which directories contain scripts. For example, many COMMANDS we've learned are scripts stored in the `/bin` directory.

```bash
$ /bin/pwd
```

- This is the script that is executed when you type the `pwd` command.

```bash
$ /bin/ls
```

- This is the script that is executed when you type the ls command. In advanced cases, you can customize the `PATH` variable when adding scripts of your own. Type :

```bash
$ env
```

- Type :

```bash
$ env | grep PATH
```

- What happens when you type this command?

```bash
$ env
```

- The `env` command stands for 'environment', and returns a list of the environment variables for the current user. Here, the `env` command returns a number of variables, including `PATH`, `PWD`, `PS1`, and `HOME`.

```bash
$ env | grep PATH
$ env | grep aliasname
```

- `env | grep PATH` is a command that displays the value of a single environment variable. Here the standard output of env is 'piped' to the `grep` command. `grep` searches for the value of the variable `PATH` and outputs it to the terminal. You learned to use the bash profile to configure the environment. What can we generalize so far? The environment refers to the preferences and settings of the current user.

-----
- Let's summarize what we've done so far.
- The `nano` editor is a command line text editor used to configure the environment.
- `~/.bash_profile` is where environment settings are stored. You can edit this file with `nano`.
- Environment variables are variables that can be used across commands and programs and hold information about the environment.
- `export VARIABLE='Value'` sets and exports an environment variable.
- `USER` is the name of the current user.
- `PS1` is the command prompt.
- `HOME` is the home directory. It is usually not customized.
- `PATH` returns a colon separated list of file paths. It is customized in advanced cases.
- `echo $PATH` prints the path.
- `PATH="value"` changes the path..
- `export PATH=/home/dir/bin:$PATH` appends the new path to environment variable PATH.
- `env` returns a list of environment variables.

# Multi-Users

- Linux is multi-user : multiple users at the same time as opposed to OS X or Windows; just like the UNIX mainframe computers with terminals, users and superuser concepts. 

**Access rights**

- Type :

```bash
$ ls -l
```

- Read, from left to right :
	- `–` or `d`: file or dir.
	- File or dir name.
	- Owner access (`r w x…-`).
	- Group access (`r w x…-`).
	- All access (`r w x…-`).
	- Owner group, size, date.

- How do we change the acces rights? With `chmod`.
- First, there are access right for:
	- `u` ser.
	- `g` roup.
	- `o` thers.
- Second, there levels. Each level has a numeric value.:
	- `r` ead: 4.
	- `w` rite: 2.
	- `x` ecute: 1.
For example, using levels:
	- `o+w`: others can write the file (create).
	- `u+x`: users can execute the file.
	- `g-x`: group can no longer execute the file.
	- etc.
	- `chmod o+w file1.txt` for example.

Why numeric value? It an alternative way for `chmod` to assign access rights. Levels are ranked with values:

| Level | Binary | Decimal |
|-----|:-:|:-:|
|r w x|111| 7 |
|r w -|110| 6 |
|r - -|100| 4 |
|- - -|000| 0 |
|r - x|101| 5 |

- A `7` grants full rights vs a `0` that grants no rights. For example:
	- `chmod 600 file`; change the file access rights to `rw- --- ---`.
	- `chmod 600 dir`; change the directory access rights.
- How are the values calculated?

```bash
r+w+x = 4+2+1 = 7
r     = 4     = 4
    x =     1 = 1
r+w   = 4+2   = 6
...
...
```
Once you have the values, you can set the access rights:

```bash
 u   g   o  
--- --- ---
rwx rw- --x
 7   6   1
```

- Therefore, `chmod 761` set the access rights `rwx rw- --x` to a file, files, a directory or directories.

**Ownership**

- `chown thou file`; assign a new owner, `thou`, to 'file'.
- `chown thou dir`; ... to dir.
- `chgrp newgr file` assign a new group owner, `newgr`, to 'file'.
- `chgrp newgr dir`; ... to dir.

**Superuser**

- `su`; superuser login.
- `su file`; unlock the file with the superuser password.
- `sudo`; do it with the privilege of a superuser.
- `sudo apt-get update`; updates the database.
- `sudo apt-get upgrade`; upgrades all packages (update before upgrading).
- `sudo apt-get install build-essential`; install a useful package (or any other package).
- `sudo apt-get install git`; install 'git'.
- `which git`; find where 'git' is located (if it's instaled).
- `sudo apt-get remove git`; remove 'git'.
- `sudo apt-get purge git`; remove 'git' and purge any remainings.
- `sudo chnow user file`; change the owner.

# Multi-Tasks

- Linux is multi-task; multiple tasks can run at the same time like OS X or Windows or UNIX; Linux kernel runs processes; they take turns at the processor(s). All programs and processes can be launched/killed from the GUI and the CLI.

**Show**

- `top`; show process dashboard by PID number; `?` for help, `q` for quit.
- `ps`; show the process list.
	- `ps aux`; show all process.
	- `ps aux | grep 'top'`; filter top processes.
	- `ps aux | grep bash`; filter processes related to the bash.
	- `ps aux | grep bash | sort`; ... and sort them.

**Manage**

- ++ctrl+z++; pause a process, put it in the background.
- `fg`; foreground, bring back the process.
- `jobs`; list paused processes.
- `fg #PID`; bring back process #PID (if there is more than one process on pause, you must identify the process).
- ++ctrl+c++; terminate the active process.
- `xload`; display the system load in a new windows, but jam the current terminal (open another or several terminals then).
- `xload &`; runs in the background
- ++ctrl+x++`; suspend the process and unjam the terminal.
- `by`; resume the process.
- `ps`; show processes and their #PID.
- `ps x | grep bad_program`; find the bad processes.
- `kill` can send a signal from the OS to a process. For example : when you log off, you send a signal to terminate a word processing program and save the file before closing.
	- `kill #PID`; kill the process.
	- `kill -STOP #PID`; pause the process.
	- `kill -TERM #PID`;  terminate the process.
	- `kill -SIGTERM #PID`;  terminate the process.
	- `kill -SIGKILL #PID`; kill the process.
	- `kill -KILL`; force closing of the current process.
	- `kill -9 #PID`;  force closing the process.
- Killing sequence:
	- `kill #PID`; doesn't work…
	- `kill -9 #PID`, or..
