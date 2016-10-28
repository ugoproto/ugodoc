# Command Shell Snippets

Sort in alphabetical order:

```bash
$ sort myfile.txt
```

Sort in numerical order:

```bash
$ sort -n myfile.txt
```

Sort on multiple column (on column 2 in numerical order, then on column 1 in alphabetical order):

```bash
$ sort myfile.txt -k2n -k1
```

Sort a comma-separated table:

```bash
$ sort -k2 -k3 k1 -t ',' myfile.txt
```

Sort in reversed order:

```bash
$ sort -r myfile.txt
```

Sort a pip-separated file in reverses order by the second column:

```bash
$ sort myfile.txt -nrk 2 -st '|'
```

Search text files for lines matching regular expressions (regex) with `grep <'matching string'> <source>`:

```bash
$ grep ArticleTitle webpage.html
```

An asterisk (`*`) indicates any character (the matching expression starts with 'Ar' and ends with 'le'):

```bash
$ grep Ar*le mytext.txt
```

Search for starting metacharacter `>`:

```bash
$ grep ^'>' mytext.txt
```

List the access rights for all files:

```bash
$ ls -lag
```

Run commands in background,
kill the job running in the foreground,
suspend the job running in the foreground, and
background the suspended job:

```bash
$ command &

$ ^C

$ ^Z

$ bg
```

List the current jobs,
foreground job number 1, and
kills job number 1:

```bash
$ jobs

$ fg%1

$ kill%1
```

List current processes, and
kill process number 26152:

```bash
$ ps

$ kill 26152
```

Help about commands:

```bash
$ man <command name>

$ whatis <command name>
```