# CLI Essentials: Working with Programs in Bash

## Learning Goals

* Demonstrate interacting with files
* Demonstrate running and killing processes

## Introduction

The command-line interface gives us access to all of the computer's
capabilities with fewer clicks or or deep-dives into the graphical user
interface (GUI) &mdash; if these interactions are available in the GUI at all.

While we've learned how to travel our file system and create empty files and
directories, we want to start working with tools that allow us to create,
update, and even run programs. Traditionally you used the Finder and
double-clicking to launch or edit files. You can do the same work, as usual,
faster, using the CLI.

You can capture output to new files and even kill programs that have hung and
are making your laptop's fan sound like a plane taking off.

## Demonstrate Interacting With Files

### Printing `String`s With `echo`

The `echo` command takes a string and prints it to the screen. You can redirect
output into a file:

KG: expand out, show simple echo THEN show echo redirect, also rm smart curly-quotes
here.

``` echo “I’m printing to the screen” >> visible```

KG: That `>>` is called "redirection" we're "redirecting" what we saw on the
monitor "into" a file. `>>` means append while `>` means overwrite.

### Viewing File Contents With `cat` and `open`

You've already seen us use `cat` to see what was in an empty file. Let's use it
to see what's in `visible`

`cat visible`

The `open` command, available on Mac OSX, is interesting because it will
trigger the default action associated with the file type. So `$ open .` will
popup a Finder window with the current directory in finder (because remember
that `.` is an alias to the current directory).

Entering `$ open hello_world.rb` will open that file in your default editor:
the program that you use to write Ruby code. You'll be writing this one a lot
in the future!

KG: integrate this para above
We can print the contents of a file by using the `cat` command. Entering `$ cat
[file-name]` (from "con**cat**enate") reads a file and prints the content to
your command line.


KG: (no no no no no, not yet) we've not introduced permissions, chmod,
executables, no.
### Use `shebang`

We can use shebang so bash knows how to run our program. When we try to run the
program without changing its permissions it tells us that the command is not
found. It's only after we add the executable flag to it that it runs like a
normal program does.

### PATH and Environment Variables

KG: Needs a lot more setup. We've not discussed envvars yet we also probably
need to provide an example.....

Let's keep this _SIMPLE_

1. env vars exist, shells can be configured, and one of those ways is thru env
   vars
2.  PATH is one. Programs might be installed in many different directories.
    Directories whose names are listed in the PATH variable can have this
    programs run without you haveing to `cd` to the directory where they are to
    run them
3. Let's save our PATH to BACKUP_PATH\
4. Now let's export PATH=""
5. show everything is broken
6. restore path from backup path
7. blah blah, take away is PATH is a very important env var, there are many
   more but they're working to help your hsell experience along, etc.

KG: Trash this para. below

The `PATH` variable gives the computer an ordered list of directories to search
in to find an executable with he name you typed.  In our case, it's going to
search for the `ls` executable. If you type `$ ls /bin`, you'll see that this is
an actual program or "binary" which is why it's usually found in the `bin`
directory (short for "**bin**ary").  If you're trying to run a ruby program and
typing `$ ruby myprogram.rb` the computer goes through all the files in the path
until it finds an executable called `ruby` and then runs that code with the
provided argument (`myprogram.rb`).  If you type `$ echo $PATH` you can see what
your path is.  If you're using [RVM](https://rvm.io/) (if you don't know what
this is at the moment don't worry), it will look something like this:

```
/Users/blake/.rvm/gems/ruby-1.9.3-p392/bin:/Users/blake/.rvm/gems/ruby-1.9.3-p392@global/bin:/Users/blake/.rvm/rubies/ruby-1.9.3-p392/bin:/Users/blake/.rvm/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/bin:/usr/local/sbin:/Users/blake/bin:/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin:/Applications/Xcode.app/Contents/Developer/usr/bin
```
(This code box is scrollable to the right.)

Each directory in the path is separated by the `:` ("colon") symbol.

KG: Trashthis
If you ever get errors where you type something in the terminal and it says it
can't be found, the executable you're trying to run needs to be added to the
path. If the wrong executable is getting run, the order of directories in your
path is wrong.

KG: Trashthis
The PATH variable is an environmental variable. These are variables you can set
specific to your computer's environment which can then be used in other
programs. For example, in Ruby you can type `ENV[name_of_variable]` to access an
environmental variable. These are typically set in your bash profile, in a bash
script, or at the command line.

KG: keep this
**Tip:** *If you want to find out where the program being run is located when
you type a command at the command line, use the `which` command; entering* `$
which ruby` *will tell you where the Ruby binary is located.* You can use that
information to `cd` over to is and `ls -l` it and learn more about your system.
Whenever you type
a command the path is going to be searched in order until it finds an executable
that matches name

KG: I dont' mind this...
We can add our own directories to the path so that our programs can be found
when we run them 

KG: but not this...too early
Here we add the bash review bin folder to our path by using the export keyword
and then attaching the current path to the end of it

by doing this no matter where we go we can run our program.

## Demonstrate Running and Killing Processes

Generally, an application process' lifecycle has three main states: start, run,
and stop. Each state can and should be managed carefully. These eight commands
can be used to manage processes through their lifecycles.

### Executing Programs

From within a shell you can also execute programs. Navigate to where you saved
your `hello_world.rb` file and try:

```bash
$ ruby hello_world.rb
```

This command is no different than the `cd` command. We're executing the `ruby`
program by supplying a path to a file to execute. Because the `hello_world.rb`
file you just created is completely empty and has no contents inside of it,
there is no program to run and your terminal won't actually produce any output
when you tried running it via `ruby hello_world.rb`.

### Working with Running Processes Using `ps`

Entering `$ ps` lists the current **p**roce**s**ses being run by your terminal.

We can look for them using the `ps` command with the flag `aux` 

We can also use the `pkill` command and give it the name of the process to stop
running. This uses both techniques of looking for a process and then killing it
if it finds it.

KG: Not sure we need this....it's very cool..but...it's so confusing, this is
our BASIC population...

### Piping "|"

Piping, a verb derived from the `|` symbol named "pipe", will send the output of
one command into the input of another command. The most common command you'll
probably use is piping the **p**roce**s**s list to
[grep](http://en.wikipedia.org/wiki/Grep) to search for a running program.

```bash
$ ps aux | grep ruby
```

This would run the `ps` command with the `a`, `u`, and `x` options and send the
output of that to `grep` (a search utility), which would then search for the
term "ruby". You'll notice that `ps` is one of the commands that only accepts
options *without* a flag. Try:

```bash
$ ps -aux
```
If you're on OS X, you should have gotten an error — something like `ps: No user
named 'x'`. Just keep in mind which commands take options *with* a flag (`-`)
and which take options *without* a flag.

### Looking Up Bash Documentation With `man`

If you're curious what the options on `ps` mean, enter:

```bash
$ man ps
```

Read about what the `a` and `u` options do. Notice that the `x` option is a
suffix on the `a` option. The `man` ("**man**ual") command reveals very useful
reference documentation on the various bash commands. You'll notice that your
command prompt has disappeared. Don't panic! You're just inside the
documentation. Enter `$ q` ("**q**uit") to return to your command prompt.

## Conclusion

Software developers still rely heavily on command-line interfaces to perform
tasks more efficiently, configure their machine, or access programs and program
features that are not available through a graphical interface. File interactions
and process management may be difficult for new CLI users to grasp because the
tools used are different from their graphical counterparts.

However, the ideas are familiar and intuitive, and with a little practice, will
become natural. Because these tasks are involved in everything you will do in
software development. Learning how to effectively work with them is an essential
skill.

## Resources
* [Using The Terminal Command ‘cat’ To View The Contents Of Files](http://www.mactricksandtips.com/2012/07/using-the-terminal-command-cat-to-view-the-contents-of-files.html)
* [On the Shebang](https://scriptingosx.com/2017/10/on-the-shebang/)
* [How to View and Kill Processes Using the Terminal in Mac OS X](https://www.chriswrites.com/how-to-view-and-kill-processes-using-the-terminal-in-mac-os-x/)
* [HOW TO VIEW AND KILL PROCESSES ON YOUR MAC](https://setapp.com/how-to/how-to-view-and-kill-processes-on-mac)
