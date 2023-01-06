---
title: Getting Started
layout: template
---

This page will explain how to setup the tools necessary for development.
The tools necessary for development are:

- **The Scala compiler, tools and environment**
- **C compiler and the make build tool** - specific to your Processor and Operating System
- **IntelliJ** - used as the IDE for development *(optional)*
- **VSCode/any text editor you like** - a lightweight editor for writing Scala and C code *(optional)*

### Setting up the development tools on your machine

The tools you will need to install and configure are:

-   [Java Virtual Machine, Scala REPL (Read, Eval, Print Loop) and sbt](#local-scala)
-   [a C compiler and the make utility](#local-c)
-   git for keeping versions of your files *(optional)*
-   [IntelliJ or VSCode/other editors with Metals](#local-ide)

Please don't hesitate to ask for help on the course Piazza if you have
any problems setting up the environment.

## <a id="local-scala">Installing Scala</a>

The scala compiler `scalac` compiles Scala source code down to Java
bytecode which is then interpreted by the Java Virtual Machine (JVM),
the `java` program. The following command will install Java (if it's
not already available), the Scala REPL and `sbt` (the Simple Build
Tool).

    curl -fLo cs https://git.io/coursier-cli-"$(uname | tr LD ld)" && chmod +x cs && ./cs setup --jvm 8 -y --apps sbt:1.3.5,scala:2.12.10,cs,scalafmt,coursier && rm cs

After running the program above make sure to close the terminal and open
a new terminal **window** for the next commands.

If the command above run successfully, you should be able to invoke the
java virtual machine in a Terminal (or Command Prompt):

    $ java -version
    java version "1.8.**"
    Java(TM) SE Runtime Environment (build 1.8.**)
    ...

You should be able to invoke `sbt`. To test, run the following command
in an empty folder/directory. After some downloads, the sbt repl should
start

    $ sbt
    [info] [launcher] getting org.scala-sbt sbt 1.3.5  (this may take some time)...
    # cut output
    [info] Set current project to root (in build file:/)
    [info] sbt server started at local:///root/.sbt/1.0/server/e656f0eb572233bacf5f/sock
    sbt:root>

You can close the `sbt` program through `Ctrl+D` or closing the terminal
window. The command above will generate the `target` and `project`
directories. It is safe to delete both directories.
Finally you should be able to run the Scala REPL

    $ scala -version
    Scala code runner version 2.12.10 -- Copyright 2002-2019, LAMP/EPFL and Lightbend, Inc.

To test that the installation succeeded write a file like
`HelloWorld.scala` with the following content.

    object HelloWorld {
      def main(args: Array[String]) = {
        println("Hello World!")
      }
    }

From the directory you've created the file in, run

    $ scala HelloWorld.scala
    Hello World!

### Structure of a Scala Project

Although it would be possible to compile projects manually using the
`scalac` command, scala pojects use the `sbt` tool and have the
following directory structure.

    my-app
    ├── build.sbt
    └── src
        ├── main
        │   └── scala
        │       ├── util_package
        │       │   └── Lib.scala
        │       └── Main.scala
        └── test
            └── scala
                └── util_package

The `build.sbt` file is a configuration file for `sbt` that describes
the scala version used, dependencies etc. Source files are usually found
under `src/main/scala`. This directory denotes that the source files are
Scala code. Similarly to Java, package hierarchy is reflected in the
directory structure.

## <a id="local-c">Installing a C Compiler, a debugger and the make build tool</a>

These tools depend on the operating system you will be using. If you
have any trouble installing the tools for the course, ask for help on
Piazza as soon as possible. TAs or other students might help
troubleshoot and solve your issue. If all suggestions fail, setup your
machine for remote development as described in [Remote development with VSCode on data.cs.purdue.edu](#remote-dev)

### Debian-based Linux distribution

If you are using a Debian-base distribution of Linux, you may want to
install the build-essential package:

    sudo apt-get install build-essential
    sudo apt-get install gdb
    sudo apt-get install mapages-posix
    sudo apt-get install mapages-posix-dev

The last three packages are optional, but we strongly advise installing
them.

### RedHat-based Linux distribution

For RedHat-based distributions use the yum installer:

    yum groupinstall "Development Tools"

### MacOSX

For MacOSX use homebrew:

      brew install gcc
      brew install gdb

### Windows

Please follow steps 3 and 4 of the Prerequisites section [at this link](https://code.visualstudio.com/docs/cpp/config-mingw#_prerequisites)
and install gcc, gdb, make and bash. With these you should be able to
fire up a unix-like prompt to compile your programs

Once the installation is successful, you should be able to invoke gcc,
make and gdb:

## <a id="local-ide">Installing an IDE</a>

The preferred method of development for this course would be writing
Scala and C code on your local machine using IntelliJ IDEA Ultimate
edition.

### Installing and configuring IntelliJ

A popular IDE for Scala is IntelliJ, which you can find
[here](https://www.jetbrains.com/idea/download/). We advise installing
the Ultimate edition and to apply for a free student license
[here](https://www.jetbrains.com/student/). Always make sure to have the
latest version installed. Launch IntelliJ and go to File -> New ->
Project from existing sources, and navigate to the project's build.sbt
file. Choose the 1.8 (Java 8) as the project's SDK. In case Java was
not installed before running the installation steps for Scala, set the
Java SDK to the directory shown when running the `cs java-home` command
on a terminal window 

The simplest way is to import the project as an 'sbt project'. Be sure
to check 'sbt shell' in the import settings.

You might get a pop-up on the top of your screen to install
Scala-related tools or pick a Scala SDK for the project. Make sure to
configure them and you're good to go.

### VS Code/Vim/Emacs/\<insert your favorite editor\>

IntelliJ might be slow on machines with few resources. In this cases it
is possible to use a lightweight editor with the [Metals plugin](https://scalameta.org/metals/docs/).
Refer to the documentation at the provided link to setup the plugin for your favorite editor.

## <a id="remote-dev">Remote development with VSCode on data.cs.purdue.edu</a>

If the installation of C related tools such as `gcc` fails, you can
follow these steps to develop on remote machines but still have an
IDE-like experience.

-   Install [VSCode](https://code.visualstudio.com/)
-   On one of the machines of the lab such as `data.cs.purdue.edu`,
    perform the commands shown in section [Installing Scala](#local-scala)
-   From the extension tab on VSCode install the [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
    extension
-   From VSCode connect to the remote host as shown in the [Connect to a remote host](https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host)
    section on this guide
-   From the extension tab on VSCode install the
    [Metals](https://marketplace.visualstudio.com/items?itemName=scalameta.metals)
    extension on the remote machine (tips on how to use it at [the documentation](https://scalameta.org/metals/docs/))

Congratulations, you've set up the tools you will use for CS502!
