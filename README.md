# Working with Programs in Bash

## Learning Goals

- View file contents with `cat` and `open`
- Print text with `echo`
- Redirect text
- Set `PATH` and environment variables
- Look up Bash documentation with `man`

## Introduction

Sometimes when we interact with computers via the graphical user interface
(GUI), it takes several clicks or deep dives into the controls to accomplish
what we want. We've started to see in the earlier lessons that interacting via
the command line interface (CLI) can make us faster!

As we begin to build applications, it will become important to also
be familiar with tasks related to displaying files, editing them with
a code editor, or getting information from the operating system.

## View File Contents With `cat` and `open`

We can print the contents of a file by using the `cat` command. Entering
`$ cat filename` reads a file and prints the content to your command line. (In
the previous command `filename` is just a placeholder for where you would
write out a valid file name).

> **ASIDE**: `cat` comes from `catenate` a middle-English word that means "make
> like a chain". Unix thinks of a file as a "chain of bytes" that it feeds to
> the screen.

**Note:** _Any time you see the_ `$` _character, you shouldn't type it in. This
is just a standard way to represent a bash prompt. Yours may or may not be a_
`$`.

The `open` command is interesting because it will trigger the default action
associated with the file type. "Default actions" are defined by the operating
system. This command is only available on Mac OSX.

`$ open .` will popup a Finder window with the current directory in finder
(recall: `.` is an alias to the current directory). Entering
`$ open hello_world.rb` will run the default program for files of a "Ruby" type
— usually a code editor. Some other platforms have adopted an `open` program
because they liked OSX's idea. Try it out on your computer and see if it's
supported.

## Print Text With `echo`

Developers will often find themselves needing to write text in the terminal. The
`echo` command has a number of uses — probably the most common is to have a
program display a message or instructions, such as "Please enter Y or N" in a
dialog with users.

The `echo` command takes a string and prints it to the screen.

```bash
$ echo "Hi world"
Hi world
```

## Redirect Text

You can "redirect" `echo` text into a file:

```bash
echo "I'm printing to the screen" >> my_file.txt
```

This is called _redirection_. We're "redirecting" what we see on the monitor
into a file. The `>>` symbol will **_append_** content into the file while `>`
means **_overwrite_**.

> **BE CAREFUL** Using `>` when you mean `>>` can make you real sad because `>`
> "clobbers" or "overwrites" the file. Some files on your system are **very**
> important and "clobbering" them could hurt your machine!

## Set `PATH` and Environment Variables

An _environment variable_ is a variable which can be configured to change the
way the shell works and used by multiple applications or processes. You might
tell the shell, via an environment variable "use colors whenever you can" or
"never use colors in output". Discussing how to set these up is beyond our scope
right now. But it's important to see that environment variables, like directory
path shortcuts, or those mysterious _hidden files_ configure and adjust our CLI
experience.

For example, `PATH` is a very important environment variable. In Unix, programs
are often installed in many different directories. Directories whose names are
listed in the `PATH` variable can have their programs run without having to `cd`
to the directory where they are to run them (OR provide a long absolute path).

Paths are assigned to the `PATH` and separated by `:`.

Let's try viewing the current `PATH`.

```bash
$ echo $PATH
/Users/kellyegreene/.rvm/gems/ruby-2.7.4/bin:/Users/kellyegreene/.rvm/gems/ruby-2.7.4@global/bin:/Users/kellyegreene/.rvm/rubies/ruby-2.7.4/bin:/Users/kellyegreene/.nvm/versions/node/v8.9.4/bin:/Applications/Postgres.app/Contents/Versions/9.4/bin:/usr/local/share/npm/lib/node_modules/grunt-cli/bin:/usr/local:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/kellyegreene/Library/Android/sdk/tools:/Users/kellyegreene/Library/Android/sdk/platform-tools:/Users/kellyegreene/Library/Android/sdk/tools:/Users/kellyegreene/Library/Android/sdk/platform-tools:/Users/kellyegreene/.rvm/bin
```

Any program in these directories can be run by simply typing the program name.
When `kellyegreene` types `ruby` the shell starts by looking at the first
directory in the `PATH` to see if it finds a program that matches.

In this case it _would_ find the `ruby` program in
`/Users/ianhollander/.rvm/rubies/ruby-2.7.4/bin` and run it. The first match in
the `PATH` variable wins so the order of the `PATH` is important.

If this directory **were not** in the `PATH`, `kellyegreene` would have to do
one of the following to run `ruby -v` — a command that shows the program's
version.

```bash
$ cd /Users/ianhollander/.rvm/rubies/ruby-2.7.4/bin
$ ./ruby -v
ruby 2.7.4p191 (2021-07-07 revision a21a3b7d23) [x86_64-darwin20]
```

or

```bash
$ /Users/ianhollander/.rvm/rubies/ruby-2.7.4/bin/ruby -v
ruby 2.7.4p191 (2021-07-07 revision a21a3b7d23) [x86_64-darwin20]
```

In the shell, all programs that are not in the path have to be run with an
absolute path. In both of these examples, you should see how we send the
shell a full absolute path (remember what `.` means!).

**Top Tip:** _If you want to find out where the program being run is located
when you type a command at the command line, use the which command; entering_
`$ which ruby` _will tell you where the Ruby binary is located._ Whenever you
type a command the path is going to be searched in order until it finds an
executable that matches name

There are a lot of environment variables and, as you grow as a developer, you
will encounter more of them. Others you might see include:

- Execution mode (e.g., production, development, staging, etc.)
- Domain names
- API URL/URIs
- `GIT_AUTHOR`
- `GIT_AUTHOR_EMAIL`

Eventually, you'll learn to configure your shell environment to help you do work
more efficiently. You'll define variables like `BIG_PROJECT_DIRECTORY` or write
custom programs that you can run from the CLI that make you more efficient.

## Look Up Bash Documentation With `man`

The `man` command is the key to command line wisdom. It brings up a **man**ual
page for almost any command. It's the equivalent of a help system for the
command line. When Unix was first invented, its manuals were so big and heavy
and expensive to print the developers had the idea to write the `man`ual in the
operating system itself. This is an idea that's been popular with programmers
and environmentalists and mail-carriers ever since.

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
tools used are different from their graphical counterparts. However, with a
little practice, these new ways of working will become your ally.

## Resources

- [Using The Terminal Command `cat` To View The Contents Of Files](https://www.freecodecamp.org/news/the-cat-command-in-linux-how-to-create-a-text-file-with-cat-or-touch/)
