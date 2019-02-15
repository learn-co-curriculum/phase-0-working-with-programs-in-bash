# CLI Essentials: Basic Commands in Bash (Continued)

## Learning Goals

* Demonstrate interacting with files
* Demonstrate running and killing processes

## Introduction

Bash is a text-based interpreter for controlling your computer (or operating system).
Bash is actually an acronym which stands for **B**ourne-**A**gain **SH**ell. It replaced
the Bourne shell and "bashed together" the unix programs sh, csh and ksh. From it you can
navigate the files on your computer and execute programs.

You can also connect to other computers and basically do everything you can do in your GUI
Operating System (like OS X or Windows).

When you open a terminal, you're basically within your file system, or in a directory, just
like you are when you open a Finder window or an Explorer window.

## Demonstrate Interacting With Files

### Printing `String`s With `echo`

The echo command takes a string and prints it to the screen. You can redirect output
into a file:
``` echo “I’m printing to the screen” >> visible```

### Viewing File Contents With `cat` and `open`

We have a lot of commands available to us. Useful ones include `open` and `cat`

The `open` command is interesting because it will trigger the default action associated with
the file type. So `$ open .` will popup a finder window with the current directory in finder
(because remember that `.` is an alias to the current directory). Entering `$ open hello_world.rb`
will open that file in your default editor.

We can print the contents of a file by using the `cat` command. Entering `$ cat [file-name]`
(from "con**cat**enate") reads a file and prints the content to your command line.

### Use `shebang`

We can use shebang so bash knows how to run our program. When we try to run the program without
changing its permissions it tells us that the command is not found. It's only after we add the
executable flag to it that it runs like a normal program does.

### PATH and Environment Variables

The `PATH` variable gives the computer an ordered list of directories to search in to find an
executable with he name you typed.  In our case, it's going to search for the `ls` executable.
If you type `$ ls /bin`, you'll see that this is an actual program or "binary" which is why it's
usually found in the `bin` directory (short for "**bin**ary").  If you're trying to run a ruby
program and typing `$ ruby myprogram.rb` the computer goes through all the files in the path
until it finds an executable called `ruby` and then runs that code with the provided argument
(`myprogram.rb`).  If you type `$ echo $PATH` you can see what your path is.  If you're using
[RVM](https://rvm.io/) (if you don't know what this is at the moment don't worry), it will look
something like this:

```
/Users/blake/.rvm/gems/ruby-1.9.3-p392/bin:/Users/blake/.rvm/gems/ruby-1.9.3-p392@global/bin:/Users/blake/.rvm/rubies/ruby-1.9.3-p392/bin:/Users/blake/.rvm/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/bin:/usr/local/sbin:/Users/blake/bin:/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin
```
(This code box is scrollable to the right.)

Each directory in the path is separated by the `:` ("colon") symbol.

If you ever get errors where you type something in the terminal and it says it can't be found,
the executable you're trying to run needs to be added to the path. If the wrong executable is
getting run, the order of directories in your path is wrong.

The PATH variable is an environmental variable. These are variables you can set specific to your
computer's environment which can then be used in other programs. For example, in Ruby you can type
`ENV[name_of_variable]` to access an environmental variable. These are typically set in your bash
profile, in a bash script, or at the command line.

**Tip:** *If you want to find out where the program being run is located when you type a command at the command line, use the which command; entering* `$ which ruby` *will tell you where the Ruby binary is located.*
Whenever you type a command the path is going to be searched in order until it finds an executable
that matches name

We can add our own directories to the path so that our programs can be found when we run them 

Here we add the bash review bin folder to our path by using the export keyword and then attaching
the current path to the end of it

by doing this no matter where we go we can run our program.

## Demonstrate Running and Killing Processes

### Executing Programs

From within a shell you can also execute programs. Navigate to where you saved your `hello_world.rb`
file and try:

```bash
$ ruby hello_world.rb
```

This command is no different than the `cd` command. We're executing the `ruby` program by supplying
a path to a file to execute. Because the `hello_world.rb` file you just created is completely empty
and has no contents inside of it, there is no program to run and your terminal won't actually
produce any output when you tried running it via `ruby hello_world.rb`.

### Working with Running Processes Using `ps`

Entering `$ ps` lists the current **p**roce**s**ses being run by your terminal.

We can look for them using the `ps` command with the flag `aux` 

We can also use the `pkill` command and give it the name of the process to stop running. This uses both
techniques of looking for a process and then killing it if it finds it. 

### Piping "|"

Piping, a verb derived from the `|` symbol named "pipe", will send the output of one command into
the input of another command.
The most common command you'll probably use is piping the **p**roce**s**s list to
[grep](http://en.wikipedia.org/wiki/Grep) to search for a running program.

```bash
$ ps aux | grep ruby
```

This would run the `ps` command with the `a`, `u`, and `x` options and send the output of that to
`grep` (a search utility), which would then search for the term "ruby". You'll notice that `ps`
is one of the commands that only accepts options *without* a flag. Try:

```bash
$ ps -aux
```
If you're on OS X, you should have gotten an error — something like `ps: No user named 'x'`. Just
keep in mind which commands take options *with* a flag (`-`) and which take options *without* a flag.

### Looking Up Bash Documentation With `man`

If you're curious what the options on `ps` mean, enter:

```bash
$ man ps
```

Read about what the `a` and `u` options do. Notice that the `x` option is a suffix on the `a` option.
The `man` ("**man**ual") command reveals very useful reference documentation on the various bash commands.
You'll notice that your command prompt has disappeared. Don't panic! You're just inside the documentation.
Enter `$ q` ("**q**uit") to return to your command prompt.

## Conclusion

## Resources

- [Lifehacker on the Command Line](http://lifehacker.com/5633909/who-needs-a-mouse-learn-to-use-the-command-line-for-almost-anything)
- [Environment Variables](http://cbednarski.com/articles/understanding-environment-variables-and-the-unix-path/)
- [Built-in Shell Commands](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html) *Very useful*
- [15 Useful Bash Commands](http://www.thegeekstuff.com/2010/08/bash-shell-builtin-commands/)thegeekstuff.com/2010/08/bash-shell-builtin-commands/)