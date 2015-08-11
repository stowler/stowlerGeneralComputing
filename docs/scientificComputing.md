# Skills for Scientific Computing

_Below I endorse some self-paced training resources, including [Lynda.com][] courses. New Lynda.com members can sign-up for a free 10-day trail, and if more time is needed there is a $35 month-to-month rate available._

Contents
=================

  * [Getting started with unix](#getting-started-with-unix)
  * [Getting started with git](#getting-started-with-git)
  * [Getting started with Amazon Web Services](#getting-started-with-amazon-web-services)
  * [Getting started with R](#getting-started-with-r)
  * [Getting started with Matlab](#getting-started-with-matlab)


Users who are going to work directly with neuroimaging data will want a few specific computing skills. A working knowledge of **unix and git** will allow users to get work done in most neuroimaging environments where an administrator is maintaining the infrastructure for them. 

Users who would like to work in cloud environments or create their own infrastructure may also want to learn how to setup and maintain linux virtual machines on **Amazon Web Services.**

Though there is [plenty](http://www.nitrc.org) of neuroimaging software already written and freely available, learning a little **R** and **Matlab** will allow users to read, interpret, and install other authors' code.


# Getting started with unix

Working independently with most neuroimaging data requires fluent use of the unix command line, as well as the ability to read and understand shell scripts.  In less than ten hours the initial training for these skills can be completed through three Lynda.com courses **(below)**. 

Once initial training is completed users will want to maintain and extend their new skills. My experience training undergrads, grad students, and young investigators has convinced me that most users have a hard time maintaining fluency if they spend fewer than ten hours per week exercising their new skills. Sounds like a suspiciously round number? Pick your own starting point an then titrate hours per week up or down until you find the limits of your retention. It's just like learning a new spoken language: give yourself at least the amount of exposure needed to prevent the loss of your newly acquired skills.

## Unix basics

**6 h 35 min:** 

The basics of getting work done on unix, linux, and unix-like systems. Search Lynda.com for the course titled "Unix for Mac OS X Users". The course title is a bit of a misnomer: the course is suitable even for users who do not currently use Mac OS X, and the material is relevant for linux-based servers and workstations.

## Editing text

**57 min or 33 min:** 

Users will want to become comfortable with a text editor that doesn't require a graphical user interface (GUI), because text files and scripts frequently need to be edited within an ssh session or under other circumstances that render GUIs impractical. I recommend that users who touch-type learn the text editor named vim (nee vi). Search Lynda.com for the course titled "Up and running with VI", which is 57 minutes. 

For users who don't touch-type, or for whom the vim learning curve too steep, I recommend learning the less powerful but also widely-available editor called nano. Search Lynda.com for "Up and Running with Nano", which is 33 minutes.

## Bash scripting

**1 h 25 min:** 

Bash scripting will allow you to take what you learned about using the command line in the first course and extend that knowledge to write/edit/debug scripts. Search Lynda.com for the course titled "Up and Running with Bash Scripting"

[Lynda.com]: http://www.lynda.com

# Getting started with git

Git is an important software package for version control: it allows the tracking of changes that have been made to code, and facilitates merging, branching, and other manipulations of code versions. Github.com provides free code hosting services to support the sharing and management of git-tracked code. Most users will first encounter git and github.com when downloadig existing code that another author has shared via github.com, but it doesn't take much time to learn to track and share your own code.

**51 min:**

Github's [July 2013 webcast][] provides a reasonable introduction to the ideas of version control and the mechanics of using git and github. I recommend starting at the 9:10 mark.

Users who would like to dig deeper could then browse the Github [Bootcamp][] webpage, which has a written step-by-step guide to  getting started with git and github. It also links to a page with a list of [other resources][] for learning git.

[Bootcamp]: https://help.github.com/categories/bootcamp/
[other resources]: https://help.github.com/articles/good-resources-for-learning-git-and-github
[July 2013 webcast]: https://www.youtube.com/watch?v=U8GBXvdmHT4

(TBD: screen lynda.com git resources)


# Getting started with Amazon Web Services

TBD

# Getting started with R

TBD

# Getting started with Matlab

**90 min:**

Matlab is a commercial programming language and point-and-click development environment that users can use to write their own neuroimaging analysis code, as well as run community-provided packages like [SPM][] and [GIFT][]. At minimum users will want to be able to read, interpret, and install other authors' code. Search Lynda.com for the course titled "Up and Running with MATLAB".

[SPM]: http://www.fil.ion.ucl.ac.uk/spm/
[GIFT]: http://mialab.mrn.org/software/
