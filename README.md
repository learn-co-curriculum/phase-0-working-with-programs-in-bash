# Working with Programs in Bash

## Learning Goals

* View file contents with `cat` and `open`
* Print `String`s with `echo`
* Set `PATH` and environment variables
* Look up Bash documentation with `man`

## Introduction

Sometimes when we interact with computers via the graphical user interface
(GUI), it takes several clicks or deep dives into the controls to accomplish
what we want. We've started to see in the earlier lessons that interacting via
the command line interface (CLI) can give us more direct actions and valuable
shortcuts. As we begin to build applications, it will become more important to
be familiar with these tasks related to modifying files, reading output, and
working with programs. The terminal has a number of useful commands that can
display running processes, kill them, and change their priority level.

## View File Contents With `cat` and `open`

We can print the contents of a file by using the `cat` command. Entering `$ cat
[filename]` (from "con**cat**enate") reads a file and prints the content to your
command line.

The `open` command is interesting because it will trigger the default action
associated with the file type. So `$ open .` will popup a finder window with the
current directory in finder (because `.` is an alias to the current directory).
Entering `$ open hello_world.rb` will open that file in your default editor.

## Print `String`s With `echo`

Developers will often find themselves needing to write text in the terminal. The
`echo` command has a number of uses -- probably most commonly used to have a
shell script display a message or instructions, such as "Please enter Y or N" in
an interactive session with users.

The `echo` command takes a string and prints it to the screen. You can redirect
output into a file: ``` echo "I'm printing to the screen" >> [filename]```.

This is called _redirection_. We're "redirecting" what we see on the monitor
into a file. The `>>` symbol will append content into the file while `>` means
overwrite.

You can also use echo in place of `ls` in certain scenarios. For example, to
list all `.rb` files in the current directory, you can execute the following
command: `echo *.rb`.

## Set `PATH` and Environment Variables

An _environment variable_ which can be used by multiple applications or
processes, is a variable with a name and an associated value that can be used
for anything like the location of executable files, libraries, current working
directory, default shell, or local system settings.

If you run the command `printenv`, you will see a list all the environment
variables currently set.

For displaying the value of any specific environment variable run the echo
$[variable name] on the terminal, as shown below.

For exampple, `PATH` is an environment variable. Programs might be installed in
many different directories. Directories whose names are listed in the `PATH`
variable can have its programs run without having to `cd` to the directory where
they are to run them.

Let's try viewing the current `PATH`.

```bash
echo $PATH
/Users/kellyegreene/.rvm/gems/ruby-2.4.1/bin:/Users/kellyegreene/.rvm/gems/ruby-2.4.1@global/bin:/Users/kellyegreene/.rvm/rubies/ruby-2.4.1/bin:/Users/kellyegreene/.nvm/versions/node/v8.9.4/bin:/Applications/Postgres.app/Contents/Versions/9.4/bin:/usr/local/share/npm/lib/node_modules/grunt-cli/bin:/usr/local:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/kellyegreene/Library/Android/sdk/tools:/Users/kellyegreene/Library/Android/sdk/platform-tools:/Users/kellyegreene/Library/Android/sdk/tools:/Users/kellyegreene/Library/Android/sdk/platform-tools:/Users/kellyegreene/.rvm/bin
```

Let's save this `PATH` to `BACKUP_PATH` using `export`.

```bash
export BACKUP_PATH="/Users/kellyegreene/.rvm/gems/ruby-2.4.1/bin:/Users/kellyegreene/.rvm/gems/ruby-2.4.1@global/bin:/Users/kellyegreene/.rvm/rubies/ruby-2.4.1/bin:/Users/kellyegreene/.nvm/versions/node/v8.9.4/bin:/Applications/Postgres.app/Contents/Versions/9.4/bin:/usr/local/share/npm/lib/node_modules/grunt-cli/bin:/usr/local:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/kellyegreene/Library/Android/sdk/tools:/Users/kellyegreene/Library/Android/sdk/platform-tools:/Users/kellyegreene/Library/Android/sdk/tools:/Users/kellyegreene/Library/Android/sdk/platform-tools:/Users/kellyegreene/.rvm/bin"
```

Now if something were to happen to our original `PATH` variable, we can restore
it from `BACKUP_PATH`.

There are a lot of environment variables and, as you grow as a developer, you
will likely encounter some of them. Others you might see include:

* Execution mode (e.g., production, development, staging, etc.)
* Domain names
* API URL/URIs

We can also add our own directories to the path so that our programs can be found
when we run them.

**Top Tip:** *If you want to find out where the program being run is located
when you type a command at the command line, use the which command; entering* `$
which ruby` *will tell you where the Ruby binary is located.* Whenever you type
a command the path is going to be searched in order until it finds an executable
that matches name

## Look Up Bash Documentation With `man`

The `man` command is the key to command line wisdom. It brings up a **man**ual
pages for almost any command. It's the equivalent of a help system for the
command line.

For example, if you're curious what the options on `ps` mean, you can go to your
terminal and enter:

```bash
$ man ps
```

In the terminal output, read about what the `a` and `u` options do. Notice that
the `x` option is a suffix on the `a` option. The `man` command reveals very
useful reference documentation on the various bash commands. You'll notice that
your command prompt has disappeared. Don't panic! You're just inside the
documentation. Enter `$ q` ("**q**uit") to return to your command prompt.

## Conclusion

Software developers still rely heavily on command-line interfaces to perform
tasks more efficiently, configure their machine, or access programs and program
features that are not available through a graphical interface. File interactions
and process management may be difficult for new CLI users to grasp because the
tools used are different from their graphical counterparts. However, the ideas
are familiar and intuitive, and with a little practice, will become natural.
Because these tasks are involved in everything you will do in software
development, learning how to effectively work with them is an essential skill.

## Resources

* [Using The Terminal Command ‘cat’ To View The Contents Of Files](http://www.mactricksandtips.com/2012/07/using-the-terminal-command-cat-to-view-the-contents-of-files.html)
