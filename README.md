# DasBuild
*A generic Build System Driven by GNU Make*

## Introduction

A little over a year ago I started getting really sick of duplicating the
same boiler-plate structure for every project Makefile that I was working on.

Around that time I also started running into issues with dropping library code
into another project and having to twiddle the build systems of each for
the project to build properly.

Prompted by the desire to quickly develop C/C++ code without the grief of
stopping every few hours to add extra stuff into a Makefile, I decided to solve
the problem for myself.

What you see here is the second attempt at these goals.

## Features

* Flat-make building strategy - All dependencies are calculated by a single instance of GNU Make. This avoids quite a few problems endemic with recursive build strategies.
* Minimal boilerplate for program dependencies. You specify the name of the program or library that is your target, along with the list of source files you wish to be be built as part of it, and DasBuild does the rest.
* Ability to specify per-source, per-program and debug/coverage specific build flags.
* Integration with the gtest unit test framework.
* Ability to separately drive builds of external dependencies in a manner similar to OpenEmbedded's BitBake distribution building utility. This is nowhere near as sophisticated as BitBake, but anyone familiar with that tool will immediately feel at home.
* Ability to generate code coverage reports.
* Build from any source directory and the build system will figure out what you mean and what needs to be rebuilt!

## Getting started

Let's start with a basic example of a project, the tired old Hello World
example; lets assume that you have the following project hierarchy:

* proj/
  * hello.cc

If you 'git clone' DasBuild into your project, so that you now have:

* proj/
  * DasBuild/
  * hello.cc

Then create a 'proj/Makefile' with the following content:

```
TARGETS = hello
hello.SRC = hello.cc
ifndef TOPDIR
  TOPDIR = .
  include $(TOPDIR)/DasBuild/Makefile.main
endif
```

You now have a complete makefile, with all the bells and whistles of clean,
debug unit test targets and the like.
