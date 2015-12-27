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
